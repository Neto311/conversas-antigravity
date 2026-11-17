# Roadmap Master: Engenharia Backend, Arquitetura, Java & Inteligência Artificial

> **Objetivo:** Construir uma formação completa e progressiva em engenharia de software, saindo dos fundamentos de Python e SQL até sistemas distribuídos de alta escala, Java empresarial (foco em bancos/fintechs), Cibersegurança aplicada e Inteligência Artificial (Agentes, RAG e Machine Learning).

## Cronograma Executivo (Base: 30 a 60 min/dia + Prática)

> **Nota Importante:** As estimativas abaixo consideram o seu ritmo atual (30 a 60 minutos diários além da faculdade e estágio). **Você não precisa esperar o fim do roadmap para entrar no mercado** — o gatilho de candidatura para vagas Júnior acontece logo após a Fase 1.

| Fase | Foco Principal | Duração Estimada | Tempo Acumulado | Marco de Carreira / Entrega |
| :--- | :--- | :--- | :--- | :--- |
| **Fase 1** | SQL, FastAPI, ORM, Auth, Testes & Docker | **5 a 7 meses** | ~6 meses | **Pronto para Vagas Júnior Backend** |
| **Fase 2** | Engenharia de IA Aplicada (LLMs, RAG & Agentes) | **3 a 4 meses** | ~9 a 11 meses | Diferencial competitivo em IA aplicada |
| **Fase 3** | Arquitetura, Concorrência, Redis, Filas & Observabilidade | **6 a 8 meses** | ~15 a 19 meses | **Maturidade Técnica Nível Pleno** |
| **Fase 4** | Java 17/21 LTS, Spring Boot, Security & Kafka | **7 a 10 meses** | ~22 a 29 meses | **Stack Corporativa para Grandes Bancos** |
| **Fase 5** | Ciência de Dados, Machine Learning & MLOps | **8 a 12 meses** | ~30 a 41 meses | Especialização em Modelos Preditivos & Visão |

---

## Fase 1: Fundação Backend, Persistência & Segurança Básica `[5 a 7 meses | Meta: Vaga Júnior]`

O objetivo desta fase é dominar o fluxo completo de uma aplicação web moderna: receber requisições HTTP, validar contratos, aplicar regras de negócio seguras, persistir em banco relacional e empacotar tudo com testes automatizados.

### 1.1 Bancos de Dados Relacionais & SQL Puro *(~4 a 6 semanas)*

* **No Curso:** **Seção 19 inteira** (Modelagem, DER, SQL) e **Seção 8** (Drivers Python e SQL Injection).
* [ ] **Modelagem de Dados:** `Entity-Relationship Diagram (ERD)`, chaves primárias/estrangeiras, cardinalidade (`1:1`, `1:N`, `N:N` com tabelas associativas), normalização (`1FN`, `2FN`, `3FN`).
* [ ] **SQL Avançado:** `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `GROUP BY`, `HAVING`, funções de agregação (`COUNT`, `SUM`, `AVG`), subqueries e `CTE (Common Table Expressions)`.
* [ ] **Integridade e Transações:** `ACID properties`, `BEGIN / COMMIT / ROLLBACK`, constraints (`ON DELETE CASCADE / RESTRICT`), índices básicos (`B-Tree`).
* [ ] **Drivers & Segurança:** Python DB-API (`PyMySQL`, `psycopg3`), cursores e prevenção de SQL Injection via *parameterized queries*.

### 1.2 APIs REST, FastAPI & ORM Moderno *(~8 a 10 semanas)*

* **No Curso:** **Seção 15** (*Type Annotations* — base para Pydantic).
* **Por Fora:** Documentação oficial do FastAPI, SQLAlchemy e Alembic.
* [ ] **Fundamentos Web & HTTP:** Métodos (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`), Status Codes (`2xx`, `4xx`, `5xx`), Headers, `CORS`, arquitetura *Stateless* e JSON.
* [ ] **FastAPI & Contratos:** Roteamento, `Dependency Injection (Depends)`, validação e serialização estrita com **Pydantic v2**, documentação OpenAPI/Swagger.
* [ ] **Persistência & Migrações:** **SQLAlchemy 2.0** (mapeamento declarativo, sessões, relacionamentos, prevenção do problema `N+1`) e **Alembic** (versionamento de schema e migrations).

### 1.3 Autenticação, AppSec Básico & Qualidade *(~8 a 12 semanas — inclui projeto de portfólio)*

