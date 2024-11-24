# Project Setup

## Prerequisites
- Java 17
- Maven
- Docker
- Kubernetes CLI (kubectl)

## Build the Project

To build the project, run the following command:

```sh
mvn clean package
```

## Build the Docker Image

To build the Docker image, use the following command:
```sh
docker build -t producer:latest .
```

## Deploy to Kubernetes

To deploy the application to Kubernetes, apply the following configurations:

### RabbitMQ
```sh
./rabbit-mq/start.sh 
kubectl apply -f kubernetes/rabbit-mq/deployment.yaml
kubectl apply -f kubernetes/rabbit-mq/service.yaml
```

### Producer
```sh
kubectl apply -f kubernetes/producer/deployment.yaml
kubectl apply -f kubernetes/producer/service.yaml
```

## View logs
```sh
kubectl get pods | grep producer
```

```sh
kubectl logs -f <pod-name>
```

## Test the Application
It is recommended to use Postman to execute the request.
```sh
curl --location --request POST 'localhost:8080/produce?message=Lima'
```

## Clean up
```sh
kubectl delete -f kubernetes/producer/deployment.yaml
kubectl delete -f kubernetes/producer/service.yaml
```

```sh
kubectl delete -f kubernetes/rabbit-mq/deployment.yaml
kubectl delete -f kubernetes/rabbit-mq/service.yaml
```

# Delete the Docker Image
```sh
docker rmi producer:latest
```