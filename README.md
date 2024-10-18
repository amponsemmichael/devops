
## Project Overview
This lab focuses on understanding container orchestration using **Kubernetes** by setting up a Kubernetes cluster, deploying a simple Java application, and exploring various Kubernetes components and features like pods, deployments, services, and load balancing.

## Lab Objectives
- **Set up a Kubernetes cluster**: Use Minikube (local) or a cloud-based Kubernetes service (e.g., GKE, AKS, EKS).
- **Deploy a simple Java application**: Create a Kubernetes deployment and service to run a Java-based application.
- **Explore Kubernetes concepts**: Work with key components like pods, deployments, services, and replication controllers.
- **Implement load balancing**: Distribute traffic across multiple application instances using Kubernetes.

## Prerequisites
- Basic knowledge of Docker containers.
- Installed Docker and Minikube or access to a cloud-based Kubernetes service.
- Java application packaged in a Docker image.

## Project Structure
```
.
├── kubernetes
│   ├── deployment.yaml   # Kubernetes deployment configuration
│   ├── service.yaml      # Kubernetes service configuration for the Java app
│   └── other-k8s-files   # Other potential Kubernetes config files (if needed)
├── src                   # Source code of the Java application (optional)
└── README.md             # Documentation
```

## Steps to Complete the Lab

### 1. Set up a Kubernetes Cluster
- **Minikube**: If you are using a local environment:
  1. Install Minikube [installation guide](https://minikube.sigs.k8s.io/docs/start/).
  2. Start Minikube with:  
     ```bash
     minikube start
     ```
- **Cloud-Based Kubernetes Service**: If you're using a cloud provider like GKE, AKS, or EKS, set up your cluster following the respective service documentation.

### 2. Create Docker Image for Java Application
1. Write a simple Java application or use a pre-built one.
2. Create a `Dockerfile` to containerize the application:
   ```Dockerfile
   FROM openjdk:11-jre-slim
   COPY target/my-java-app.jar /app/my-java-app.jar
   CMD ["java", "-jar", "/app/my-java-app.jar"]
   ```
3. Build the Docker image:
   ```bash
   docker build -t my-java-app .
   ```
4. Push the image to DockerHub or another container registry:
   ```bash
   docker tag my-java-app <your-dockerhub-username>/my-java-app
   docker push <your-dockerhub-username>/my-java-app
   ```

### 3. Deploy Java Application on Kubernetes
1. **Deployment Configuration** (`deployment.yaml`):
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: java-app-deployment
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: java-app
     template:
       metadata:
         labels:
           app: java-app
       spec:
         containers:
         - name: java-app
           image: <your-dockerhub-username>/my-java-app:latest
           ports:
           - containerPort: 8080
   ```
2. **Service Configuration** (`service.yaml`):
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: java-app-service
   spec:
     selector:
       app: java-app
     ports:
       - protocol: TCP
         port: 80
         targetPort: 8080
     type: LoadBalancer
   ```
3. Apply configurations:
   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

### 4. Verify the Deployment
- **Pods**: Check the running pods:
  ```bash
  kubectl get pods
  ```
- **Services**: Verify that the service has been created and is running:
  ```bash
  kubectl get services
  ```

### 5. Load Balancing
Once the service is up, Kubernetes will automatically distribute incoming traffic across the available replicas of the Java application.

### 6. Explore Kubernetes Concepts
- **Pods**: The smallest deployable unit in Kubernetes.
- **Deployments**: Manage a set of identical pods, ensuring they are up and running.
- **Services**: Expose your application to external traffic.
- **Replication Controller**: Ensures a specified number of pod replicas are running at all times.

### References
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [Minikube Documentation](https://minikube.sigs.k8s.io/docs/)
- [DockerHub](https://hub.docker.com/)

---