* **No Curso:** **Seção 14** (mentalidade de TDD e testes unitários).
* [ ] **Autenticação & Autorização:** Hashing seguro de senhas (`Argon2` / `bcrypt`), **JWT (JSON Web Tokens)** (*Access* e *Refresh Tokens*), `OAuth2 Password Flow` e `RBAC (Role-Based Access Control)`.
* [ ] **Segurança Defensiva (OWASP Top 10):** Proteção contra `Broken Access Control (IDOR)` (garantir isolamento de dados por usuário), gestão de segredos com `.env` e princípio do menor privilégio no banco.
* [ ] **Testes Automatizados:** **`pytest`**, `fixtures`, mocks e testes de integração de endpoints com `httpx.AsyncClient`.
* [ ] **Containerização & Git:** `Dockerfile` multi-stage, **`Docker Compose`** (orquestrando API + PostgreSQL), fluxo Git profissional (`Conventional Commits`, Pull Requests) e CI básico no **GitHub Actions**.

---

## Fase 2: Engenharia de IA Aplicada (LLMs, RAG e Agentes) `[3 a 4 meses | Pós-Fase 1]`

* **Por que aqui?** Porque integrar LLMs em produção depende 80% do que você acabou de construir na Fase 1 (FastAPI, Pydantic, PostgreSQL e requisições assíncronas).

### 2.1 APIs de LLM, Prompts & Contratos Estritos *(~4 a 6 semanas)*

* [ ] **Mecânica & SDKs:** SDKs oficiais (OpenAI, Google GenAI, Anthropic), `Context Window`, `Tokenization`, custos (`Input vs Output`), `Temperature`, `TTFT` e `Server-Sent Events (SSE) Streaming`.
* [ ] **Structured Outputs:** Forçar respostas tipadas e validadas com **Pydantic / JSON Schema**.
* [ ] **Engenharia de Prompt Sistemática:** `System vs Developer vs User Prompts`, `Few-Shot Prompting`, `Chain-of-Thought (CoT)`, delimitadores XML e versionamento de prompts.

### 2.2 Tool Use, RAG & Orquestração de Agentes *(~8 a 10 semanas)*

* [ ] **Function Calling & MCP:** `Tool Use loop` (LLM acionando funções Python com validação determinística) e **Model Context Protocol (MCP)**.
* [ ] **RAG (Retrieval-Augmented Generation):** `Text Embeddings`, busca vetorial no PostgreSQL com **`pgvector`** (`HNSW`), estratégias de `Chunking`, `Hybrid Search (BM25 + Vetorial)` e `Reranking`.
* [ ] **Arquitetura de Agentes:** Padrões (*Routing*, *Prompt Chaining*, *Reflection*), máquinas de estado com **LangGraph** ou **PydanticAI**, persistência de memória (`Checkpointers`) e `Human-in-the-Loop (HITL)`.
* [ ] **LLMOps & Segurança de IA:** Testes com `LLM Evals` (`Golden Datasets`, `LLM-as-a-Judge`), tracing com **Langfuse / OpenTelemetry**, defesa contra `Prompt Injection` e mascaramento de dados sensíveis (`PII Redaction`).

---

## Fase 3: Engenharia de Software, Concorrência & Sistemas Distribuídos `[6 a 8 meses | Meta: Nível Pleno]`

Aqui você deixa de apenas construir CRUDs e aprende a projetar sistemas resilientes, escaláveis, desacoplados e observáveis.

### 3.1 Engenharia de Software & Arquitetura *(~8 a 10 semanas)*

* **No Curso:** **Seção 17** (*Design Patterns* — GoF).
* [ ] **Princípios & Padrões:** **SOLID**, *Design Patterns* criacionais, estruturais e comportamentais (`Repository`, `Service Layer`, `Factory`, `Strategy`, `Adapter`, `Dependency Injection`).
* [ ] **Arquitetura de Software:** *Clean Architecture*, *Hexagonal Architecture (Ports & Adapters)* e fundamentos de *Domain-Driven Design (DDD)* tático (Entidades, Value Objects, Aggregates).

### 3.2 Concorrência, Cache & Mensageria *(~10 a 12 semanas)*

