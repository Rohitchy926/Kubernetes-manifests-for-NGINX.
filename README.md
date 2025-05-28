# Kubernetes-manifests-for-NGINX.
## step-1 after installation of kubectl / after creation of cluster.

curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.30.2/2024-07-12/bin/linux/amd64/kubectl

chmod +x kubectl

mv kubectl /usr/local/bin/kubectl

## step-2: Create a nginx.yml file and yml file for nginx using command - vi nginx.yml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80

## step 3- Run the command for creating a deplyoment from a file
 ( kubectl create -f nginx.yml)
## step 4- check the deplyoment is created or not by using -
kubectl get deployments

## step-4 check the service by 
 kubectl get svc nginx-service 
<img width="1298" alt="image" src="https://github.com/user-attachments/assets/0a6b18c5-bbb8-449f-b5cd-7f25f48225ae" />

## step 5- take the external ip and paste it to chrome 
<img width="1161" alt="image" src="https://github.com/user-attachments/assets/818d8585-628e-4b44-b69d-db78c8b31518" />



