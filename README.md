# 🏥 Clinical AI Platform: End-to-End Health Data & LLM Ecosystem

This repository demonstrates a production-grade Clinical AI architecture, built specifically to align with UK NHS data standards and global pharmaceutical compliance (OMOP CDM, GDPR, Algorithmic Fairness). 

The project is divided into three interconnected phases: **Clinical Data Engineering**, **MLOps & Governance**, and **Medical LLM Engineering**.

## 🏗️ System Architecture

```mermaid
graph TD
    %% Styling
    classDef data fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef mlops fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px;
    classDef llm fill:#fff3e0,stroke:#e65100,stroke-width:2px;

    subgraph Phase 1: Clinical Data Engineering
        A[Raw Synthetic EHR Data<br/>JSON/CSV]:::data -->|Airflow Orchestration| B(Google Cloud Storage<br/>Data Lake):::data
        B --> C(BigQuery<br/>Raw Tables):::data
        C -->|dbt Models| D[(OMOP CDM<br/>Clinical Data Warehouse)]:::data
    end

    subgraph Phase 2: MLOps & Governance
        D -->|Feature Engineering| E[MLflow<br/>Experiment Tracking]:::mlops
        E -->|Register Best Model| F[FastAPI + Docker<br/>Inference API]:::mlops
        F -->|Drift & Bias Checks| G[Evidently AI & Fairlearn<br/>Compliance Dashboards]:::mlops
    end

    subgraph Phase 3: Medical LLM Co-Pilot
        H[UK NICE Guidelines<br/>Medical Literature]:::llm -->|LangChain Embeddings| I[(Vector Database<br/>Chroma / Elastic)]:::llm
        I -->|Semantic Search| J{Local LLM via Ollama<br/>BioMistral / Llama 3}:::llm
        F -.->|Patient Risk Scores| J
        J -->|NVIDIA NeMo Guardrails| K[Streamlit UI<br/>Clinical Co-Pilot]:::llm
    end