* [ ] **Concorrência & Paralelismo:** Diferença real entre tarefas `I/O-Bound` e `CPU-Bound`, **`asyncio`**, *Event Loop*, corrotinas, `Multithreading` (GIL) vs `Multiprocessing`.
* [ ] **Cache & Estado em Memória:** **Redis** (estratégias `Cache-Aside`, invalidação, TTL, armazenamento de sessões e `Rate Limiting` distribuído).
* [ ] **Mensageria & Processamento Assíncrono:** Brokers (**RabbitMQ**), filas de tarefas em background (**Celery** ou **`arq`**), conceitos de `Dead Letter Queues (DLQ)`, `Idempotência` e garantia de entrega (*At-least-once*).

### 3.3 Observabilidade & DevSecOps Corporativo *(~6 a 8 semanas)*

* [ ] **Observabilidade (Os 3 Pilares):**
  * *Logs:* Structured Logging em JSON com `Correlation ID` (nunca logar senhas/tokens).
  * *Métricas:* **Prometheus** e dashboards no **Grafana** (latência p95/p99, taxa de erro, throughput).
  * *Tracing:* **OpenTelemetry** para rastrear requisições entre serviços.
* [ ] **Segurança Avançada (AppSec / DevSecOps):** Análise estática (`Bandit`), análise de vulnerabilidades em dependências (`pip-audit`), scan de imagens Docker (`Trivy`), criptografia em trânsito/repouso (`TLS`, `mTLS`, `AES-256`) e conformidade LGPD.

---

## Fase 4: Ecossistema Java Empresarial `[7 a 10 meses | Foco: Grandes Bancos & Fintechs]`

* **Por que aqui?** Toda a teoria de SQL, HTTP, transações, mensageria, testes e arquitetura já foi dominada. O foco agora é aprender a linguagem estática e o ecossistema padrão do setor financeiro.

* [ ] **Java Core & JVM *(~10 a 12 semanas)*:** Java 17 / 21 LTS, tipagem estática forte, `Collections Framework`, `Generics`, `Streams API`, `Lambdas`, gerenciamento de memória da **JVM** (`Heap`, `Stack`, `Garbage Collectors`) e build com **Maven** ou **Gradle**.
* [ ] **Spring Boot & Persistência *(~10 a 14 semanas)*:** `Spring Core (IoC / DI)`, `Spring Web`, **Spring Data JPA / Hibernate** (ciclo de vida das entidades, transações declarativas `@Transactional`, prevenção de `LazyInitializationException` e `N+1`).
* [ ] **Segurança & Testes no Java *(~4 a 6 semanas)*:** **Spring Security** (cadeia de filtros, OAuth2, JWT), **JUnit 5**, **Mockito** e **Testcontainers** (subindo PostgreSQL/Kafka reais em Docker durante os testes).
* [ ] **Mensageria de Alta Escala & Resiliência *(~4 a 8 semanas)*:** **Apache Kafka** (`Topics`, `Partitions`, `Consumer Groups`, `Offsets`) com Spring Kafka e padrões de resiliência com **Resilience4j** (`Circuit Breaker`, `Retry`, `Bulkhead`).

---

## Fase 5: Ciência de Dados, Machine Learning & MLOps `[8 a 12 meses | Longo Prazo]`

* **Foco:** Construir, treinar e disponibilizar modelos preditivos próprios (ex.: detecção de fraude bancária, credit scoring) e modelos de visão computacional.

| Etapa | Duração Estimada | Conceitos & Termos para Pesquisa | Ferramentas / Bibliotecas | Status |
| :--- | :--- | :--- | :--- | :--- |
| **1. Matemática & Dados** | ~8 a 12 semanas | `Linear Algebra`, `Calculus (Gradients)`, `Probability & Statistics`, `Vectorization` | `NumPy`, `Pandas` | `[ ]` |
| **2. ML Clássico (Tabular)** | ~10 a 14 semanas | `Supervised/Unsupervised Learning`, `Feature Engineering`, `Cross-Validation`, `ROC-AUC`, `Precision/Recall` | `Scikit-learn`, `XGBoost`, `LightGBM` | `[ ]` |
| **3. Deep Learning & Visão** | ~10 a 14 semanas | `Neural Networks`, `Backpropagation`, `CNNs`, `Transfer Learning`, `Object Detection` | `PyTorch`, `OpenCV`, `YOLO` | `[ ]` |
| **4. MLOps & Serving** | ~4 a 8 semanas | `Model Serialization (ONNX)`, `Feature Stores`, `Data Drift`, `Experiment Tracking` | `FastAPI`, `ONNX Runtime`, `MLflow`, `DVC` | `[ ]` |

---

## Biblioteca Recomendada (Por Etapa)

### Leitura Imediata (Mentalidade, Algoritmos e Código Limpo)

