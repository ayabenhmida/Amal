# DeepSeek Architecture

## Team 3IDL03
- **Eya Ben Hmida**
- **Eya Belkadhie**
- **Rihab Ben Amor Souissi**

# **DeepSeek Gateway Architecture**

This architecture represents a **layered, policy-driven AI gateway system** that coordinates communication between client applications and multiple AI model providers (DeepSeek, OpenAI, Anthropic).  
Its goal is to **orchestrate, secure, and optimize** AI requests using routing intelligence, safety filters, and infrastructure automation.

---

##  **Architecture Description**

###  **Client Layer**
This layer includes **Web**, **Mobile**, and **Backend** clients, as well as SDK integrations.  
Clients communicate with the gateway via secure HTTPS endpoints.  
It ensures a consistent entry point for different application types and environments.

###  **Edge & Gateway Layer**
The **AI Gateway (Cloudflare)** handles global routing, CDN caching, and rate limiting.  
The **API Gateway (APISIX)** manages authentication, request routing, caching, and logging.  
Together, they form a **dual-layer edge**, separating external traffic handling (Cloudflare) from internal microservice orchestration (APISIX).  
This improves scalability and isolates network-level and application-level responsibilities.

###  **AI Orchestration Layer**
This is the core logic of the system:
- **Model Router:** selects the right AI model provider based on workload, latency, or policies.  
- **Safety Layer:** filters unsafe or biased prompts and model responses.  
- **Policy Engine:** applies access control, quotas, and compliance rules.  
- **Prompt Filters:** perform content sanitization and prompt optimization.  

The orchestration layer ensures **controlled, secure, and adaptive routing** of requests before reaching any backend AI model.

###  **Data & Metadata Layer**
This layer supports configuration and performance optimization:
- **Feature Flags** for activating or testing components dynamically.  
- **Vault/KMS** for managing API secrets and encryption keys.  
- **Logs & Metrics** for monitoring usage, performance, and anomalies.  
- **Cache Layer** for fast response retrieval.  
- **RAG Store** for retrieval-augmented generation using vector data or embeddings.  

It provides both **security (KMS, Vault)** and **speed (cache, RAG)** to the system.

###  **AI Backends Layer**
This layer connects to multiple AI models:
- **DeepSeek API** as the main engine.  
- **OpenAI** and **Anthropic** as fallback providers.  

The router and policy engine decide when to switch providers, ensuring **resilience and continuity** if one API fails or becomes overloaded.

###  **Infrastructure Layer**
Composed of:
- **Kubernetes (HPA):** handles auto-scaling.  
- **OpenTelemetry:** provides full observability (traces, logs, metrics).  
- **CI/CD with Canary Deployments:** allows progressive, safe rollouts.  

This foundation guarantees **reliability, monitoring, and continuous delivery**.

---
##  **Resources**

-  **Source Code:** [View on GitHub](https://github.com/EyaGIT/Amal_2/blob/main/Gateway_Deepseek.tex)  
-  **Architecture Diagram (PDF):** [Download PDF](https://github.com/EyaGIT/Amal_2/blob/main/Gateway_Deepseek.pdf)

---

# **Parallel Microservices Architecture Summary**

This system is a **parallel, event-driven microservices pipeline**.  
Requests enter through an **API Gateway** *(Auth, rate-limit, circuit-break, retry, logging)*.  
A **service mesh** secures and routes traffic to **core services** *(Ingestion, Validation, Enrichment, Transform)*.  
Services publish domain events to **Kafka/Pulsar**.  
**Worker pools** *(Preprocess, GPU Inference, Post-Process, Batch)* consume in **parallel** using consumer groups and scale **horizontally** based on queue depth.  
Results are persisted to **PostgreSQL**, **MongoDB**, **Redis**, **Search**, and **S3**.  
A **Query Service** and a **BFF** expose optimized read APIs.  
**Prometheus/Grafana/Jaeger/ELK** provide observability.  
**Kubernetes/Helm/ArgoCD** manage deployment and scaling.

---

##  **When to Use**

- High-throughput pipelines  
- ML inference workloads  
- Spiky traffic or bursty workloads  
- Multi-team ownership with clear service boundaries  
- Systems requiring strong resilience and auto-scaling  

---

## **When Not to Use**

- Small or simple CRUD applications  
- Ultra-low-latency synchronous flows  
- Systems needing strict cross-service ACID transactions  

---

## **Pros**

- Elastic horizontal scaling  
- High resilience through asynchronous queues  
- High throughput from parallelism  
- Clear service ownership and boundaries  

---

##  **Cons**

- High operational complexity and cost  
- Eventual consistency across services  
- Schema/version management required  
- More complex debugging and tracing  

---

##  **Recommended Practices**

- Keep **CORS**, **compression**, and **validation** at the **Gateway**;  
  use the **Service Mesh** for **mTLS** and **traffic policies**.  
- Prefer **one orchestrator** *(Temporal or Airflow)* — avoid overlapping Celery unless required.  
- Use **Schema Registry**, **Dead-Letter Queues (DLQs)**, and **idempotency keys** for safe retries.  
- Centralize database writes through dedicated **Writer/Indexer services**, not directly from workers.  
- Scale consumer groups via **Horizontal Pod Autoscaler (HPA)** on **Kafka topic lag**;  
  use **partition keys** for ordered per-entity processing.  

---

## **Resources**

- **Source Code:** [📂 View on GitHub](https://github.com/EyaGIT/Amal_2/blob/main/Microservice_parallele.tex)  
- **Architecture Diagram (PDF):** [Download PDF](https://github.com/EyaGIT/Amal_2/blob/main/Microservice_parallele.pdf)

---
 
*Last Updated: October 2025*
