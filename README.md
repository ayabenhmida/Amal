# DeepSeek Architecture

## Team 3IDL03
- **Eya Ben Hmida**
- **Eya Belkadhie**
- **Rihab Ben Amor Souissi**

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
 
*Last Updated: October 2025*