1. **O Programador Pragmático** (*Andrew Hunt & David Thomas*) — *Mentalidade profissional, responsabilidade e como não programar por coincidência usando IA.*
2. **Entendendo Algoritmos** (*Aditya Bhargava*) — *Apoio visual direto para a prática diária no Beecrowd (Big-O, grafos, tabelas hash, PD).*
3. **A Philosophy of Software Design** (*John Ousterhout*) — *Combate à complexidade e identificação de abstrações rasas geradas por LLMs.*
4. **Código Limpo (Clean Code)** (*Robert C. Martin*) — *Legibilidade, nomeação e organização de funções (prepara também para a sintaxe Java).*
5. **Python Fluente** (*Luciano Ramalho*) — *Livro de consulta para Python idiomático, iteradores, decoradores e concorrência.*

### Médio e Longo Prazo (Dados, Arquitetura e IA)

6. **AI Engineering: Building Applications with Foundation Models** (*Chip Huyen*) — *Engenharia de produção sobre LLMs: prompts, RAG, agentes, Evals e otimização.*
7. **Designing Data-Intensive Applications** (*Martin Kleppmann*) — *A bíblia de backend: armazenamento, índices, transações, replicação, particionamento e mensageria.*

---

## Mapa Visual Completo (Estilo roadmap.sh)

> **Legenda de Cores:**
> * 🟨 **Amarelo:** Fase 1 (5–7 meses) — Fundação Backend, Persistência & AppSec Básico
> * 🟪 **Roxo:** Fase 2 (3–4 meses) — Engenharia de IA Aplicada (LLMs, RAG & Agentes)
> * 🟧 **Laranja:** Fase 3 (6–8 meses) — Arquitetura, Concorrência, Redis, Mensageria & Observabilidade
> * 🟥 **Vermelho:** Fase 4 (7–10 meses) — Ecossistema Java Empresarial & Spring (Bancos)
> * 🟦 **Azul:** Fase 5 (8–12 meses) — Machine Learning, Deep Learning & MLOps
> * 🟩 **Verde:** Marcos de Carreira e Projetos Práticos

