<div align="center">

# 🚀 GitOps Blogging Application
### *DevSecOps-Enabled Full-Stack CI/CD Pipeline*

[![CI](https://img.shields.io/badge/CI-GitHub%20Actions-blue?logo=githubactions&logoColor=white)](.)
[![Docker](https://img.shields.io/badge/Containerized-Docker-2496ED?logo=docker&logoColor=white)](.)
[![Kubernetes](https://img.shields.io/badge/Orchestration-Kubernetes-326CE5?logo=kubernetes&logoColor=white)](.)
[![ArgoCD](https://img.shields.io/badge/GitOps-ArgoCD-EF7B4D?logo=argo&logoColor=white)](.)
[![Monitoring](https://img.shields.io/badge/Monitoring-Prometheus%20%7C%20Grafana-E6522C?logo=prometheus&logoColor=white)](.)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**A production-grade blogging platform, deployed end-to-end via GitOps — from `git push` to a running pod on Amazon EKS, with security gates at every stage.**

</div>

---

## 📌 Overview

This project is a full-stack blogging application demonstrating a **complete GitOps + DevSecOps pipeline** — not just a CRUD app, but the entire delivery system around it.

Code is scanned for secrets and vulnerabilities before it's ever built, images are hardened and scanned before they're pushed, and deployments are driven declaratively by Argo CD watching Git — not by anyone running `kubectl apply` by hand.

> Built to demonstrate real-world DevSecOps practices for **DevOps portfolios, interviews, and production-ready architecture demos.**

---

## ✨ Key Features

| | |
|---|---|
| 📝 | Full CRUD blog post management |
| 🔐 | Multi-stage DevSecOps security pipeline |
| ⚡ | Fully automated GitOps deployment (zero manual `kubectl`) |
| 🐳 | Containerized frontend & backend |
| ☸️ | Kubernetes orchestration on Amazon EKS |
| 🔍 | Integrated secret, dependency, Dockerfile & image scanning |
| 📊 | Real-time monitoring via Prometheus & Grafana |
| 🔄 | Continuous sync & self-healing deployment via Argo CD |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | React.js |
| **Backend** | Node.js (Express) |
| **Containerization** | Docker |
| **Orchestration** | Kubernetes (Amazon EKS) |
| **CI** | GitHub Actions |
| **GitOps / CD** | Argo CD |
| **Monitoring** | Prometheus, Grafana |
| **Security Scanning** | Gitleaks, OWASP Dependency-Check, Hadolint, Trivy |

---

## 🏗️ Architecture

```
Developer → GitHub → GitHub Actions (Security + Build) → DockerHub
                                                              │
                                                              ▼
                                          k8s manifests updated (image tag)
                                                              │
                                                              ▼
                                          Argo CD detects change in Git
                                                              │
                                                              ▼
                                        Auto-sync → Deploy → Amazon EKS
                                                              │
                                                              ▼
                                        Prometheus + Grafana (Observability)
```

### System Design Notes

- **GitOps as source of truth** — the live cluster state always mirrors what's committed in `k8s/`. No one deploys by running `kubectl apply` manually; Argo CD is the only thing that touches the cluster.
- **Immutable image tags** — every build produces a uniquely tagged image (commit SHA), so rollbacks are just a Git revert away, not a rebuild.
- **Shift-left security** — vulnerabilities and secrets are caught in CI, before an image is ever pushed, not after deployment.
- **Self-healing deployments** — if someone manually edits a resource on the cluster (config drift), Argo CD detects and reverts it back to match Git.

---

## ⚙️ Prerequisites

Before running this project locally or deploying it, make sure you have:

| Tool | Purpose | Version |
|---|---|---|
| Node.js | Frontend & backend runtime | ≥ 18.x |
| Docker | Building & running containers | ≥ 24.x |
| kubectl | Interacting with the EKS cluster | ≥ 1.28 |
| Argo CD CLI | Managing GitOps sync | ≥ 2.9 |
| AWS CLI | EKS cluster access | ≥ 2.x |
| Helm | Installing Prometheus/Grafana stack | ≥ 3.x |
| eksctl (optional) | Provisioning EKS cluster | latest |

---

## 💻 Local Development Setup

Run the app locally without Kubernetes, using Docker Compose:

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/gitops-blogging-app.git
cd gitops-blogging-app

# 2. Set up environment variables (see below)
cp .env.example .env

# 3. Start frontend + backend with Docker Compose
docker-compose up --build

# App will be available at:
# Frontend → http://localhost:3000
# Backend  → http://localhost:5000
```

Or run each service independently:

```bash
# Backend
cd backend
npm install
npm run dev

# Frontend (in a new terminal)
cd frontend
npm install
npm start
```

---

## 🔑 Environment Variables

| Variable | Description | Example |
|---|---|---|
| `PORT` | Backend server port | `5000` |
| `MONGO_URI` / `DB_URI` | Database connection string | `mongodb://localhost:27017/blogdb` |
| `JWT_SECRET` | Secret for signing auth tokens | `your-secret-key` |
| `REACT_APP_API_URL` | Backend API base URL for frontend | `http://localhost:5000/api` |
| `NODE_ENV` | Environment mode | `development` / `production` |

> ⚠️ Never commit `.env` files — they're excluded via `.gitignore` and scanned for by **Gitleaks** in CI.

---

## 📡 API Reference (Backend)

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/posts` | Fetch all blog posts |
| `GET` | `/api/posts/:id` | Fetch a single post by ID |
| `POST` | `/api/posts` | Create a new post |
| `PUT` | `/api/posts/:id` | Update an existing post |
| `DELETE` | `/api/posts/:id` | Delete a post |
| `GET` | `/health` | Health check endpoint (used by K8s probes) |

---

## 🔄 CI/CD + DevSecOps Pipeline

**Step-by-step flow:**

1. 👨‍💻 **Developer pushes code** to GitHub
2. ⚙️ **GitHub Actions pipeline triggers** automatically
3. 🔐 **Security & Quality Gates**
   - 🔍 **Gitleaks** — detects secrets/credentials in code
   - 🛡️ **OWASP Dependency-Check** — flags vulnerable dependencies
   - 🐳 **Hadolint** — lints the Dockerfile for best practices
4. 🏗️ **Build & Scan**
   - Docker image built
   - 🔎 **Trivy** scans the image for CVEs
5. 🚀 **Deployment Prep**
   - Image pushed to DockerHub
   - Kubernetes manifests updated with the new image tag
6. 🔁 **GitOps Deployment**
   - Argo CD continuously watches the GitHub repo
   - Detects manifest changes
   - Auto-syncs and deploys to EKS

> ✅ Argo CD is fully configured and actively reconciling this application on the Amazon EKS cluster — Git is the single source of truth.

---

## 📁 Folder Structure

```
project-root/
│
├── frontend/                 # React app
├── backend/                  # Node.js API
├── k8s/                      # Kubernetes manifests
├── .github/workflows/        # CI/CD pipeline definitions
├── Dockerfile
├── docker-compose.yml
└── README.md
```

---

## 🔐 Security in Depth

Every stage of the pipeline has a dedicated gate — nothing skips a check:

| Stage | Tool | What it catches |
|---|---|---|
| **Pre-build** | Gitleaks | Hardcoded secrets, API keys, tokens in code/commits |
| **Pre-build** | OWASP Dependency-Check | Known CVEs in project dependencies |
| **Pre-build** | Hadolint | Dockerfile anti-patterns & best-practice violations |
| **Post-build** | Trivy | OS package & application-layer vulnerabilities in the final image |
| **Runtime** | Kubernetes NetworkPolicies / RBAC (recommended) | Lateral movement & over-permissioned access |

If any stage fails its threshold, the pipeline halts **before** an image is pushed to DockerHub — vulnerable or leaky builds never reach the cluster.

---

## ☸️ Deployment Process (EKS + Argo CD)

1. Build and push the Docker image (tagged with commit SHA)
2. Update Kubernetes manifests in `k8s/` with the new image tag
3. Push changes to GitHub
4. Argo CD detects the change via its Git polling/webhook
5. Argo CD auto-syncs and deploys to the EKS cluster
6. Health probes confirm the rollout before old pods are terminated

📌 Argo CD ensures continuous synchronization between GitHub and the cluster — any drift is automatically corrected.

### Manual Argo CD Sync (if needed)

```bash
argocd app get gitops-blogging-app
argocd app sync gitops-blogging-app
argocd app history gitops-blogging-app   # view rollout history
argocd app rollback gitops-blogging-app <revision>   # rollback if needed
```

---

## 📊 Monitoring Setup

- **Prometheus** scrapes metrics from the Kubernetes cluster (nodes, pods, and app-level metrics)
- **Grafana** visualizes them via dashboards for real-time visibility

**Tracked metrics include:**
- CPU usage
- Memory usage
- Pod health & restart counts
- Application performance (request latency, error rates)

### Quick Install (Helm)

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install monitoring prometheus-community/kube-prometheus-stack -n monitoring --create-namespace

# Access Grafana
kubectl port-forward svc/monitoring-grafana -n monitoring 3000:80
# Default login: admin / prom-operator
```

---

## 🧯 Troubleshooting

| Issue | Likely Cause | Fix |
|---|---|---|
| Argo CD app stuck `OutOfSync` | Manual cluster edit or manifest drift | `argocd app sync <app>` or check diff with `argocd app diff` |
| Pod `CrashLoopBackOff` | Bad env vars / DB not reachable | `kubectl logs <pod> -n <namespace>` and check `ConfigMap`/`Secret` |
| Image not updating after push | Manifest not updated with new tag | Confirm CI step updated `k8s/deployment.yaml` image tag |
| Trivy/OWASP pipeline failing | New CVE in dependency or base image | Bump the dependency/base image version, re-run pipeline |
| Grafana shows no data | Prometheus not scraping targets | Check `ServiceMonitor` / scrape config and target status in Prometheus UI |

---

## 🗺️ Roadmap

- [ ] Add Helm chart for the application itself (currently raw manifests)
- [ ] Integrate Slack/Teams alerts from Prometheus Alertmanager
- [ ] Add horizontal pod autoscaling (HPA) based on custom metrics
- [ ] Add Envoy Gateway / Ingress with TLS via cert-manager
- [ ] Add automated rollback on failed health checks in Argo CD
- [ ] Write integration tests into the CI pipeline

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add: your feature"`
4. Push and open a Pull Request

All PRs automatically run through the same security & CI pipeline described above.

---

## 🧰 Tools Used

`Gitleaks` · `OWASP Dependency-Check` · `Hadolint` · `Trivy` · `Docker` · `Kubernetes` · `GitHub Actions` · `Argo CD` · `Prometheus` · `Grafana`

---

## 📄 License

This project is licensed under the **MIT License**.

---

<div align="center">

### ⭐ If this project helped you, consider giving it a star!

**Built to showcase real-world DevSecOps practice** — CI/CD automation, a security-first pipeline, GitOps deployment, and Kubernetes orchestration, in one repo.

</div>
