# 🚀 DevOps Flask App by Raedbari

This project is a simple Flask-based web application that is containerized with Docker and deployed on a Kubernetes cluster hosted on an AWS EC2 instance.

---

### 1. 🔧 Create an EC2 Instance

### 2. 🖥️ Connect to EC2 via MobaXterm

### ⚙️ Haven’t Installed Kubernetes with kubeadm?

If you haven’t installed Kubernetes using `kubeadm` on your master and worker nodes, follow the installation steps in the following repository:

🔗 Go to the **install-k8s** repository

---

### 📦 Project Setup

```bash
# After installing kubeadm
mkdir app && cd app

# Create the Flask app
vim app.py
```

- [python-app.py](./app/app.py)

```bash
# Add Flask to requirements
vim requirements.txt
```

```
flask
```

```bash
# Return to the home directory
cd ..
```

---

### 🐳 Dockerize the App

```bash
vim Dockerfile
```

- [Dockerfile](./Dockerfile)

```bash
# Build and push the Docker image
docker build -t raedbari/devops-app:latest .
docker push raedbari/devops-app:latest
```

> 🔹 **Note:** Make sure your GitHub repository is named `devops-app`.  
> If not, update the image name accordingly:

```bash
docker build -t your-username/your-repo-name:latest .
docker push your-username/your-repo-name:latest
```

> It's recommended to copy the push command directly from your Docker Hub repo for accuracy.

---

### 📂 Create Kubernetes Manifests

```bash
# Create a directory for YAML files
mkdir k8s && cd k8s

# Create Deployment manifest
vim deployment.yaml
```

- [deploy.yaml](./k8s/deploy.yaml)

> ℹ️ Note: A `tolerations` section is added because some users may run this on a master node, which has a taint `node-role.kubernetes.io/control-plane` preventing pods from running on it.

```bash
# Create Service manifest
vim service.yaml
```

- [svc.yaml](./k8s/services.yaml)

---

### 🚀 Deploy to Kubernetes

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

---

### 🌐 Access the App

Open your browser and navigate to:

```
http://<EC2-IP>:30007
```

Replace `<EC2-IP>` with your EC2 instance’s public IP address.