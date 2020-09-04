
# Kogito Studies

## What 

[Kogito](https://kogito.kie.org/) is a cloud native business automation based on latest technology stack like quarkus and knative

* focus on business domain
* developer centric to address complex business logic like
    * stateful long running process 
    * stateful state machine
    * decision service and logic
    * constraint programming
    * Based on standard: BPMN 2.0, DMN
    * Support standards like: reactive messaging for microprofile, cloudevent

[Product documentation](https://docs.jboss.org/kogito/release/latest/html_single). 

Base docker image is: quay.io/kiegroup/kogito-quarkus-ubi8

[Online Editor to do BPMN or DMN model](https://kiegroup.github.io/kogito-online)

## Kogito operator

To deploy on OpenShift, Kogito offers an operator and CLI to build and deploy app.

## Code studies

[Kotigo examples are here](), and the getting started is simple and illustrative. The first very interesting one is kakfa - quarkus and kogito example.

Simple Dockerfile for a quarkus native app:

```dockerfile
FROM quay.io/kiegroup/kogito-quarkus-ubi8
COPY target/*-runner /home/kotigo/bin
```

### Kafka Kogito examples 

* [Process with Kafka](https://github.com/kiegroup/kogito-examples/tree/master/process-kafka-quickstart-quarkus)
    * consuming events from a Kafka topic and for each event start new process instance
    * each process instance is expecting a traveller information in JSON format
    * traveller is then processed by rules 
* [Process with Knative Eventing]() to demonstrate:
    * consuming events from a Knative Eventing broker and for each event start new process instance
    * each process instance is expecting a traveller information in JSON format
    * traveller is then processed by rules