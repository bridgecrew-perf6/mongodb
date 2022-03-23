In this Subject, 

1. Deploy MongoDB Express using same Database with local

I will deploy local mongodb on Centos 8
Then I will deploy MongoDB Express using same Database with local MongoDB
Deploy Configmap for MongoDB Express to perform this purpose

kubectl apply -f mongo.yaml
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo-service.yaml
kubectl apply -f mongo-express.yaml
kubectl apply -f mongo-express-service.yaml
kubectl apply -f mongo-configmap.yaml
kubectl apply -f ingress.yaml

2. Deploy Ingress to point a DNS to the MongoDB

--for the ingress.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: mongo-express-ingress
spec:
  rules:
    - host: mongo-express.com -> You can test by creating a DNS name in HOST file
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: mongo-express-service
                port:
                  number: 8081
