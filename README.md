# 🚀 Secure EKS Microservice Deployment

This repository showcases how to provision a secure, production-ready AWS EKS cluster using **Terraform**, and deploy a hardened microservice on **Kubernetes** following best practices. It's designed for cloud security enthusiasts, DevSecOps engineers, and anyone looking to combine infrastructure-as-code with container security.

---

## 🧱 Features

- 🔐 EKS cluster with IRSA-enabled node groups
- 🛡️ Hardened Kubernetes deployment (non-root, read-only FS, no privilege escalation)
- 🔧 S3 read-only IAM role attached to pod via service account (IRSA)
- 🌐 VPC with public/private subnets using Terraform modules
- ✅ Checkov integration with custom policies for IaC and K8s security validation
- 💻 Manual CI/CD friendly (GitHub Actions optional, commented out)

---

## 📁 Directory Structure

```bash
.
├── terraform/                  # EKS, VPC, IAM roles
├── k8s/                        # K8s manifests (deployment, service)
├── checkov-custom-policies/   # Custom Checkov rules
└── README.md                   # This file
```

---

## ⚙️ Technologies Used

- AWS (EKS, IAM, VPC)
- Terraform (modularized)
- Kubernetes (apps/v1, RBAC, Services)
- Checkov (custom and default policy scans)
- GitHub Actions (optional manual CI)

---

## 📌 Usage

### 🛠️ Provision Infrastructure
```bash
cd terraform
terraform init
terraform apply
```

### 🔗 Update kubeconfig
```bash
aws eks update-kubeconfig --region us-east-1 --name demo-eks-cluster
```

### 🚀 Deploy Application
```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### 🔍 Run Checkov (Optional)
```bash
checkov -d terraform --external-checks-dir checkov-custom-policies
```

---

## ✨ Custom Checkov Rules

- Disallow public Security Groups (`0.0.0.0/0`)
- Enforce `securityContext` on all Kubernetes pods/deployments

---

## 📦 Notes

- This project avoids automatic CI/CD execution; GitHub Actions are commented for manual use only.
- You can integrate this into a CI pipeline using GitHub Actions, Jenkins, or GitLab CI when ready.

---

## 👨‍💻 Author

**Mariano Dorado**  
Sr. Cybersecurity Engineer  
[GitHub →](https://github.com/nanodorado)
