Edge AI Service: Continuous Delivery & Deployment with Spring Boot & Docker Compose
Overview
This project demonstrates a continuous delivery and deployment (CI/CD) pipeline for an Edge AI Service using Spring Boot and Docker Compose. The system enables seamless model updates, scalable inference, and automated deployment on edge devices, ensuring efficient real-time AI processing.

Features
✅ Spring Boot-based Edge AI Service – RESTful API for AI inference requests.
✅ Dockerized Deployment – Containerized microservices for easy scalability.
✅ Continuous Delivery (CD) Pipeline – Automates deployment using GitHub Actions/Jenkins.
✅ Load Balancing & Fault Tolerance – Uses Docker Compose for multi-container orchestration.
✅ Edge-Optimized AI Inference – Runs lightweight models on edge hardware (e.g., Jetson, Raspberry Pi).

System Architecture
Spring Boot API – Handles AI inference requests.
AI Model Server – Serves pre-trained models via TensorFlow Serving/PyTorch.
Docker Compose – Manages containerized services.
CD Pipeline – Automates deployment on edge nodes.
Installation & Setup
1. Clone the Repository
bash
Copy
Edit
git clone https://github.com/nkenyelio/edgeaiservice.git
cd edgeaiservice
2. Build & Run with Docker Compose
docker-compose up --build -d
3. Access the API
bash
Copy
Edit
curl -X POST http://localhost:8080/infer -d '{"input": "image.jpg"}' -H "Content-Type: application/json"
Configuration
Modify docker-compose.yml to update services, ports, and volume mappings. Example:

name: CI/CD for Edge AI Service
on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Build & Push Docker Image
        run: |
          docker build -t nkenye1982/mhealth ai service:1.0 .
          docker login -u ${{ secrets.DOCKER_USER }} -p ${{ secrets.DOCKER_PASS }}
          docker push nkenye1982/mhealth ai service:1.0

      - name: Deploy on Edge Device
        run: |
          ssh user@edge-device "docker pull nkenye1982/mhealth ai service:1.0 && docker-compose up -d"

