# DeepSeek Architecture

## Team
- **Eya Ben Hmida**
- **Eya Belkadhie**
- **Rihab Ben Amor Souissi**

## Description
DeepSeek is a modular and scalable platform combining a **microservices architecture** with an **intelligent gateway** for managing and orchestrating AI models. The project consists of two main components:

1. **DeepSeek Gateway**: Handles authentication, data validation, enrichment, and routing requests to backend services.
2. **DeepSeek Microservices**: Provides AI services, orchestration, ingestion, notification, and data storage for parallel processing and scalability.

---

## 1. Gateway Architecture

This architecture manages clients and orchestrates downstream services via an **API Gateway** and authentication services.

### Key Components
- **Clients / Frontend / API Consumers**
- **API Gateway**: Authentication, rate-limiting
- **Auth Service**: OAuth2 / Keycloak
- **Ingestion Service**: Data validation and enrichment
- **Message Broker**: Kafka / RabbitMQ for parallel processing
- **Workers Cluster**: Pre-processing, ML inference, enrichment
- **Orchestrator / Workflow**: Temporal / Argo
- **Storages**: PostgreSQL, MongoDB, S3 / MinIO
- **Notification Service**: Email, webhook, SMS
- **Observability**: Prometheus, Grafana, Jaeger
- **CI/CD & Infrastructure**: Kubernetes, GitHub Actions / GitLab CI

> This architecture is optimized for scalability and parallel processing of AI requests.

---

## 2. Microservices Architecture

This architecture represents the full set of DeepSeek services and layers, including AI orchestration and backend services.

### Client Layer
- Web Client
- Mobile Client
- Backend Service
- OpenAI SDK

### Edge & Gateway Layer
- AI Gateway (Cloudflare)
- API Gateway (APISIX)

### AI Orchestration Layer
- Model Router
- Safety Layer
- Policy Engine
- Prompt Filters

### Data & Metadata Layer
- Feature Flags
- KMS / Vault
- Logs / Metrics
- Cache Layer
- RAG Store

### AI Backend Layer
- DeepSeek API
- OpenAI Fallback
- Anthropic Fallback

### Infrastructure Layer
- Kubernetes HPA
- Observability (OTel)
- CI/CD with Canary Deployments


---
