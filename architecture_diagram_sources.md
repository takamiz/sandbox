# Draw.io で作成する多面的アーキテクチャ図（ソース）

Draw.io の 「配置」 -> 「挿入」 -> 「高度」 -> 「Mermaid...」 に以下のコードを貼り付けることで、高度なアーキテクチャ図を作成できます。

## 1. 全体スタック図 (Rust + PostgreSQL + Leptos)
```mermaid
graph TD
    Client["User Browser (WASM)"] <--> Frontend["Leptos Frontend (WASM)"]
    Frontend <--> API["Rust API (Axum/Actix-web)"]
    
    subgraph Shared["Shared Crate"]
        DTO["DTO & Type Definitions"]
    end
    
    API <--> DTO
    Frontend <--> DTO
    
    subgraph Backend["Backend & DB"]
        API <--> SQLx["SQLx / PgPool"]
        SQLx <--> DB[(PostgreSQL + pgvector)]
    end
    
    style Client fill:#f9f,stroke:#333,stroke-width:2px
    style DB fill:#00d,color:#fff,stroke:#333,stroke-width:2px
```

## 2. 高度なRAGパイプライン図
```mermaid
flowchart LR
    Docs[Data Sources] --> Parse[Markdown Parser]
    Parse --> Chunk[Small2Big Chunking]
    Chunk --> Embed[Embedding]
    Embed --> DB[(Vector DB)]
    
    Query[User Query] --> Transform[Query Transformation]
    Transform --> Search{Hybrid Search}
    DB <--> Search
    Search --> Rerank[Cross-Encoder Reranker]
    Rerank --> Context[Context Assembly]
    Context --> LLM[LLM / Rig Agent]
    LLM --> Verify{Self-Reflection}
    Verify -- Failed --> Transform
    Verify -- Success --> Answer[Final Answer]
```

## 3. 自己向上ループ (Self-Improving Loop)
```mermaid
sequenceDiagram
    participant U as User
    participant A as RAG Agent
    participant E as Evaluator (RAGAS)
    participant DB as Feedback DB
    participant O as Optimizer
    
    U->>A: Query
    A->>U: Answer + Self-Score
    A->>DB: Log Score & Trace
    
    loop Weekly Tuning
        E->>DB: Analyze Failed Queries
        E->>O: Identify Weaknesses
        O->>A: Update Chunks / Prompt
    end
```
