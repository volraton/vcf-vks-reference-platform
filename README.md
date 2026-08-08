# VCF VKS Reference Platform

A VMware Cloud Foundation 9 reference platform for building repeatable labs, demos, and production-style blueprints around VKS, Harbor, Secret Store, DSM, GitOps, identity, networking, and optional platform services.

## Why this repository exists

This repo is intended to start with **Harbor first**, because Harbor is the common foundation for most platform services and workloads.

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

## Platform layers

```text
                         VMware Cloud Foundation 9
┌─────────────────────────────────────────────────────────────────────┐
│                         vSphere Supervisor                          │
│                                                                     │
│  Secret Store     Foundation LB      DSM       VKS                  │
│     │                  │              │          │                   │
└─────┼──────────────────┼──────────────┼──────────┘                   │
      │                  │              │                              │
      ▼                  ▼              ▼                              │
                    Platform Services                                 │
┌─────────────────────────────────────────────────────────────────────┐
│ Harbor Registry                                                      │
│      │                                                               │
│      ▼                                                               │
│ Argo CD (AppProject / App-of-Apps)                                   │
│      │                                                               │
│      ├── Workloads                                                   │
│      ├── AI Platform                                                 │
│      ├── Monitoring                                                  │
│      └── Future Services                                             │
│                                                                     │
│ Optional                                                            │
│   ├── Pinniped                                                     │
│   ├── AVI / NSX ALB                                                │
│   ├── cert-manager                                                 │
│   ├── Velero                                                       │
│   └── Gateway API                                                  │
└─────────────────────────────────────────────────────────────────────┘
```

## Option catalog

The repository is organized as a catalog of options. Each option can be used independently or combined with the others.

| Option | Purpose | Priority |
|---|---|---|
| Harbor | Container registry foundation | Core |
| Secret Store | Centralized secret management | Core |
| Foundation LB | Standard application exposure | Core |
| DSM | Managed database services | Core |
| Argo CD | GitOps delivery | Core |
| Pinniped | Identity / OIDC | Optional |
| AVI / NSX ALB | Advanced load balancing | Optional |
| Gateway API | Modern traffic policy | Optional |
| cert-manager | TLS automation | Optional |
| Velero | Backup / restore | Optional |
| Monitoring | Metrics / dashboards | Optional |
| AI Platform | vLLM / Ollama / Open WebUI | Optional |

## Recommended order

1. Harbor
2. VKS
3. Secret Store
4. DSM
5. Argo CD App-of-Apps
6. Foundation LB
7. Pinniped
8. AVI / NSX ALB
9. Gateway API
10. cert-manager
11. Velero
12. Monitoring
13. AI Platform

## Current focus

The first implementation target should be:

- Harbor as the base registry
- VKS as the runtime platform
- Secret Store as the security foundation
- DSM as the managed data service
- Argo CD as the deployment engine

This gives a clean base that everything else can build on.

## Repository layout

```text
vcf-vks-reference-platform/
├── README.md
├── core/
├── options/
├── labs/
├── examples/
├── docs/
└── scripts/
```

## Next build targets

- `options/harbor/`
- `options/secret-store/`
- `options/dsm/`
- `options/argocd/`
- `options/foundation-lb/`
- `options/avi-lb/`
- `options/pinniped/`

The goal is to make each option a self-contained block that can be turned on when needed, without forcing the rest of the platform to change.
