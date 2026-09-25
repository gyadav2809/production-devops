# production-devops


                         USER
                           │
                           ▼
                      INTERNET
                           │
                           ▼
                         DNS
                       Route53
                           │
                           ▼
                    ┌──────────────┐
                    │     WAF      │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │ Load Balancer│
                    └──────┬───────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Ingress / Nginx     │
                └──────────┬──────────┘
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
          Frontend       API          API Worker
                           │
             ┌─────────────┼──────────────┐
             ▼             ▼              ▼
          PostgreSQL     Redis           Kafka
             │                            │
             ▼                            ▼
            EBS                         Workers
             │
             ▼
            S3


       ┌──────────────── OBSERVABILITY ────────────────┐
       │                                               │
       │  Prometheus → Grafana                         │
       │       │                                       │
       │       └→ Alertmanager                         │
       │                                               │
       │  Loki → Grafana                               │
       │                                               │
       │  OpenTelemetry → Tracing                      │
       └───────────────────────────────────────────────┘


       ┌──────────────── DELIVERY ─────────────────────┐
       │                                               │
       │ GitHub → GitHub Actions → Registry            │
       │                         ↓                     │
       │                    Deployment                 │
       │                                               │
       │ Terraform → AWS infrastructure               │
       │ Helm → Kubernetes                             │
       └───────────────────────────────────────────────┘
