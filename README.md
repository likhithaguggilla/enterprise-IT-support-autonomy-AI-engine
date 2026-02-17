
 # IT Support Agentic RAG Engine

This is an intelligent orchestration system designed to automate Level 1 (L1) IT support. This **agentic RAG (Retrieval-Augmented Generation)** system autonomously resolves high-volume, low-complexity requests such as **policy inquiries and technical troubleshooting** while intelligently **triaging complex issues to human agents with full context**.

By moving beyond traditional keyword-matching chatbots, this engine utilizes semantic reasoning to disambiguate vague user inputs and extract actionable instructions from dense corporate documentation.

---

## Key Features

* **Semantic RAG Pipeline:** Processes complex, multi-page PDFs (handbooks, security policies) into vectorized "knowledge flashcards" for precise information retrieval.


* **Agentic Routing:** A "brain" powered by Llama 3.3 that decides whether to answer a question directly, search the knowledge base, or trigger a technical workflow.


* **Human-in-the-Loop (HITL) Safety:** High-stakes actions, such as ticket creation or password resets, require an asynchronous confirmation signal from a human supervisor before execution.


* **Automated QA & Evaluation:** An "LLM-as-a-Judge" framework that mathematically scores agent responses against ground-truth data to ensure accuracy and minimize hallucinations.


---

## System Architecture

![Architecture Diagram](https://github.com/likhithaguggilla/enterprise-IT-support-autonomy-AI-engine/blob/main/assets/system-architecture.png)


---

### Tech Stack

* **Orchestration:** n8n (Self-hosted) 


* **LLMs:** Llama 3.3-70b (Reasoning) & Llama 3-8b (Speed) via Groq 


* **Vector Database:** Pinecone (Serverless) 


* **Embeddings:** Hugging Face (`all-MiniLM-L6-v2`) 


* **Integrations:** Google Drive (Ingestion), Google Sheets (Database), and Gmail (Approvals)


---

## System Boundaries & Behavior

To ensure enterprise-grade reliability, the agent operates under strict constraints:

* **Scope:** Limited exclusively to IT support and general company policy; it refuses queries regarding salaries or personal legal advice.


* **"I Don't Know" Protocol:** If retrieval confidence falls below 75%, the agent automatically offers to escalate to a human expert rather than risking a hallucination.


* **Recency Weighting:** The RAG pipeline prioritizes the most recent documentation (e.g., 2025 policies over 2023) to prevent outdated responses.



---

## Engineering Challenges & Solutions

* **Asynchronous UX:** Solved "hanging" chat interfaces by decoupling ticket requests from execution, allowing the agent to confirm the request immediately while a background worker handles approvals.


* **Deterministic Output:** Prevented the LLM from "inventing" fake ticket IDs by using an "Edit Fields" node to force strict string returns for specific actions.


* **Complex Data Handling:** Addressed table-reading hallucinations by identifying the need for future "Code Interpreter" tools or CSV pre-processing for heavy tabular data.



---

## Getting Started

### Prerequisites

* **Docker:** To host the n8n environment.


* **API Keys:** Groq (Inference), Pinecone (Vector Store), and Hugging Face (Embeddings).


* **Google Cloud Console:** Configured with Client IDs for Drive and Sheets access.



### Deployment

1. **Environment Setup:** Start n8n using Docker.
2. **Knowledge Ingestion:** Run the **Phase 1 ETL Pipeline** to download and vectorize your policy documentation into Pinecone.
3. **Agent Activation:** Deploy the **Phase 2 Inference Layer** to enable chat-based retrieval.
4. **Action Layer Configuration:** Connect your Gmail and Google Sheets to the **Phase 3 Tool Workflows** for ticket logging.



---




