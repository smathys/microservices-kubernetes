# Microservices and Kubernetes

> My 50 Cents about microservices running in the cloud

Experiences made, working with Microservices and Kubernetes on AWS during one year

![title](assets/image/container.png)

---

## Intro - Rise of the Containers

<table>
<tr>
  <td><img src="assets/image/docker.png" width="150px"></td>
    <td>Docker</td>
</tr>

<tr>
  <td><img src="assets/image/compose.jpg" width="150px"></td>
    <td>Docker Compose</td>
</tr>

<tr>
  <td><img src="assets/image/swarm.png" width="150px"></td>
    <td>Docker Swarm</td>
</tr>
<tr>
  <td><img src="assets/image/kubernetes.png" width="150px"></td>
    <td>Kubernetes</td>
</tr>
<tr>
  <td><img src="assets/image/openshift.png" width="150px"> </td>
    <td>Openshift</td>
</tr>
</table>

---

## The Project

### www.abilio.ch

![Abilio](assets/image/abilio.png)

Note:
Siemens biete die Platform an um die Abilio App zu betreiben.
Fahrten von Passagieren werden anhand von Sensor-Daten berechnet und das günstigte Ticket ausgewählt und gekauft
+++

### Tech Stack

- Container Platform: Kubernetes Cluster on AWS Cloud
- Database: Cassandra Cluster on AWS Cloud
  Postgres on AWS Cloud
- Message Queue: Kafka Cluster on AWS Cloud
- App: Xamarin Mobile Apps mit gemeinsamen Mobile-SDK
- Microservices:

  - Java Spring Microservices
  - React Frontend "Cockpit"

- Tools Microservices:
  - Grafana
  - Kibana
  - Nginx as Gateway
  - Gitlab Pipelines

### Team

- Ops team in India
- Dev Team :
  - 1 Siemens Ops Team Coordinator
  - 6 backend developers Noser Engineering
  - 2 frontend developers Noser Engineering
  - 3 Mobile developers Noser Engineering
  - 2 Hardware developers Siemens
  - 1 PO Siemens
  - 1 Project/Team Manager / Tech Lead Noser Engineering
  - 1 mathematician Siemens Munich

---

## Working with Kubernetes and Microservices

![Microservices](assets/image/microservices.jpg)

### Cluster

- 3 Environments: dev, staging, prod
- dev & staging AWS Ireland
- prod AWS Frankfurt, no access rights for developers
- multi tenancy with namespaces in clusters
- access via identity file and ssh
- Tools
  - Grafana
  - Kibana
  - Cockpit

+++

#### Setup/Organisation of Microservices

- 1 git repo per service
- corresponding config files in config-repo
- cassandra keyspace per service per client
- kafka topics per event-stream and client

+++

#### Working on Microservices

- small code repos
- read kafka topic, process message, calculate, store in db, rest-controller
- serialize / deserialze json

+++

#### Development on Microservices

- Java & kotlin mixed
- Spring Boot Jars
- 1 Parent Pom for managing Spring Boot Version
- Support Libs as abstraction for Cassandra, Kafka, Http

+++

#### Testing on a Microservices

- Portforwarding for local development, Dev cluster used heavenly by developers
- automated API Tests with Postman/
- replay of old journeys from staging or prod

+++

#### Tools used for Development

- docker-compose
- postman
- ssh portforwarding
- bash script/ tools provided by cassandra & kafka

---

## The Pro's

- focus on small functions
- independent deployment of releases
- docker-image run everywhere, deployment of release means config uses new version of docker-image
- zero downtime deployment
- usage of Kafka:
  - dead-letter-que
  - mesarue metrics on kafka-queues

---

## The Cons's

- config files hell
- dependencies on deployment
- losing overview of services and their version
- complex management of requirements which apply for multi microservices
- manually connection services via config
- backend had to fix app-bugs because of more frequent release cycles
- handling of multi tenancy was introduced after first releases

---

## Wrap Up

- use managed Kubernetes
- think about multi tenancy
- bleeding edge is not always fun (spring-data cassandra release was to late)
- think about when / how remove old microservices

+++
