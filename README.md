# 🩺 Medical RAG Chatbot

A Medical RAG Chatbot built with Python that helps retrieve and generate answers from medical knowledge sources. The project is containerized with Docker, automated with Jenkins, scanned with Trivy, pushed to AWS ECR, and deployed to AWS App Runner using a complete CI/CD pipeline.

---

## 📌 Project Overview

This project demonstrates an end-to-end MLOps/DevOps workflow for a Medical RAG Chatbot. It covers source control, local development setup, Jenkins-based automation, vulnerability scanning, image publishing to AWS ECR, and deployment to AWS App Runner.

The goal of the project is to provide a production-style pipeline for building, scanning, and deploying an AI-powered application in a reliable and repeatable way.

---

## 🧱 Architecture Flow

GitHub → Jenkins → Docker Build → Trivy Scan → AWS ECR → AWS App Runner

### Flow Explanation
- **GitHub** → Stores the source code and Jenkinsfile.
- **Jenkins** → Automates the build, scan, push, and deployment pipeline.
- **Docker Build** → Packages the Medical RAG Chatbot into a container image.
- **Trivy Scan** → Checks the image for vulnerabilities before deployment.
- **AWS ECR** → Stores the Docker image securely in AWS.
- **AWS App Runner** → Deploys the containerized application and makes it publicly accessible.

---

## ✨ Features

- Medical RAG-based chatbot application.
- Local development support using Python virtual environment.
- Dockerized application for consistent runtime.
- Jenkins CI/CD pipeline for automation.
- Trivy vulnerability scanning.
- AWS ECR image publishing.
- AWS App Runner deployment.

---

## 📁 Repository Structure

```bash
LLMOPS-2-TESTING-MEDICAL/
├── custom_jenkins/
│   └── Dockerfile
├── Dockerfile
├── Jenkinsfile
├── src/
├── tests/
├── README.md
└── pyproject.toml




<img width="1586" height="992" alt="MEDICAL RAG CHATBOT FLOW DIAGRAM" src="https://github.com/user-attachments/assets/0eb4b547-fcd6-4dab-bb0f-7c57276f4206" />
