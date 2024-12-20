# Deploy MongoDB and Mongo Express into local Kubernetes cluster 

This project demonstrates deploying **MongoDB** and **Mongo Express** to a local Kubernetes cluster using Minikube. It includes configurations for managing sensitive credentials via Kubernetes Secrets and externalizing connection details using ConfigMaps.

## Project Overview
- Deploy a local Kubernetes cluster using **Minikube**.
- Set up **MongoDB** for database management.
- Set up **Mongo Express** for a web-based database management interface.
- Utilize **Secrets** for secure credentials storage and **ConfigMaps** for configuration management.

## Prerequisites
- Minikube installed on your system.
- Basic understanding of Kubernetes concepts such as Deployments, Services, Secrets, and ConfigMaps.

## Steps to Deploy MongoDB and Mongo Express

### 1. Set Up Minikube
1. Install Minikube. 
Start Minikube with Docker as the driver:
minikube start --driver=docker
Verify Minikube status:
minikube status
Note: kubectl is installed as a dependency during Minikube installation.

### 2. Deploy MongoDB
Create a Secret for the MongoDB username and password.
Deploy MongoDB using a Kubernetes Deployment. The credentials will be sourced from the created Secret.
Expose MongoDB via an internal ClusterIP Service.

### 3. Deploy Mongo Express
Create a ConfigMap to store MongoDB connection details.
Deploy Mongo Express as a Kubernetes Deployment, using:
Secrets for the MongoDB username and password.
ConfigMap for the MongoDB service URL.
Expose Mongo Express via an external LoadBalancer Service.

### 4. Access Mongo Express
Since Minikube does not support external LoadBalancers, run the following to assign an accessible IP:
minikube service mongo-express-service
This will display a URL (e.g., http://192.168.49.2:30000) to access the Mongo Express web interface.

**Deployment Files:**
The following YAML files are included in the project:
- mongodb-secret.yaml - Stores MongoDB credentials as a Secret.
- mongodb.yaml - Defines MongoDB Deployment and Service.
- mongodb-configmap.yaml - Stores MongoDB service URL as a ConfigMap.
- mongoexpress.yaml - Defines Mongo Express Deployment and Service.

Additional Notes: 
The mongo-root-username and mongo-root-password are base64-encoded in the Secret. Use the following commands to encode your credentials:
echo -n 'username' | base64
echo -n 'password' | base64

When running on Minikube, the Mongo Express service URL will display <pending> as the external IP. Use the minikube service command to tunnel access.

**Conclusion:**
This setup provides a quick and secure way to deploy MongoDB and Mongo Express in a local Kubernetes cluster using Minikube. The combination of Secrets and ConfigMaps ensures secure and modular configuration management.
