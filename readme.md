=>What’s Included

Dockerfile: Instructions to create a Docker image for the Flask app.
flask-app/: Contains the code for the Flask application.
k8s/: Kubernetes configuration files.
flask-ingress.yaml: Sets up routing for the Flask app.
flask-service.yaml: Exposes the Flask app to the network.

=>What You Need

Docker: To build and manage containers.
Minikube: To run a local Kubernetes cluster.
kubectl: To interact with your Kubernetes cluster.

=>How to Get Started

1. Build and Push Docker Image
Build the Docker Image

bash
Copy code
docker build -t your-dockerhub-username/flask-mongodb-app:latest .
Push the Image to Docker Hub

bash
Copy code
docker push your-dockerhub-username/flask-mongodb-app:latest

2. Start Minikube
bash
Copy code
minikube start

3. Deploy the App
Apply the Flask Service Configuration

bash
Copy code
kubectl apply -f k8s/flask-service.yaml
Apply the Ingress Configuration

bash
Copy code
kubectl apply -f k8s/flask-ingress.yaml

4. Access the App
Get the URL to Access the Service

bash
Copy code
minikube service flask-service --url
This command will provide a URL you can use to access your Flask app from your browser.

Troubleshooting
Can't Access the App: Make sure Minikube is running and ports are correctly exposed.
Ingress Issues: If you’re using Ingress, ensure it’s set up correctly and running.

=>DNS Resolution in Kubernetes

Within a Kubernetes cluster, DNS resolution allows pods to communicate with each other using service names rather than IP addresses. 
Each service in the cluster gets a DNS entry managed by the Kubernetes DNS system, which translates service names into their corresponding cluster IP addresses. 
This makes inter-pod communication seamless and reliable.

=>Resource Requests and Limits

Resource requests and limits are used in Kubernetes to manage pod resource allocation and ensure that no single application consumes all available resources.
For example, you can specify CPU and memory requests to guarantee a minimum allocation, while limits prevent the application from using more than a specified maximum. 
This approach helps maintain cluster stability and ensures that resources are fairly distributed among running applications.

=>Design Choices

Configurations and Setups: I chose to use Minikube for local testing and Kubernetes for deployment due to its scalability and ease of use. 
Minikube provides an excellent environment to simulate production scenarios without the need for a full-scale cloud setup.

Alternatives Considered: I considered using Docker Compose instead of Kubernetes; however, Kubernetes offers better scalability, resource management, 
and supports Ingress controllers, which makes it more suitable for production-like environments.

=>Testing Scenarios

Autoscaling: I tested autoscaling by applying a Horizontal Pod Autoscaler (HPA) configuration and simulating high traffic loads. 
The application scaled up as expected during high load and scaled down during idle periods, effectively managing resource consumption.

Database Interactions: Tested database interactions by sending multiple GET and POST requests to ensure data consistency and response times under load.
The application performed well, with minimal delays observed.

Testing Results: Autoscaling worked without issues, but during the highest load, response times slightly increased. 
Database interactions remained consistent, demonstrating the robustness of MongoDB under simulated high traf
