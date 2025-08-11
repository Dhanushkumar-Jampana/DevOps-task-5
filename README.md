# DevOps Task 5 – Kubernetes with Minikube

## Objective
Deploy and manage an application in Kubernetes using Minikube, kubectl, and Docker.

## Steps Performed

### 1. Installed Minikube & kubectl
Installed using Chocolatey:
```powershell
choco install minikube
choco install kubernetes-cli
2. Started Minikube Cluster
minikube start --driver=docker
kubectl get nodes
3. Created Deployment
deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp-container
          image: nginx:latest
          ports:
            - containerPort: 80
Apply
kubectl apply -f deployment.yaml

4. Created Service
service.yaml

apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort
Applied:
kubectl apply -f service.yaml

5. Accessed Application

minikube service myapp-service
Opened the URL in a browser and saw the nginx welcome page.

6. Scaled the Deployment

kubectl scale deployment myapp-deployment --replicas=4
kubectl get pods

7. Verified Logs & Descriptions

kubectl logs <pod-name>
kubectl describe pod <pod-name>
Screenshots

Pods list

Services list

nginx home page


Outcome
Learned Kubernetes basics: deployments, services, scaling.

Successfully deployed and accessed an application locally with Minikube.
