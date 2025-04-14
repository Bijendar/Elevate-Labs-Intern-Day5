
# 🚀 Task 5 – Kubernetes Cluster Locally with Minikube

## 📌 Objective
Build and manage a local Kubernetes cluster using **Minikube** and deploy a simple app using **kubectl** and **YAML files**.

---

## 🧰 Tools & Technologies Used
- Minikube
- kubectl
- Docker
- YAML
- Ubuntu (local setup)

---

## 🛠️ Steps Performed

### 1️⃣ Installed & Started Minikube
```bash
minikube start
kubectl get nodes
kubectl cluster-info
```

---

### 2️⃣ Created a Deployment – `deployment.yaml`
Deployed a sample `nginx` container with 2 replicas.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: nginx
        ports:
        - containerPort: 80
```

**Applied using:**
```bash
kubectl apply -f deployment.yaml
kubectl get pods
```

---

### 3️⃣ Exposed the Deployment – `service.yaml`
Created a NodePort service to access the app from browser.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

**Applied using:**
```bash
kubectl apply -f service.yaml
kubectl get services
```

**Opened the app in browser:**
```bash
minikube service myapp-service
```

---

### 4️⃣ Scaled the Deployment
Increased pod count to 4 using:

```bash
kubectl scale deployment myapp-deployment --replicas=4
kubectl get pods
```

---

### 5️⃣ Checked Logs & Pod Info
To check status and events:
```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

---

## 📁 Folder Structure

```
📦task-5-kubernetes
 ┣ 📂screenshots
 ┃ ┣ get-pods.png
 ┃ ┣ get-services.png
 ┃ ┗ app-in-browser.png
 ┣ deployment.yaml
 ┣ service.yaml
 ┗ README.md
```

---

## 📸 Screenshots Attached
- Pods and Services (`kubectl get pods`, `kubectl get services`)
- App running in browser

---

## 💬 Key Concepts Practiced
- Deployments, Pods, and Services
- Minikube for local K8s cluster
- Scaling apps in Kubernetes
- Viewing logs and pod details using `kubectl`


