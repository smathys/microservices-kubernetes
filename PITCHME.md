# Microservices and Kubernetes

![title](assets/image/container.png)

+++
> My 50 Cents about microservices running in the cloud

Experiences made, working with Microservices and Kubernetes on AWS during one year

---

## Intro - Rise of the Containers

<table>
<tr>
  <td><img src="assets/image/docker.png" width="100px"></td>
    <td>Docker</td>
</tr>

<tr>
  <td><img src="assets/image/compose.jpg" width="100px"></td>
    <td>Docker Compose</td>
</tr>
</table>

+++

<table>
<tr>
  <td><img src="assets/image/swarm.png" width="100px"></td>
    <td>Docker Swarm</td>
</tr>
<tr>
  <td><img src="assets/image/kubernetes.png" width="100px"></td>
    <td>Kubernetes</td>
</tr>
<tr>
  <td><img src="assets/image/openshift.png" width="100px"> </td>
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
- Database:
  - Cassandra Cluster on AWS Cloud
  - Postgres on AWS Cloud
- Message Queue: Kafka Cluster on AWS Cloud
- App: Xamarin Mobile Apps mit gemeinsamen Mobile-SDK

+++

- Microservices Languages:

  - Java Spring Microservices
  - React Frontend "Cockpit"
  - Python PDF processing

+++

- Tools Microservices:
  - Grafana
  - Kibana
  - Nginx as Gateway
  - Gitlab Pipelines
  
+++
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

+++

### Cluster

- 3 Environments: dev, staging, prod
- Dev & staging AWS Ireland
- Prod AWS Frankfurt, no access rights for developers
- Multi tenancy with namespaces in clusters
- Access via identity file and ssh
- Tools
  - Grafana
  - Kibana
  - Cockpit

+++

### Setup/Organisation of Microservices

- 1 git repo per service
- Corresponding config files in config-repo
- Cassandra keyspace per service per client
- Kafka topics per event-stream and client

+++

### Working on Microservices

- Small code repos
- Tasks:
  - Read kafka topic
  - Process message
  - Calculate
  - Store in db
  - Write to kafka topic
  - Rest-controller
- Serialize / Deserialze json

+++

### Development on Microservices

- Java & kotlin mixed
- Spring Boot Jars
- 1 Parent Pom for managing Spring Boot Version
- Support Libs as abstraction for Cassandra, Kafka, Http

+++

### Testing on a Microservices

- Portforwarding for local development, Dev cluster used heavenly by developers
- Automated API Tests for each Service with Postman
- Replay of old journeys from staging or prod
- Fake model train in office which drive one S-Bahn line all day long

+++

### Tools used for Development

- Docker-compose
- Postman
- Ssh portforwarding
- Bash script/ tools provided by cassandra & kafka

---

## The Pro's

- Focus on small functions
- Independent deployment of releases
- Docker-image run everywhere, deployment of release means config uses new version of docker-image
- Zero downtime deployment
- Usage of Kafka:
  - dead-letter-que
  - mesarue metrics on kafka-queues

---

## The Cons's

- Config files hell
- Dependencies on deployment
- Maven transitive clashing dependencies
- Losing overview of services and their version
- Complex management of requirements which apply for multi microservices
- Manually connection services via config
- Backend had to fix app-bugs because of more frequent release cycles
- Handling of multi tenancy was introduced after first releases

---

## Wrap Up

- Use managed Kubernetes
- Think about multi tenancy
- Bleeding edge is not always fun (spring-data cassandra release was to late)
- Think about when / how remove old microservices

