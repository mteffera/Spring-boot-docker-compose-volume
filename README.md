This repository contains two primary applications:

demo/demo: a Spring Boot backend service with REST endpoints, H2/JPA persistence, Kafka publisher/consumer, and Resilience4j circuit breakers.
frontend/employee-ui: an Angular UI app built with Angular CLI and packaged into a static Node.js http-server container.
Important integration points:

Backend REST API: EmployeeController exposes /api/employees for create and list operations.
Kafka topic: EmployeeEventPublisher sends to the employee-created topic, and EmployeeEventConsumer listens on the same topic.
Default Kafka bootstrap server is kafka:9092 in compose and Kubernetes manifests.
Backend health endpoint is exposed via Spring Actuator at /actuator/health.
Build / run conventions:

Build & Deployment Notes (Docker Swarm):  
• Backend build: run demo/demo/mvnw.cmd clean package on Windows or ./demo/demo/mvnw clean package on Linux/macOS.
• Backend Docker image: built using demo/demo/infra.docker/Dockerfile.backend.
• Frontend build: inside frontend/employee-ui, run npm install then npm run build.
• Frontend Docker image: built using frontend/employee-ui/Dockerfile, serving assets from dist/employee-ui/browser.
• This stack is deployed using Docker Swarm (docker swarm init + docker stack deploy).
• The Compose file uses deploy: blocks, overlay networks, and replicated services — all Swarm‑specific features.
• The frontend is exposed via NodePort‑style port mapping (4200:4200).

Technologies I used in this project

Java(Version 17) + Spring Boot(Version 3.2.5) for building a clean, modular backend service with REST APIs

Apache Kafka for event‑driven communication, producers/consumers, and real‑time processing

Zookeeper for Kafka coordination and cluster stability

Angular(Version 21) for a responsive, modern frontend UI

Docker Swarm to containerize the full stack and orchestrate multi‑service environments

Kafdrop for Kafka topic inspection and message visibility

H2 Database for lightweight, in‑memory persistence during development

Resilience4j for circuit breakers and fault‑tolerant service behavior

Distributed, containerized architecture demonstrating real‑world deployment patterns
