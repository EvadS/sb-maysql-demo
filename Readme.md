
## Requirements for running app
### Data base
Before the Spring Boot application can interact with the database, the specified database must exist
```mysql script
CREATE DATABASE your_database_name;
```
### environments variables to start
* ${DB_USERNAME}
* ${DB_PASSWORD}
* ${DB_NAME}


## build project
```
./mvnw clean install -DskipTests
```

## Crud operation
### get all users
```bash
    curl http://localhost:8080/api/users
```

### create user
```bash
curl --location 'http://localhost:8080/api/users' \
--header 'Content-Type: application/json' \
--data-raw '{
    "firstName": "first2 name",
    "lastName": "last name",
    "email":"mail@mail.com"
}'
```

## working with k8s
```
https://benstitou-anas.medium.com/deploy-java-spring-application-with-mysql-db-on-kubernetes-1e456271c6a1
```

## Dockers instructions

### создаем образ

```bash
    docker build . -t evaddev/sb-mysql-users:latest -t evaddev/sb-mysql-users:1.0.0
```

### проверяем
```
    docker images | grep sb-mysql-users
```

Push the Docker Image to a Registry
репозиторий должен быть создан  docker hub
```bash
    docker push evaddev/sb-mysql-users --all-tags
```

```
 minikube status
```

```
minikube start
```
go k8s folder on project directory
```
   cd k8s
```

deploy your configmap:
```bash
    kubectl apply -f mysql-configmap.yaml
```

```bash
 kubectl apply -f .\secrets.yaml
```

```bash
 kubectl apply -f mysql-deployment.yaml
```

 ### validate
```bash
  kubectl get all
```

### check mysql
````bash
  kubectl exec -it deploy/demo-app-mysql -- /bin/bash
```

  ```bash
  mysql --user=$MYSQL_USER --password=$MYSQL_PASSWORD
  ```

```bash
   select CURRENT_DATE()
```

```
 minikube tunnel
```

### развернуть deployment
```
    kubectl apply -f .\app-deployment.yaml
```

### проверяем работо способность
```bash
 kubectl logs pod/[POD_NAME]
```

### Очиcтка
 ```bash
    kubectl delete deploy [NAME]
    kubectl delete  [SERVICE_NAME]
    kubectl delete secrets  [SECRETS_NAME]
 ```


пример на момент запуска
kubectl delete deploy demo-app-mysql
kubectl delete deploy demo-app-spring

kubectl delete  service/demo-app-mysql
kubectl delete  service/demo-app-spring
kubectl delete secrets mysql-pass

затем становить
minikube stop

осовбодить место
minikube delete




