
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

[Kotigo examples are here](https://github.com/kiegroup/kogito-examples), and the getting started is simple and illustrative. 

### Getting started code

The first application is the [process-quarkus-example]() with a copy of the code in this repository. I did some changes to it.
The top level BPMN process is orders.bpmn2. The Add items subprocess invokes the following orderItems.bpmn2 process, which uses a CalculationService.calculateTotal custom Java service and a user task to verify the order.

It can run with `quarkus:dev` and any change to the models generate and code is available. REST end points are generated for each process start point and decision service defined in the app.

Calling the POST on /orders with a JSON oder doc, creates a process instance, and a unique UUID for the order for future reference.

### Creating my own project

```
mvn archetype:generate \
    -DarchetypeGroupId=org.kie.kogito \
    -DarchetypeArtifactId=kogito-quarkus-archetype \
    -DgroupId=jbcodeforce -DartifactId=sample-kogito \
    -DarchetypeVersion=0.14.0 \
    -Dversion=1.0-SNAPSHOT
```
The Quarkus extension and Maven plug-in within a standard Kogito project generate all the required code and boilerplate for your Kogito services. The generated service usually exposes default REST endpoints using the information that is inferred from the business assets that you include in your project. See [detail here](https://docs.jboss.org/kogito/release/latest/html_single/#proc-kogito-creating-project-custom_kogito-creating-running).

### Other samples

The second very interesting sample is for knative

one is kakfa - quarkus and kogito example.

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