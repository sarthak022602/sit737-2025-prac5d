# 🚀 SIT737 Task 5.2D – Dockerized Node.js Microservice with Health Check

This repository hosts the final working version of a Node.js-based microservice built and containerized for the **SIT737 – Cloud-Native Application Development** unit (Task 5.2D).

The microservice is designed with the following goals:
- ✔️ Build a simple Express-based web server
- 🐳 Containerize it using Docker
- 🔁 Orchestrate it using Docker Compose
- 💓 Integrate a health check endpoint
- 📦 Prepare it for deployment to a cloud platform like Google Cloud Run

---

## 📁 Project Structure

sit737-task-5-2d/ │ ├── index.js # Main Express server file ├── Dockerfile # Docker configuration ├── docker-compose.yml # Compose file with health check ├── package.json # Node.js metadata and dependencies ├── .gitignore # Files ignored by Git └── README.md # This documentation


---

## 🧠 Learning Outcomes (Task 5.2D)

- Understand and apply microservice containerization
- Use Docker and Docker Compose to manage local development environments
- Implement basic health check monitoring using Docker Compose
- Gain familiarity with deploying microservices to platforms like Google Cloud Run

---

## 🔧 Technologies Used

- **Node.js** (v18)
- **Express.js** web framework
- **Docker** for containerization
- **Docker Compose** for orchestration
- **cURL** for health checks
- **GitHub** for version control

---

## 🌐 API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET    | `/`  | Returns a success message indicating the app is running |
| ALL    | `*`  | Catches all other requests with a 404 error message |

---

## 🧪 Health Check Overview

Docker Compose provides the ability to monitor the health of services with a `healthcheck`. In this app:

```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:8080"]
  interval: 30s
  timeout: 10s
  retries: 3
This setup:

Tests the health of the app every 30 seconds

Times out if no response in 10 seconds

Fails if 3 consecutive checks are unsuccessful

⚙️ Running the App
1. 📦 Install Dependencies (Optional)
If you want to run outside Docker:


npm install
node index.js
2. 🐳 Run via Docker Compose

docker-compose up --build
Visit the app at http://localhost:3010

📂 Important Files Explained
🔸 index.js
Main Express server that:

Serves GET / route

Handles 404 errors

Listens on dynamic PORT (default: 8080)

js

app.get('/', (req, res) => {
  res.send('✅ Hello from Dockerized Node.js app running for SIT737 Task 5.2D!');
});
🔸 Dockerfile
dockerfile

FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD ["node", "index.js"]
🔸 docker-compose.yml

version: '3.8'

services:
  web:
    build: .
    ports:
      - "3010:8080"
    restart: always
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080"]
      interval: 30s
      timeout: 10s
      retries: 3
🔸 .gitignore
gitignore

node_modules
.env
☁️ Deployment (Optional)
To deploy this service on Google Cloud Run, first build and push the Docker image to Google Container Registry or Artifact Registry, then:

gcloud run deploy sit737-app \
  --image gcr.io/[PROJECT_ID]/sit737-app \
  --platform managed \
  --region australia-southeast1 \
  --allow-unauthenticated
📌 Future Enhancements
Implement unit and integration testing (Jest or Mocha)

Add environment configuration with .env

Add logging and error tracking

Containerize using multi-stage builds for optimization

👨‍💻 Author
Sarthak Dutta
Master's Student, Deakin University
📘 SIT737 – Cloud Native Application Development
🔗 GitHub

📃 License
MIT License. You are free to use, modify, and distribute this software.

🏁 Final Note
This project demonstrates the full lifecycle of a microservice — from development to containerization and orchestration — as aligned with cloud-native best practices.


---



    

