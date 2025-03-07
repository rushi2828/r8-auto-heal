# ⚙️ R8 Auto Heal 

**R8 Auto Heal** is a Kubernetes-based Self-Healing System that automatically detects issues in applications and resolves them using predefined actions.

## 🌟 Features
- Self-Healing System with Prometheus & Alertmanager
- Custom Alert Rules
- Automatic Pod Restart on Failure
- Easy Setup with Kubernetes
- Observability Dashboard

## 📁 Project Folder Structure
```
r8-auto-heal/
├── app/                  # FastAPI app code
│   ├── main.py           # Main API code
│   ├── Dockerfile        # Docker build file
│   ├── requirements.txt  # Python dependencies
│   └── config.py         # App Configurations
├── k8s/                  # Kubernetes manifests
│   ├── deployment.yaml   # Deployment with Liveness and Readiness probes
│   ├── service.yaml      # Service manifest
│   ├── configmap.yaml    # ConfigMap for environment variables
│   └── prometheus/        # Prometheus setup
│       ├── prometheus-config.yaml    # Prometheus configuration
│       ├── alert-rules.yaml          # Custom alert rules
│       ├── alertmanager-config.yaml  # Alertmanager configuration
└── README.md             # Documentation
```

## 🔑 Prerequisites 
- Docker 
- Kubernetes (Kind luster)
- Helm
- kubectl

## 🚀 Installation

### 1. 🧑‍💻 Clone the Repository
```bash
git clone https://github.com/rushi2828/r8-auto-heal.git
cd r8-auto-heal
```

### 2. 📊 Install Prometheus & Alertmanager

#### Step 1: Add Prometheus Helm Repository
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

#### Step 2: Install Prometheus Stack
```bash
helm install prometheus prometheus-community/kube-prometheus-stack -f prometheus/values.yaml
```

#### Step 3: Verify Prometheus Installation
```bash
kubectl get pods
```
✅ You should see Prometheus, Alertmanager, and related pods running.

![image](https://github.com/user-attachments/assets/2294e0ca-e836-4918-b360-597a498637d4)

### 3. 🌐 Access Prometheus & Alertmanager UIs

#### Prometheus UI
```bash
kubectl port-forward svc/prometheus-kube-prometheus-prometheus 9090:9090
```
URL: [http://localhost:9090](http://localhost:9090)
![image](https://github.com/user-attachments/assets/5d63f4ff-819d-4dd3-8fdd-adb984bbb3ee)


#### Alertmanager UI
```bash
kubectl port-forward svc/prometheus-kube-prometheus-alertmanager 9093:9093
```
URL: [http://localhost:9093](http://localhost:9093)
![image](https://github.com/user-attachments/assets/3e0fab42-9887-4c8e-8107-82479cdae36e)


### 4. ⚠️ Apply Alert Rules

Apply custom alert rules:
```bash
kubectl apply -f prometheus/alerts.yaml
```

### 5. 🔥 Deploy Self-Healing System

Deploy the auto-healing system with custom handlers:
```bash
kubectl apply -f manifests/
```

### 6. 🎯 Testing Self-Healing System
1. Delete a running pod:
```bash
kubectl delete pod <pod-name>
```
2. Prometheus will fire an **UnhealthyPod** alert.
3. Alertmanager will trigger the webhook API.
4. Webhook API automatically recreates the unhealthy pod.

---

## 📌 Prometheus Alert Rule Example
```yaml
alert: UnhealthyPod
expr: kube_pod_container_status_ready == 0
for: 1m
labels:
  severity: critical
annotations:
  summary: "Pod {{ $labels.pod }} is not healthy"
```

---

## 🔗 References
- [Prometheus](https://prometheus.io/)
- [Kubernetes](https://kubernetes.io/)
- [FastAPI](https://fastapi.tiangolo.com/)
- [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/)

---

## ✍️ Author
[Rushi2828](https://github.com/rushi2828)

Happy Automating 🚀!
