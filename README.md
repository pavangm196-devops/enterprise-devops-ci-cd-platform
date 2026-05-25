# Enterprise DevOps CI/CD Platform

> An enterprise-grade observability and CI/CD platform built on top of the OpenTelemetry Demo — extended with custom Kubernetes deployment configs, multi-service Docker Compose setups, and a production-ready CI/CD pipeline. Demonstrates distributed tracing, metrics, and logs across a 20+ service polyglot microservices system.

---

> **Note:** This project is adapted from the [OpenTelemetry Demo](https://github.com/open-telemetry/opentelemetry-demo) (Apache 2.0 License). I forked and configured this project to study and demonstrate enterprise-level observability practices, Kubernetes deployment patterns, and CI/CD pipeline implementation on a real-world distributed system.

---

## Tech Stack

![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-Observability-blueviolet?logo=opentelemetry)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Deployment-blue?logo=kubernetes)
![Docker](https://img.shields.io/badge/Docker-Compose-blue?logo=docker)
![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-black?logo=github-actions)
![TypeScript](https://img.shields.io/badge/Language-TypeScript-3178C6?logo=typescript)
![Python](https://img.shields.io/badge/Language-Python-3776AB?logo=python)
![Go](https://img.shields.io/badge/Language-Go-00ADD8?logo=go)
![Grafana](https://img.shields.io/badge/Dashboards-Grafana-F46800?logo=grafana)
![Prometheus](https://img.shields.io/badge/Metrics-Prometheus-E6522C?logo=prometheus)
![Jaeger](https://img.shields.io/badge/Tracing-Jaeger-66CFE3)

---

## What Problem This Solves

In enterprise environments, debugging distributed systems without proper observability is extremely difficult — a single request touches 10+ services and failures are hard to trace. This platform demonstrates how OpenTelemetry can instrument a full polyglot microservices system (TypeScript, Python, Go, Java, C#) to provide unified distributed tracing, metrics, and logs — all deployable on Kubernetes with a working CI/CD pipeline.

---

## Architecture

```
┌──────────────────────────────────────────────────────────────┐
│              OpenTelemetry Instrumented Services              │
│                                                              │
│  TypeScript  │  Python  │  Go  │  Java  │  C#  │  Erlang    │
│                                                              │
│  Each service emits:                                         │
│  - Traces  → OpenTelemetry Collector → Jaeger               │
│  - Metrics → OpenTelemetry Collector → Prometheus → Grafana  │
│  - Logs    → OpenTelemetry Collector → Loki                  │
└──────────────────────────────────────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────────────────────────────┐
│               Kubernetes Deployment (k8s/)                    │
│                                                              │
│  Deployments + Services + ConfigMaps for each microservice   │
│  Ingress → Frontend                                          │
└──────────────────────────────────────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────────────────────────────┐
│               CI/CD Pipeline (GitHub Actions)                 │
│                                                              │
│  Push → Build Docker images → Run integration tests          │
│       → Push to registry → Deploy to Kubernetes              │
└──────────────────────────────────────────────────────────────┘
```

---

## Key Features / What I Configured

- **Full OpenTelemetry instrumentation** across 20+ microservices in TypeScript, Python, Go, Java, C#, and Erlang
- **Kubernetes deployment manifests** in `/kubernetes` directory for all services — Deployments, Services, ConfigMaps, and ingress rules
- **Multi-environment Docker Compose** — `docker-compose.yml` (full stack), `docker-compose.minimal.yml` (lean local dev), `docker-compose-tests.yml` (integration test suite)
- **GitHub Actions CI/CD pipeline** in `.github/workflows/` — builds, tests, and deploys on every push
- **Makefile** with developer-friendly targets for build, run, test, and clean
- **Integration test suite** in `/test` — verifies end-to-end service behaviour
- **Distributed tracing** — trace a single user request across all services with Jaeger
- **Metrics dashboards** — Prometheus + Grafana for real-time service health
- **Renovate bot config** (`renovate.json5`) — automated dependency updates
- **Internal tools** in `/internal/tools` — custom utilities for the platform

---

## Folder Structure

```
enterprise-devops-ci-cd-platform/
├── .github/
│   └── workflows/               # GitHub Actions CI/CD pipeline
├── src/                         # Application source code (polyglot services)
├── kubernetes/                  # K8s deployment manifests
│   ├── opentelemetry-demo.yaml
│   └── ...
├── internal/
│   └── tools/                   # Internal utility scripts
├── pb/                          # Protocol Buffer definitions
├── test/                        # Integration test suite
├── docker-compose.yml           # Full stack local dev
├── docker-compose.minimal.yml   # Minimal local dev
├── docker-compose-tests.yml     # Integration test compose
├── Makefile                     # Developer task runner
├── renovate.json5               # Automated dependency updates
├── CHANGELOG.md                 # Release history
├── CONTRIBUTING.md              # Contribution guide
└── README.md
```

---

## How to Run

### Prerequisites

- Docker & Docker Compose
- Kubernetes cluster (for K8s deployment)
- 6GB+ RAM recommended for full stack

### Quick Start — Docker Compose (Full Stack)

```bash
# Clone the repo
git clone https://github.com/pavangm196-devops/enterprise-devops-ci-cd-platform.git
cd enterprise-devops-ci-cd-platform

# Start full stack
docker-compose up --build

# Or minimal version (faster startup)
docker-compose -f docker-compose.minimal.yml up --build
```

Access the platform:
- Frontend → http://localhost:8080
- Grafana Dashboards → http://localhost:3000
- Jaeger Tracing UI → http://localhost:16686
- Prometheus → http://localhost:9090

### Run Integration Tests

```bash
docker-compose -f docker-compose-tests.yml up --build
```

### Deploy to Kubernetes

```bash
# Apply all Kubernetes manifests
kubectl apply -f kubernetes/

# Check all pods are running
kubectl get pods -n otel-demo
```

### Using the Makefile

```bash
make build      # Build all Docker images
make run        # Start the full stack
make test       # Run integration tests
make clean      # Stop and remove containers
```

---

## What This Demonstrates

| Skill | How it's shown |
|---|---|
| Observability | OpenTelemetry distributed tracing, metrics, logs across 20+ services |
| Kubernetes | Full deployment manifests for polyglot microservices |
| CI/CD | GitHub Actions pipeline — build, test, deploy |
| Docker | Multi-service compose, minimal dev, test environments |
| Monitoring | Prometheus + Grafana dashboards, Jaeger trace visualization |
| Languages | TypeScript, Python, Go, Java, C#, Erlang — multi-language instrumentation |
| DevOps Tooling | Makefile, Renovate, Protocol Buffers, integration test suite |

---

## Original Project Credit

This repo is adapted from [opentelemetry/opentelemetry-demo](https://github.com/open-telemetry/opentelemetry-demo), licensed under Apache 2.0. Full credit to the OpenTelemetry contributors. My contributions: Kubernetes deployment customization, CI/CD pipeline setup, and observability configuration study.

---

## Author

**Pavan G M** — DevOps Engineer | AWS Certified Solutions Architect (SAA-C03) | CKA Certified

[![GitHub](https://img.shields.io/badge/GitHub-pavangm196--devops-black?logo=github)](https://github.com/pavangm196-devops)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-pavan--gm96-blue?logo=linkedin)](https://linkedin.com/in/pavan-gm96)
