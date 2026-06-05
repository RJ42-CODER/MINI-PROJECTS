# Project1: Linux Sysadmin Automation Kit - linuz zip

## Overview
A Bash script that performs automated server health checks and stores formatted reports in a log file.

## Features
- Disk space monitoring
- RAM usage tracking
- Running services check
- Formatted log report output
- Automated hourly execution via cron job

## Skills Applied here are
`Linux` `Bash` `Cron` `Logging`

## Usage

### To Run manually
```bash
bash health_check.sh
```

### Setting up cron job (runs every hour)
```bash
crontab -e
```

---------------------------------------------------------------------------

# Project2: Git Workflow Simulator - githubsimul zip

## What is this?
A mini project where I simulated how a real dev team works on GitHub.
I set up a shared repo and pretended to be a 3-person team — branches,
pull requests, code reviews, merge conflicts, the whole thing.

## What I did
- Created a GitHub repo with **branch protection** on `main` (no direct pushes allowed)
- Made feature branches like a real team would
- Opened **Pull Requests** and did mock code reviews
- Deliberately caused a **merge conflict** and fixed it
- Tagged a **release** at the end
- Wrote a `CONTRIBUTING.md` explaining the whole workflow

## Why I built this
To understand how professional teams actually use Git day-to-day —
not just `git add`, `git commit`, `git push`, but the real collaboration flow.

## Skills practiced
`Git` `GitHub` `Branching` `PRs` `Docs`


---------------------------------------------------------------------------

# Project3: CI Pipeline for a Python App day3 zip

## Overview
A simple Python calculator wired up with a full CI pipeline using GitHub Actions.
Every push automatically runs linting, unit tests, and a coverage report —
just like a real production repo.

## What's inside
project/
├── calculator.py        
├── test_calculator.py   
├── .github/workflows/
│   └── ci.yml           
└── .gitignore

## Tools Used
| Tool | Purpose |
|------|---------|
| Python | Core language |
| pytest | Unit testing |
| flake8 | Linting |
| GitHub Actions | CI automation |
| Coverage.py | Test coverage |

## How to Run

### Install dependencies
pip install pytest flake8 pytest-cov

### Run tests
pytest test_calculator.py

### Run tests with coverage
pytest --cov=calculator test_calculator.py

### Run linter
flake8 calculator.py

## What I'd improve next
- Add edge case tests (division by zero, negative numbers)
- Set a minimum coverage threshold (80%+)
- Add a requirements.txt
- Test across multiple Python versions


# Project6: Automated Artifact Versioning Pipeline - SkillsTrainingAcademyJuneBatch1 zip

## Overview
A Flask API wired up with a full CI/CD pipeline using GitHub Actions.
Every push automatically tests, builds a Docker image, tags it with
the git commit SHA, and pushes it to Docker Hub.

## What's inside
SkillsTrainingAcademyJuneBatch1/
├── app.py
├── test_app.py
├── dockerfile
├── requirements.txt
├── nginx.html
├── reports/
│   └── pylint-report.txt
├── backups/
│   ├── calculator.yml
│   └── ci_old.yml
└── .github/workflows/
    └── ci.yml

## API Endpoints
| Endpoint | Method | Response |
|----------|--------|---------|
| `/` | GET | `Hello DevOps Students!` |
| `/health` | GET | `{"status": "UP"}` |
| `/userDetails` | GET | `{"name": "Riya Jamsutkar", "age": 21, ...}` |

## Tools Used
| Tool | Purpose |
|------|---------|
| Flask | Backend API |
| pytest | Unit testing |
| Docker | Containerising the app |
| Docker Hub | Image registry |
| GitHub Actions | CI/CD automation |

## How to Run

### Run locally
pip install -r requirements.txt
python app.py

### Run tests
pytest test_app.py

### Build and run with Docker
docker build -f dockerfile -t flask-ci-demo .
docker run -p 5000:5000 flask-ci-demo

## Triggering a versioned release
git tag v1.0.0
git push origin v1.0.0

## What I'd improve next
- Add more API endpoints with real data
- Add a database (PostgreSQL)
- Auto-generate changelog from commit messages
- Multi-platform Docker builds (amd64 + arm64)


# Project8: Kubernetes Horizontal Pod Autoscaler assessment zip

## Overview
A CPU-intensive Flask app deployed to Kubernetes with Horizontal Pod Autoscaler configured.
HPA automatically scales pods from a minimum of 2 up to a maximum of 8 based on CPU usage.
The `hey` load testing tool simulates real traffic to demonstrate auto-scaling in action.

## Project structure
mini-project-08/
├── app.py
├── Dockerfile
├── requirements.txt
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── hpa.yaml
└── .github/workflows/
└── deployment.yaml

## Stack
| Component | Technology | Role |
|-----------|------------|------|
| App | Flask (Python) | CPU-intensive endpoint to trigger scaling |
| Container | Docker | Packages the app into an image |
| Orchestration | Kubernetes | Runs and manages pods |
| Auto-scaling | HPA | Scales pods up/down based on CPU % |
| Load testing | hey | Generates HTTP traffic to spike CPU |
| Metrics | Metrics Server | Feeds CPU data to HPA |

## How it works
hey sends requests
↓
Flask CPU spikes above 50%
↓
Metrics Server detects high CPU
↓
HPA scales from 2 pods → up to 8 pods
↓
Traffic load drops
↓
HPA scales back down to 2 pods

## HPA configuration
| Setting | Value |
|---------|-------|
| Min replicas | 2 |
| Max replicas | 8 |
| Scale up trigger | CPU above 50% |
| Metric source | Metrics Server |

## Commands

### Start the cluster
```bash
minikube start
```

### Enable Metrics Server (required for HPA)
```bash
minikube addons enable metrics-server
```

### Build and load the Docker image
```bash
docker build -t flask-cpu-app:latest .
minikube image load flask-cpu-app:latest
```

### Deploy everything to Kubernetes
```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl apply -f k8s/hpa.yaml
```

### Verify everything is running
```bash
kubectl get pods
kubectl get hpa
kubectl get svc
```

### Get the app URL
```bash
minikube service flask-app --url
```

### Run load test to trigger auto-scaling
```bash
hey -z 2m -c 50 http://<minikube-url>/cpu
```

### Watch pods scale in real time (separate terminal)
```bash
kubectl get hpa -w
kubectl get pods -w
```

### Check CPU usage per pod
```bash
kubectl top pods
```

### See full HPA scaling history
```bash
kubectl describe hpa flask-hpa
```

### View pod logs
```bash
kubectl logs -l app=flask-app
```

### Delete everything
```bash
kubectl delete -f k8s/
```

## What I'd improve next
- Add Prometheus and Grafana to visualize scaling events on a live dashboard
- Use Terraform to provision the cluster as Infrastructure as Code
- Add a custom HPA metric based on HTTP requests per second instead of CPU
- Set resource requests and limits on all pods for more accurate HPA decisions
- Add alerts when pod count hits the maximum of 8

-----------------------------------------------------------------