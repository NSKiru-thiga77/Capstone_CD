# deployment-repo
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mypod
  labels:
    app: mypod
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mypod
  template:
    metadata:
      labels:
        app: mypod
    spec:
      containers:
        - name: cont1
          image: 820171507408.dkr.ecr.us-east-1.amazonaws.com/myecr-reop:latest
          imagePullPolicy: IfNotPresent                                             
          ports:
            - containerPort: 80
          resources:
            requests:
              cpu: "100m"
              memory: "128Mi"
            limits:
              cpu: "500m"
              memory: "256Mi"
          env:
            - name: ENV
              value: "dev"

```
# Continuous Deployment Workflow
1.Developer pushes code to the application repository.
2.Jenkins pipeline builds and scans the application.
3.Docker image is pushed to Docker Hub/AWS ECR.
4.Jenkins updates image tags in Kubernetes manifests.
5.Changes are committed to the GitOps repository.
6.Argo CD detects repository changes.
7.Argo CD synchronizes manifests with Amazon EKS.
8.Kubernetes performs rolling deployment.
9.Updated application becomes available automatically.

# Kubernetes Resources
# Deployment

The Deployment resource manages application pods and ensures the desired number of replicas are running.
# Apply deployment:

kubectl apply -f deployment.yaml

# Verify deployment:

kubectl get deployments
kubectl get pods

# Service

The Service resource exposes the application inside the Kubernetes cluster.
# Apply service:

kubectl apply -f service.yaml

# Verify:

kubectl get svc
