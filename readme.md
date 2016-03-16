# REST based micro-services sample - using Kubernetes

You have already seen this application in the PaaS lecture.
In this Lab we weill deploy it on a Kubernetes cluster using kubectl

## Running Instructions
- Before deploying the appliction containers you will need to deploy the databases
- First make sure you are using your group namespace to deploy:
  $ kubectl config set-context aws_kubernetes --namespace=group1
- Then deploy the MongoDB service and pod:
  $ kubectl create -f mongo_svc.yml
  $ kubectl create -f mysql_pod.yml

## Lab Instructions

Please follow the detailed lab instructons on [OLAT](https://olat.zhaw.ch/auth/RepositoryEntry/196968466/CourseNode/74113252610159/path%3D~~03%20Labs/0).

Here are just some quick information pointers:

- Docker images:
  - User Interface:  icclabcna/customers-stores-ui:latest
  - Store REST Microservice: icclabcna/rest-microservices-store:latest
  - Customers REST Microservice: icclabcna/rest-microservices-customers:latest

- User Interface Docker container:
  - Runs on port: 9900
  - ENVIRONMENT VARIABLES:
    - zuul_routes_customers_url: URL to which Zuul forwards Customers services requests e.g., http://localhost:9000
    - zuul_routes_stores_url: URL to which Zuul forwards Stores services requests e.g., http://localhost:8081

- Stores REST Microservice Docker container:
  - Runs on port: 8081
  - ENVIRONMENT VARIABLES:
    - SPRING_DATA_MONGODB_URI: JDBC Endpoint URI for MongoDB e.g., mongodb://localhost:27017/stores

- Customers REST Microservice Docker container:
  - Runs on port: 9000
  - ENVIRONMENT VARIABLES:
    - spring_datasource_username: e.g., root
    - spring_datasource_password: e.g., yourpassword
    - spring_datasource_url: JDBC Endpoint URI for MySQL DB e.g., jdbc:mysql://localhost:3306/customers
    - integration_stores_uri: URI the Customers service uses to connect to the Stores service e.g., http://stores:8081
