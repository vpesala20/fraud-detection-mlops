# Fraud Detection MLOps Pipeline (Production-Oriented)

This project simulates a **production-style MLOps setup** for a **fraud detection model**.  
It focuses on how a model would be **served, containerized, and automated with CI/CD**, not just trained in a notebook.

The goal is to demonstrate **how you would deploy and operate a fraud detection model in the real world**:
- API-based model serving  
- Dockerized application  
- Automated tests + CI/CD  
- Ready to plug into AWS (ECR/EKS) or any cloud-native stack  

---

## 🔍 Problem Overview

Fraud detection is a classic **high-risk, high-volume** machine learning use case.

- Incoming transactions must be evaluated quickly (low latency)
- Models must be **versioned, monitored, and safe to roll back**
- CI/CD must ensure that **broken models or APIs never reach production**

This project shows the **MLOps side** of that story:
how we package, test, ship, and (conceptually) deploy a fraud model.

---

## 🧱 Architecture Overview

**High-level flow:**

1. **Client / Upstream Service**  
   Sends a transaction payload (amount, merchant, location, risk signals, etc.) to the API.

2. **Fraud Detection API (Python)**  
   - Lives in `src/api/app.py`  
   - Exposes `/predict`  
   - Returns `fraud` / `not_fraud` + probability.

3. **Containerization (Docker)**  
   - `Dockerfile` builds a production-ready image  
   - Requirements pinned in `requirements.txt`

4. **CI/CD Pipeline (GitHub Actions)**  
   - Validates code  
   - Builds Docker image  
   - Runs tests  
   - (Optionally) pushes container to AWS ECR  
   - Ready for EKS deployment

> 📌 Add architecture images later into:  
> `images/fraud-mlops-architecture.png`  
> `images/fraud-mlops-cicd.png`

---

## 🧰 Tech Stack

- **Python**
- **Docker**
- **GitHub Actions**
- **MLOps best practices**
- **API-based model serving**

---

## 📂 Repository Structure

```bash
mlops-fraud-detection/
  ├── .github/
  │   └── workflows/
  │       └── ci-cd.yml        # CI/CD pipeline: lint, build, (optional) push
  ├── src/
  │   └── api/
  │       └── app.py           # Fraud detection API entrypoint
  ├── Dockerfile               # Builds the container image
  ├── requirements.txt         # Python dependencies
  └── README.md                # Project documentation

