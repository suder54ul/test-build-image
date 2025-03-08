# test-build-image
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-python-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-python-app
  template:
    metadata:
      labels:
        app: my-python-app
    spec:
      containers:
      - name: mypythondockerrepo
        image: myacrrepo421.azurecr.io/akannan1087/mypythondockerrepo:#{Build.BuildId}#
        ports:
        - containerPort: 5000
# service type loadbalancer       
---
apiVersion: v1
kind: Service
metadata:
  name: my-python-app-svc
spec:
  selector:
    app: my-python-app
  ports:
    - protocol: TCP
      port: 5000
      targetPort: 5000
  type: LoadBalancer
