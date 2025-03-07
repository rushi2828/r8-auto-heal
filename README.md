# r8-auto-heal
## Project Folder Structure
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
└── README.md             # Project documentation
```
