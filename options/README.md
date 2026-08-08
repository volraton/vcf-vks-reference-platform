# Options Catalog

This catalog breaks the platform into reusable blocks. Harbor comes first because it is the registry foundation for most workloads.

![Options Block Diagram](architecture-options.svg)

## Platform dependency flow

```text
Developer
  |
  v
GitHub
  |
  v
GitHub Actions / CI
  |
  v
Harbor Registry
  |
  v
Argo CD App-of-Apps
  |
  v
VKS Cluster
```

## Core options

| Option | Purpose | Status |
|---|---|---|
| Harbor | Container registry foundation | Core |
| Secret Store | Centralized secret management | Core |
| DSM | Managed PostgreSQL / data services | Core |
| Argo CD | GitOps delivery | Core |
| Foundation LB | Standard load-balancing exposure | Core |

## Optional options

| Option | Purpose | Status |
|---|---|---|
| Pinniped | Identity / OIDC | Optional |
| AVI / NSX ALB | Advanced load balancing | Optional |
| Gateway API | Modern traffic policy | Optional |
| cert-manager | TLS automation | Optional |
| Velero | Backup / restore | Optional |
| Monitoring | Metrics / dashboards | Optional |
| AI Platform | vLLM / Ollama / Open WebUI | Optional |

## Secret flow with Harbor

Harbor is not just a place to store images. Its robot accounts and registry credentials should also come from the platform secret layer.

```text
VCF Secret Store
   |
   +--> Harbor Robot Account
   +--> Harbor Registry Credentials
   +--> DSM Database Credentials
   +--> GitOps Credentials
   +--> Application API Keys
   +--> AI Provider Keys
```

Recommended flow:

```text
Harbor
  |
  v
Robot Account / Registry Credential
  |
  v
VCF Secret Store
  |
  v
External Secrets / Kubernetes Secret
  |
  v
ImagePullSecret / Workload Auth
```

## Recommended order

1. Harbor
2. Secret Store
3. VKS
4. DSM
5. Argo CD
6. Foundation LB
7. Pinniped
8. AVI / NSX ALB
9. Gateway API
10. cert-manager
11. Velero
12. Monitoring
13. AI Platform

## Use this catalog

Start with the core blocks, then layer optional services only when the workshop or customer demo needs them.
