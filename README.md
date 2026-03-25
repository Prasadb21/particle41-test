This project implements a minimal microservice that returns the current timestamp and the IP address of the requester.

It demonstrates a complete DevOps workflow including:

Application development (Python Flask)
Containerization (Docker)
Container registry (DockerHub)
Kubernetes deployment (Deployment + Service)

🚀 Application Details
Endpoint:
GET /
Sample Response:
{
  "timestamp": "2026-03-25T12:38:55.262249",
  "ip": "127.0.0.1"
}

🧰 Tech Stack
Python (Flask)
Docker
Kubernetes
DockerHub

📁 Project Structure
.
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── k8s/
│   └── microservice.yml
└── README.md
⚙️ Prerequisites

Ensure the following tools are installed:

Python 3.x
Docker
Kubernetes cluster (Minikube / KIND / k3s)
kubectl
▶️ Run Application Locally
cd app
pip3 install -r requirements.txt
python3 app.py

Access:

http://localhost:5000

🐳 Build & Run Docker Image
cd app
docker build -t simple-time-service .
docker run -p 5000:5000 simple-time-service
📦 DockerHub Image

Public image available at:

gappi2108/simple-time-service:latest

☸️ Deploy to Kubernetes
kubectl apply -f k8s/microservice.yml

Check pods:

kubectl get pods

Check service:

kubectl get svc

🌐 Access Application
Option 1: Port Forward
kubectl port-forward --address 0.0.0.0 svc/simple-time-service 8081:80

Access:

http://localhost:8081

⚠️ Notes

Container runs as a non-root user (security best practice)
Service type is NodePort (as required, LoadBalancer not used)
Resource limits are defined in Kubernetes manifest
✅ Acceptance Criteria Covered
Minimal web service implemented
Docker image built and pushed to DockerHub
Kubernetes Deployment and Service created
Application accessible via Kubernetes
Proper documentation provided

💡 Improvements (Optional)
Add CI/CD pipeline (GitHub Actions)
Add Helm chart for deployment
Add logging/monitoring (Prometheus, Grafana)

👤 Author

Prasad Bhalkikar
