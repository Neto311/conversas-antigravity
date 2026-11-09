# Resumo de Desenvolvimento — Bot_Financa (09.11.2026)

Este documento consolida todo o progresso, decisões arquiteturais e próximos passos do projeto **`bot_finance`** (`https://github.com/Neto311/bot_finance`).

---

## 1. O que já foi implementado e enviado ao GitHub

### Parte A — Paginação Mensal no Bot do Telegram
- **Branch:** `feature/paginacao-mensal-me` (commit `d45fe2e`)
- **Arquivos alterados:** `services/bot_telegram.py`
- **O que entrou:**
  - Ajuste em `montar_headers` usando `update.effective_message` para suportar tanto mensagens comuns quanto cliques em botões inline (`CallbackQuery`).
  - Extração da função reutilizável `montar_blocos_transacoes_mes(dados, provedor)` (ordena por data, agrupa por dia `dd/mm` e divide em blocos de até 4000 caracteres).
  - Handler assíncrono `ver_mais_mes_minhas_economias` registrado via `CallbackQueryHandler(ver_mais_mes_minhas_economias, pattern="^mes_me_ver_mais$")`, com proteção contra clique duplo (`message_id` + flag `carregando`), busca paginada por `cursor` em `/financas/mes/minhas-economias` e atualização/remoção automática do botão **“Ver mais ➡️”**.

---

### Parte B — Fase 1 da Plataforma Própria (Autenticação JWT + Google + Modo Dual)
- **Branch atual:** `feature/app-chat-auth` (commit `84469fc`)
- **Decisões de Produto e Arquitetura fechadas:**
  - **Monorepo:** App Mobile dedicado em **React Native + Expo (TypeScript)** dentro de `bot_finance/mobile/`, versionado junto com a API.
  - **Modelo de trabalho:** No backend Python (FastAPI / SQLAlchemy / Alembic) o desenvolvimento é guiado de forma didática e incremental; no frontend mobile (Expo / TypeScript) os componentes e telas são construídos com explicação passo a passo.
  - **Login:** E-mail/Senha (Argon2 via `pwdlib`) + Login Social Google usando a tabela `identidades_externas`, emitindo **JWT** (`access_token` de 60 min + `refresh_token` de 30 dias). *Sign in with Apple* preparado para futuro lançamento iOS.
  - **Modo Dual:** As rotas aceitam tanto `Bearer <JWT>` (App/Web) quanto `Bearer <INTERNAL_API_KEY>` + headers de identidade (`X-Identity-Provider` / `X-External-Identity` do Telegram) durante a transição.
  - **Onboarding sem atrito:** Criar conta no App já define o banco `"local"` automaticamente como integração principal. Integrações externas (Minhas Economias e futuro Open Finance) ficam em `⚙️ Configurações` no topo do Chat.
  - **Escopo Financeiro:** Suporte a **`GASTO`** e **`GANHO`** já no MVP do App.
  - **Chat Híbrido Inteligente via REST:** Classificação de intenção no Groq (diferenciando registros financeiros de consultas como saldo/resumo/extrato), transcrição de áudio no Whisper salvando texto + duração na bolha (sem armazenamento pesado de arquivos de áudio no MVP), cards interativos com botões `[✏️ Editar]` e `[🗑️ Excluir]` na própria conversa e chips rápidos de 1 toque.

- **Arquivos criados/atualizados na Fase 1 (`ruff` 100% aprovado):**
  1. `models/financas.py` — Adicionadas colunas `email` (`NOT NULL`, `UNIQUE`, `INDEX`) e `senha_hash` (`NULLABLE`) em `Usuario`.
  2. `migrations/versions/8ed0041efad7_add_email_and_senha_hash_to_usuarios.py` — Migration em 3 etapas (`add_column` nullable → backfill nos usuários legados do Telegram → `alter_column` `NOT NULL` + índice único).
  3. `repositories/identidade_externa_repository.py` — Preenchimento de e-mail placeholder legado em `obter_ou_criar_usuario`.
  4. `schemas/auth.py` — Schemas Pydantic (`RequestRegistro`, `RequestLogin`, `RequestGoogleAuth`, `RequestRefresh`, `ResponseUsuarioAuth`, `ResponseTokens`).
  5. `services/auth_service.py` — Hash Argon2 (`gerar_hash_senha`, `verificar_senha`), geração/decodificação JWT (`criar_access_token`, `criar_refresh_token`, `decodificar_token`) e validação Google (`validar_token_google`).
  6. `dependencies/autenticacao_servico.py` e `dependencies/identidade.py` — Modo Dual (JWT ou `INTERNAL_API_KEY`).
  7. `routes/auth.py` e `main.py` — Rotas `POST /auth/registro`, `POST /auth/login`, `POST /auth/google`, `POST /auth/refresh`, `GET /auth/me` + `CORSMiddleware`.

---

## 2. Como sincronizar o ambiente em outro computador

```powershell
git fetch origin
git checkout feature/app-chat-auth
git pull origin feature/app-chat-auth

# Instalar os novos pacotes de Auth na .venv:
pip install "pwdlib[argon2]" google-auth email-validator

# Garantir que no .env existam:
# JWT_SECRET_KEY=<uma_chave_segura>
# GOOGLE_CLIENT_ID=

# Aplicar a migration nova no banco PostgreSQL local:
alembic upgrade head
```

---

## 3. Próximos Passos (A partir da Fase 2)

### Fase 2 — Backend: Suporte a `GANHO` + Motor de Chat Inteligente
1. **Passo 2.1 (Próximo imediato) — Liberar `GANHO` além de `GASTO` em `routes/routes.py`:**
   - `validar_dados`: aceitar `tipo in {"GASTO", "GANHO"}` e retornar `"tipo": tipo`.
   - `salvar_financa`: subtrair do `usuario.saldo` se `GASTO` e somar se `GANHO`.
   - `atualizar_transacao`: remover bloqueio de `GANHO`, estornar o valor antigo conforme o tipo antigo, atualizar `transacao.tipo` e aplicar o valor novo conforme o tipo novo.
   - `resumo`: separar a soma de `gasto_total` (só `GASTO`) e `ganho_total` (só `GANHO`), retornando também `"ganho_total"` e `"saldo_mes"`.
2. **Passo 2.2 — Tabela `mensagens_chat` (`models/chat.py` + Migration Alembic):**
   - Salvar histórico de mensagens do usuário e do assistente (`remetente`, `tipo`, `conteudo`, `dados_extras` JSON para os cards e duração de áudio, `criado_em`).
3. **Passo 2.3 — Classificador de Intenção e `services/chat_service.py`:**
   - Evoluir `services/groq_client.py` para identificar se o texto/áudio do usuário é um registro (`GASTO`/`GANHO`) ou uma pergunta/consulta (saldo, resumo do mês, últimos lançamentos, ajuda).
4. **Passo 2.4 — Rotas do Chat (`routes/chat.py`):**
   - `GET /chat/mensagens` (histórico paginado por cursor), `POST /chat/texto` e `POST /chat/audio` (transcrição no Whisper salvando texto + duração na bolha).

### Fase 3 & Fase 4 — App Mobile em React Native / Expo
- **Fase 3:** Criar `bot_finance/mobile/` com Expo Router, `expo-secure-store`, cliente HTTP com auto-refresh de JWT e telas de Login / Cadastro / Google.
- **Fase 4:** Tela principal de Chat estilo WhatsApp com gravação de áudio nativo, barra de chips rápidos de 1 toque, cards interativos de transação (verde/vermelho com botões `[✏️ Editar]` e `[🗑️ Excluir]` na própria conversa) e modal `⚙️ Integrações`.
