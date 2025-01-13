# Deploying Containers on Elastic Beanstalk

## Overview
In this project, I used **Docker** to create a custom container image for my website and deployed it on the internet using **AWS Elastic Beanstalk**. This documentation outlines the steps I followed, the challenges I faced, and how I resolved them to successfully deploy the application.
![Screenshot 2025-01-05 150519](https://github.com/user-attachments/assets/3e3ad9b3-5504-4a18-8646-776721475572)

---

## Table of Contents
1. [What is Docker?](#what-is-docker)
2. [Understanding Containers](#understanding-containers)
3. [Running an Nginx Image](#running-an-nginx-image)
4. [Creating a Custom Docker Image](#creating-a-custom-docker-image)
5. [Running My Custom Image](#running-my-custom-image)
6. [Introduction to Elastic Beanstalk](#introduction-to-elastic-beanstalk)
7. [Deploying a Custom Image with Elastic Beanstalk](#deploying-a-custom-image-with-elastic-beanstalk)
8. [Deploying App Updates](#deploying-app-updates)
9. [Summary](#summary)

---

## What is Docker?
**Docker** is a tool for creating and managing containers. Containers package up an application and all its dependencies, ensuring that it runs consistently across different environments.

- **Docker Desktop**: A program used to manage containers, create new ones, adjust their settings, and monitor their performance.
- **Docker Daemon**: Often referred to as the Docker engine, it runs containers and manages their lifecycle.

![Screenshot 2025-01-05 151351](https://github.com/user-attachments/assets/3bd088ca-ef75-439a-8fe6-a70087e32ecd)

---

## Understanding Containers
**Containers** package up an application along with all the dependencies it needs to run, ensuring compatibility across systems.

### Key Concepts:
- **Container Image**: A blueprint or template for creating containers. It includes application code, libraries, and dependencies.
- **Dockerfile**: A file that provides instructions for building custom Docker images.

---

## Running an Nginx Image
To test Docker, I first ran an Nginx container, which is commonly used as a web server for handling web traffic.

### Command:
```bash
docker run -d -p 80:80 nginx
```

- **Explanation**:
  - `-d`: Runs the container in detached mode.
  - `-p 80:80`: Maps the container's port 80 to the host's port 80.
  - `nginx`: Specifies the Nginx image.

![Screenshot 2025-01-11 013045](https://github.com/user-attachments/assets/6bd25aa8-33f9-44e7-b69f-de6a7935804c)

This successfully started the Nginx container on port 80, allowing me to serve a basic webpage.

---

## Creating a Custom Docker Image
Using Docker, I built a custom image for my web application by creating a **Dockerfile**. The Dockerfile provides step-by-step instructions for Docker to build an image.

### Dockerfile Example:
```dockerfile
# Use the official Nginx image as the base
FROM nginx:latest

# Copy a custom HTML file to replace the default Nginx HTML file
COPY index.html /usr/share/nginx/html/

# Expose port 80 for web traffic
EXPOSE 80
```

📌 **Screenshot Placeholder**: Add a screenshot of the `index.html` file contents.

### Command to Build the Image:
```bash
docker build -t my-web-app .
```

- **Explanation**:
  - `-t my-web-app`: Tags the image with the name `my-web-app`.
  - `.`: Indicates that the Dockerfile is in the current directory.

![Screenshot 2025-01-06 134138](https://github.com/user-attachments/assets/e2dcf704-ee19-473d-91ed-77a0640e0a4c)

This created a custom Docker image that replaces the default Nginx webpage with my custom `index.html`.

---

## Running My Custom Image
When I first attempted to run my custom image, I encountered an error:

### Error:
```bash
Error response from daemon: Bind for 0.0.0.0:80 failed: port is already allocated.
```

- **Cause**: The Nginx container I had previously started was still running on port 80.
- **Solution**: Stopped the existing container using the following command:
  ```bash
  docker stop <container_id>
  ```
![image](https://github.com/user-attachments/assets/518ea379-d763-489f-b7bb-90723c34226a)

After stopping the conflicting container, I successfully ran my custom image.

### Command to Run the Custom Image:
```bash
docker run -d -p 80:80 my-web-app
```

![Screenshot 2025-01-11 021657](https://github.com/user-attachments/assets/e447dbed-2b91-418b-9a59-5e1bef12fce9)

This created a live webpage based on the `my-web-app` image, serving the custom `index.html` file I had specified in the Dockerfile.

---

## Introduction to Elastic Beanstalk
**Elastic Beanstalk** is an AWS service that simplifies the deployment of cloud applications by abstracting the underlying infrastructure. It supports applications packaged as Docker containers, making it an ideal choice for deploying my custom web app.

### Key Features:
- Automatically provisions resources like EC2 instances.
- Manages scaling, load balancing, and health monitoring.
- Simplifies deployment with a few clicks.

![Screenshot 2025-01-13 030400](https://github.com/user-attachments/assets/ccfd0c0e-fd6a-4108-905e-3cba548b27f8)

---

## Deploying a Custom Image with Elastic Beanstalk
After building the custom Docker image, I deployed it to **AWS Elastic Beanstalk**. 

### Steps to Deploy:
1. Packaged the application as a Docker container.
2. Uploaded the container to Elastic Beanstalk.
3. Clicked "Deploy" to launch the application in the cloud.

![Screenshot 2025-01-11 031148](https://github.com/user-attachments/assets/6301b14f-8464-41cc-880e-a6b6424a37e3)

The deployment process was fast, taking approximately **5 minutes**.

### Benefits:
- Eliminated the need to manually manage infrastructure.
- Allowed me to focus on application development rather than server configuration.

---

## Deploying App Updates
To test the update process in Elastic Beanstalk, I redesigned my website by modifying the `index.html` file and adding an image. 

### Steps for Updating the App:
1. Edited the `index.html` file and tested it locally in Google Chrome.
2. Uploaded the updated files to Elastic Beanstalk by clicking **"Upload and Deploy"**.

![image](https://github.com/user-attachments/assets/6ba34244-6094-4a84-9b15-603855474695)

### Issue:
- Initially, the app updates did not reflect in the live environment because the original HTML file was still deployed.

### Solution:
- Re-deployed the application with the updated `index.html` file, which immediately reflected the changes in the live environment.

![Screenshot 2025-01-13 032105](https://github.com/user-attachments/assets/0ef617cf-4130-446a-8897-d4ea4da9ec9d)

---

## Summary
In this project, I successfully:
- Learned the fundamentals of **Docker** and **containers**.
- Created and ran a **custom Docker image** for a web application.
- Used **AWS Elastic Beanstalk** to deploy the application in the cloud.
- Tested and deployed app updates using Elastic Beanstalk's **upload and deploy** feature.

This project deepened my understanding of containerization, Docker, and cloud deployment with Elastic Beanstalk, equipping me with valuable skills for modern software development workflows.

---

## References
- [Docker Documentation](https://docs.docker.com/)
- [AWS Elastic Beanstalk Documentation](https://aws.amazon.com/elasticbeanstalk/)
- [Nginx Documentation](https://nginx.org/en/docs/)
