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

## ☸️ Deployment Process (EKS + Argo CD)

1. Build and push the Docker image
2. Update Kubernetes manifests with the new tag
3. Push changes to GitHub
4. Argo CD detects the change
5. Argo CD automatically deploys to the EKS cluster

📌 Argo CD ensures continuous synchronization between GitHub and the cluster — any drift is automatically corrected.

---

## 📊 Monitoring Setup

- **Prometheus** scrapes metrics from the Kubernetes cluster
- **Grafana** visualizes them via dashboards

**Tracked metrics include:**
- CPU usage
- Memory usage
- Pod health
- Application performance

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
