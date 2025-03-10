# Jenkins Pipeline for Java based application using Maven, SonarQube, Argo CD, Helm and Kubernetes

![Screenshot 2023-03-28 at 9 38 09 PM](https://user-images.githubusercontent.com/43399466/228301952-abc02ca2-9942-4a67-8293-f76647b6f9d8.png)



# CI/CD Pipeline with Jenkins, SonarQube, Docker, and ArgoCD

This project implements a complete CI/CD pipeline using Jenkins, Maven, SonarQube, Docker, and ArgoCD to automate the build, test, security scanning, and deployment process for containerized applications.
This Project is inspired from [Abhishek Veermalla](https://github.com/iam-veeramalla).

## **Pipeline Overview**
The pipeline follows these steps:

1. **Code Commit:** Developers push code to a Git repository.
2. **Webhook Trigger:** A webhook triggers Jenkins to start the pipeline.
3. **Build Process:** Jenkins uses Maven to build the project.
4. **Code Quality Analysis:** SonarQube analyzes the code for security vulnerabilities and code quality.
   - If issues are found, the pipeline stops, and a report is sent to Slack and email.
   - If the code passes the quality check, the pipeline proceeds.
5. **Testing:** Automated tests are executed.
   - If tests fail, the pipeline stops.
   - If tests pass, the pipeline proceeds.
6. **Docker Image Creation & Push:** The application is containerized using Docker and pushed to Docker Hub.
7. **Kubernetes Deployment:** 
   - Used Shell Script to update the manifest folder with the new image.
   - ArgoCD detects changes and deploys the updated application to Kubernetes.

---

## **Technology Stack**
- **Jenkins**: Automates the build and CI/CD process.
- **Maven**: Manages project dependencies and builds the application.
- **SonarQube**: Performs static code analysis and security scanning.
- **Docker**: Containers the application for deployment.
- **Docker Hub**: Stores the built container images.
- **ArgoCD**: Automates Kubernetes application deployments.
- **Slack & Email Notifications**: Notifies teams of build failures.

---

## **Pipeline Flow**
1. **Jenkins Build Trigger**
   - A webhook triggers Jenkins when code is pushed.

2. **Build & Code Analysis**
   - Jenkins runs Maven to build the application.
   - SonarQube checks code quality and security.
   - If code quality fails, a report is sent via Slack and email.

3. **Testing Phase**
   - If code quality passes, tests are executed.
   - If tests fail, the pipeline stops.

4. **Docker Image Creation & Push**
   - If tests pass, the application is containerized using Docker.
   - The Docker image is pushed to Docker Hub.

5. **ArgoCD Deployment**
   - I have replaced the image updater with `Shell Script` which I have included in JenkinsFile which will update the Kubernetes manifests in a separate repository(in my case I have created a separate folder in the same repo).
   - ArgoCD detects the changes and deploys the updated application.

---

## **Installation & Setup**
### **1. Jenkins Setup**
- Install Jenkins and required plugins (`Pipeline`, `Maven`, `Docker Pipeline`, `SonarQube Scanner`).
- Configure Jenkins to use a webhook for Git repository triggers.

### **2. SonarQube Setup**
- Install and configure SonarQube.
- Connect SonarQube with Jenkins using the `SonarQube Scanner` plugin.

### **3. Docker & Docker Hub**
- Install Docker on the Jenkins server.
- Authenticate with Docker Hub to push images.

### **4. ArgoCD Setup**
- Install ArgoCD in your Kubernetes cluster.
- Connect ArgoCD with the manifests repository.

---

## **Notifications**
- If the pipeline fails at SonarQube or testing, a report is sent via Slack and email.
- Notifications include build status and failure reasons.

---

## **Conclusion**
This CI/CD pipeline automates the complete software development lifecycle, ensuring efficient code quality checks, security scanning, and automated deployments using modern DevOps tools. 🚀
