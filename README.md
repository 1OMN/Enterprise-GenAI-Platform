# Enterprise GenAI Platform
**A Production-Grade RAG & Agentic System for Secure Environments**

![Status](https://img.shields.io/badge/Status-Active_Development-brightgreen) ![Stack](https://img.shields.io/badge/Tech-vLLM_%7C_LangGraph_%7C_RHEL-blue)

## 1. Executive Summary
This platform demonstrates a reference architecture for deploying **Autonomous AI Agents** and **RAG pipelines** in highly regulated enterprise environments (e.g., Telco, Banking). Unlike standard SaaS wrappers, this solution focuses on **Data Sovereignty** (On-Premise/Private Cloud), **Cost Control** (Local Inference), and **Safety** (Guardrails).

## 2. Architecture Overview
The system is designed as a modular microservices architecture:
* **Inference Layer:** High-throughput serving using `vLLM` on Linux/GPU nodes.
* **Orchestration Layer:** Agentic workflows managed by `LangGraph`.
* **Knowledge Layer:** Vector search using `Qdrant` (Self-hosted).
* **Guardrails:** Input/Output filtering using `NeMo Guardrails` / `Langfuse`.

### High-Level Diagram
```mermaid
graph TD
    User[Enterprise User] -->|HTTPS| Gateway[API Gateway / NGINX]
    Gateway -->|Auth| Guard[Security Guardrails]
    Guard --> Router{Semantic Router}
    Router -->|Complex| GPT4[GPT-4o External]
    Router -->|Sensitive/Routine| LocalLLM[Local Inference (vLLM)]
    LocalLLM -->|Context| VectorDB[(Qdrant Vector DB)]
