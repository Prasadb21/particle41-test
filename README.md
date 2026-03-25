# SimpleTimeService – DevOps Challenge (Particle41)

## 📌 Overview

This project demonstrates a complete DevOps workflow by implementing a minimal web service and deploying it using containerization, Kubernetes, and Infrastructure as Code (Terraform on AWS).

The application returns the current timestamp and the IP address of the requester in JSON format.

---

## 🧰 Tech Stack

* Python (Flask)
* Docker
* DockerHub (Container Registry)
* Kubernetes (KIND / k3s compatible)
* Terraform (AWS – VPC + EKS)

---

## 📁 Project Structure

```
.
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── k8s/
│   └── microservice.yml
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── terraform.tfvars
│   └── provider.tf
└── README.md
```

---

## 🚀 Application Details

### Endpoint

```
GET /
```

### Sample Response

```json
{
  "timestamp": "2026-03-25T12:38:55.262249",
  "ip": "127.0.0.1"
}
```

---

# 🧪 Task 1 – Application, Docker & Kubernetes

## ▶️ Run Application Locally

```bash
cd app
pip3 install -r requirements.txt
python3 app.py
```

Access:

```
http://localhost:5000
```

---

## 🐳 Build & Run Docker Image

```bash
cd app
docker build -t simple-time-service .
docker run -p 5000:5000 simple-time-service
```

---

## 📦 DockerHub Image

Public image:

```
gappi2108/simple-time-service:latest
```

---

## ☸️ Deploy to Kubernetes

```bash
kubectl apply -f k8s/microservice.yml
```

Verify:

```bash
kubectl get pods
kubectl get svc
```

---

## 🌐 Access Application

### Option 1: Port Forward (Recommended)

```bash
kubectl port-forward --address 0.0.0.0 svc/simple-time-service 8081:80
```

Access:

```
http://localhost:8081
```

---

## ⚠️ Notes

* Container runs as a **non-root user** (security best practice)
* Kubernetes Service uses **NodePort** (LoadBalancer not used as per requirement)
* Resource limits are defined for better scheduling and stability

---

# 🌍 Task 2 – Terraform (AWS Infrastructure)

## 📌 Overview

Terraform is used to provision AWS infrastructure including:

* VPC with public and private subnets
* EKS cluster
* Managed node group (2 nodes, m6a.large)
* Worker nodes deployed in private subnets

---

## ⚙️ Prerequisites

* AWS account
* AWS CLI configured (`aws configure`)
* Terraform installed

---

## ▶️ Deploy Infrastructure

```bash
cd terraform
terraform init
terraform plan
terraform apply
```

---

## 🧹 Destroy Infrastructure

```bash
terraform destroy
```

---

## ⚠️ Important Notes

* No AWS credentials are stored in the repository
* Infrastructure is fully parameterized using variables
* Code is reusable across AWS accounts

---

# ✅ Acceptance Criteria Covered

### Task 1

* Minimal web service implemented
* Docker image built and pushed to DockerHub
* Kubernetes Deployment and Service created
* Application accessible via Kubernetes

### Task 2

* VPC with public and private subnets created
* EKS cluster provisioned
* Node group configured with required instance type
* Infrastructure deployable via `terraform apply`

---

# 💡 Improvements (Optional Enhancements)

* CI/CD pipeline (GitHub Actions)
* Helm chart deployment
* Monitoring (Prometheus + Grafana)
* Remote Terraform backend (S3 + DynamoDB)

---

# 👤 Author

Prasad Bhalkikar

