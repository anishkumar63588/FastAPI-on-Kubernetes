# 🚀 Deploying a FastAPI Application on Kubernetes

This repository demonstrates how to deploy a **FastAPI web application on Kubernetes**, covering the essential components required for a scalable, production-ready API. It walks through containerisation, deployment, service exposure, secret management, and ingress configuration.

The project is designed to help developers understand how Kubernetes manages **availability, scaling, and traffic routing** without manual server maintenance.

---

## 📌 Features

- Lightweight **FastAPI** application
- Docker-based containerisation
- Kubernetes **Deployment** for scaling and high availability
- Kubernetes **Service** for internal and external access
- **Ingress** for domain-based routing
- Secure configuration using **environment variables and Secrets**
- Cloud-native and production-ready design

---

## 🛠️ Technologies Used

- **FastAPI** – Python web framework for APIs
- **Docker** – Containerisation platform
- **Kubernetes** – Container orchestration
- **Uvicorn** – ASGI server
- **kubectl** – Kubernetes CLI

---

## 📂 Project Structure

```
.
├── main.py                # FastAPI application
├── requirements.txt       # Python dependencies
├── Dockerfile              # Docker image definition
├── deployment.yaml         # Kubernetes Deployment
├── service.yaml            # Kubernetes Service
├── ingress.yaml            # Kubernetes Ingress
└── README.md               # Project documentation
```

---

## ⚙️ FastAPI Application

A simple FastAPI app exposing a single endpoint:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI on Kubernetes!"}
```

---

## 🐳 Containerisation

Build the Docker image:

```bash
docker build -t <your-registry>/fastapi-k8s:latest .
```

Push the image to your container registry:

```bash
docker push <your-registry>/fastapi-k8s:latest
```

---

## ☸️ Kubernetes Deployment

The **Deployment** ensures your application runs reliably and scales automatically.

Apply the deployment:

```bash
kubectl apply -f deployment.yaml
```

Key features:
- Multiple replicas for high availability
- Automatic pod restarts
- Rolling updates

---

## 🌐 Service Exposure

The **Service** exposes the FastAPI application:

```bash
kubectl apply -f service.yaml
```

Depending on configuration, the service can be:
- `ClusterIP` – internal access
- `LoadBalancer` – external access

---

## 🔐 Secrets & Environment Variables

Create a Kubernetes Secret:

```bash
kubectl create secret generic api-secrets --from-literal=API_KEY=12345
```

Reference the secret in the Deployment:

```yaml
env:
- name: API_KEY
  valueFrom:
    secretKeyRef:
      name: api-secrets
      key: API_KEY
```

This keeps sensitive data out of source code.

---

## 🌍 Ingress Configuration

Ingress enables domain-based access to the application.

Apply the ingress:

```bash
kubectl apply -f ingress.yaml
```

Example access:

```
http://fastapi.example.com
```

With an Ingress Controller and TLS configuration, HTTPS can also be enabled.

---

## 📈 Scalability & Availability

Kubernetes automatically:

- Restarts failed containers
- Distributes traffic across replicas
- Scales the application based on demand

This ensures your FastAPI app remains reliable and performant.

---

## 📄 License

This project is open-source and available under the MIT License.

---

Happy deploying! 🎉