```mermaid
flowchart TD
    %% Estilos inspirados no roadmap.sh
    classDef phase1 fill:#fef08a,stroke:#ca8a04,stroke-width:2px,color:#1f2937,font-weight:bold;
    classDef phase2 fill:#e9d5ff,stroke:#7e22ce,stroke-width:2px,color:#1f2937,font-weight:bold;
    classDef phase3 fill:#fed7aa,stroke:#c2410c,stroke-width:2px,color:#1f2937,font-weight:bold;
    classDef phase4 fill:#fecaca,stroke:#b91c1c,stroke-width:2px,color:#1f2937,font-weight:bold;
    classDef phase5 fill:#bfdbfe,stroke:#1d4ed8,stroke-width:2px,color:#1f2937,font-weight:bold;
    classDef sub fill:#ffffff,stroke:#4b5563,stroke-width:1.5px,color:#111827;
    classDef milestone fill:#bbf7d0,stroke:#15803d,stroke-width:2.5px,color:#14532d,font-weight:bold;

    %% Tronco Principal
    START(["Início: Python Base + Algoritmos (Beecrowd)"]):::milestone

    %% Fase 1 (5-7 meses)
    P1_SQL["1. SQL & Modelagem Relacional [4–6 sem]<br/>(Curso Seções 19 e 8)"]:::phase1
    P1_API["2. FastAPI + Pydantic v2 + PostgreSQL [4–5 sem]"]:::phase1
    P1_ORM["3. SQLAlchemy 2.0 & Alembic [4–5 sem]"]:::phase1
    P1_SEC["4. Auth (JWT), AppSec & Pytest [4–6 sem]"]:::phase1
    P1_DOC["5. Docker, Docker Compose & CI [4–6 sem]"]:::phase1
    M_JR(["MARCO 1 (~6 meses): Portfólio Backend Pronto<br/>Apto para Vagas Júnior"]):::milestone

    %% Fase 2 (3-4 meses)
    P2_LLM["6. APIs de LLM & Structured Outputs [4–6 sem]"]:::phase2
    P2_RAG["7. Tool Calling, MCP & RAG (pgvector) [4–5 sem]"]:::phase2
    P2_AGT["8. Orquestração de Agentes & LLMOps [4–5 sem]"]:::phase2

    %% Fase 3 (6-8 meses)
    P3_ARCH["9. SOLID, Design Patterns (Seção 17) & Clean Arch [8–10 sem]"]:::phase3
    P3_ASYNC["10. Concorrência (AsyncIO) & Redis [5–6 sem]"]:::phase3
    P3_MSG["11. Mensageria (RabbitMQ) & Filas [5–6 sem]"]:::phase3
    P3_OBS["12. Observabilidade & DevSecOps [6–8 sem]"]:::phase3
    M_PL(["MARCO 2 (~18 meses): Engenharia Distribuída<br/>Maturidade Técnica Pleno"]):::milestone

    %% Fase 4 (7-10 meses)
    P4_JAVA["13. Java 17/21 LTS, JVM & Maven/Gradle [10–12 sem]"]:::phase4
    P4_SPRING["14. Spring Boot, Data JPA & Spring Security [14–20 sem]"]:::phase4
    P4_KAFKA["15. Apache Kafka, Testcontainers & Resiliência [4–8 sem]"]:::phase4
    M_BANK(["MARCO 3 (~28 meses): Stack Corporativa Completa<br/>Pronto para Grandes Bancos"]):::milestone

    %% Fase 5 (8-12 meses)
    P5_DATA["16. Matemática, NumPy & Pandas [8–12 sem]"]:::phase5
    P5_ML["17. Machine Learning & Deep Learning [20–28 sem]"]:::phase5
    P5_MLOPS["18. MLOps & Serving Escalável [4–8 sem]"]:::phase5

    %% Conexões Principais
    START --> P1_SQL --> P1_API --> P1_ORM --> P1_SEC --> P1_DOC --> M_JR
    M_JR --> P2_LLM --> P2_RAG --> P2_AGT
    P2_AGT --> P3_ARCH --> P3_ASYNC --> P3_MSG --> P3_OBS --> M_PL
    M_PL --> P4_JAVA --> P4_SPRING --> P4_KAFKA --> M_BANK
    M_BANK --> P5_DATA --> P5_ML --> P5_MLOPS

    %% Ramificações Laterais (Estilo roadmap.sh)
    P1_SQL -.- S1["DER, 1:N, N:N, JOINs, GROUP BY<br/>Transações ACID & Queries Parametrizadas"]:::sub
    P1_API -.- S2["HTTP, REST, Status Codes<br/>Type Hints (Seção 15) & Depends"]:::sub
    P1_ORM -.- S3["Models, Sessões, Migrations<br/>Prevenção do problema N+1"]:::sub
    P1_SEC -.- S4["Argon2/Bcrypt, RBAC, IDOR<br/>Fixtures & httpx.AsyncClient"]:::sub
    P1_DOC -.- S5["Dockerfile Multi-stage, .env<br/>GitHub Actions CI"]:::sub

    P2_LLM -.- S6["Tokens, SSE Streaming, Prompting<br/>Validação JSON com Pydantic"]:::sub
    P2_RAG -.- S7["Embeddings, Chunking, HNSW<br/>Hybrid Search (BM25 + Vetor)"]:::sub
    P2_AGT -.- S8["LangGraph / PydanticAI, HITL<br/>Evals, Langfuse & PII Guardrails"]:::sub

    P3_ARCH -.- S9["Repository, Strategy, Factory<br/>Hexagonal Arch & DDD Tático"]:::sub
    P3_ASYNC -.- S10["Event Loop, I/O vs CPU-Bound<br/>Cache-Aside & Rate Limiting"]:::sub
    P3_MSG -.- S11["Celery / arq, DLQ<br/>Idempotência & At-least-once"]:::sub
    P3_OBS -.- S12["OpenTelemetry, Prometheus, Grafana<br/>Trivy, Bandit, mTLS & LGPD"]:::sub

    P4_JAVA -.- S13["Heap/Stack, GC, Streams API<br/>Collections & Generics"]:::sub
    P4_SPRING -.- S14["IoC/DI, @Transactional<br/>JUnit 5 & Mockito"]:::sub
    P4_KAFKA -.- S15["Topics, Partitions, Consumer Groups<br/>Resilience4j (Circuit Breaker)"]:::sub

    P5_DATA -.- S16["Álgebra Linear, Estatística<br/>DataFrames & Vetorização"]:::sub
    P5_ML -.- S17["Scikit-learn, XGBoost (Fraude)<br/>PyTorch, OpenCV & YOLO"]:::sub
    P5_MLOPS -.- S18["ONNX Runtime, MLflow, DVC<br/>Inferência via FastAPI"]:::sub
```