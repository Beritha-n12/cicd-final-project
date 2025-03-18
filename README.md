# CI/CD Final Project

## Overview
This project demonstrates a complete **CI/CD pipeline** using **GitHub Actions, Tekton, and OpenShift**. It includes:
- **GitHub Actions** for linting and unit testing
- **Tekton tasks** for linting, unit testing, and building an image
- **An OpenShift CI Pipeline** that integrates these Tekton tasks
- **Automated deployment** to an OpenShift cluster

## Repository Structure
```
.cicd-final-project/
├── .github/workflows/workflow.yml       # GitHub Actions pipeline
├── .tekton/tasks.yml                    # Tekton tasks for CI/CD
├── .tekton/pipeline.yml                 # Tekton pipeline definition
├── .tekton/deploy.yml                    # Tekton deployment task
├── requirements.txt                      # Project dependencies
├── src/                                  # Application source code
├── tests/                                # Unit tests
└── README.md                             # Project documentation
```

## Prerequisites
Before running this project, ensure you have:
- **Git** installed
- **Docker** installed
- **Python 3.8+** installed
- **An OpenShift Cluster** set up
- **Tekton CLI (`tkn`)** installed

## Getting Started
### 1️⃣ Clone the Repository
```bash
git clone https://github.com/Beritha-n12/cicd-final-project.git
cd cicd-final-project
```

### 2️⃣ Set Up Virtual Environment & Install Dependencies
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
pip install -r requirements.txt
```

### 3️⃣ Run Linting Locally
```bash
flake8 .
```

### 4️⃣ Run Unit Tests Locally
```bash
pytest tests/
```

## CI/CD Pipeline Details
### 🚀 **GitHub Actions (CI Pipeline)**
Defined in `.github/workflows/workflow.yml`, this workflow:
- Runs **linting** using `flake8`
- Runs **unit tests** using `pytest`

### 🛠 **Tekton Tasks**
Defined in `.tekton/tasks.yml`, this includes:
- **Linting Task**: Runs `flake8` checks
- **Testing Task**: Executes `pytest`
- **Build Task**: Uses `buildah` to create and push an image
- **Cleanup Task**: Removes temporary files
- **Nose Test Task**: Runs `nosetests`

### 🔄 **Tekton Pipeline (OpenShift CI Pipeline)**
Defined in `.tekton/pipeline.yml`, it orchestrates:
1. **Linting**
2. **Testing**
3. **Building the Image**
4. **Deploying to OpenShift**

## Deploying on OpenShift
### 1️⃣ Apply Tekton Pipeline
```bash
oc apply -f .tekton/pipeline.yml
```

### 2️⃣ Run the Pipeline
```bash
tkn pipeline start ci-pipeline --showlog
```

### 3️⃣ Check OpenShift Deployment
```bash
oc get pods
oc get svc
oc get routes
```
