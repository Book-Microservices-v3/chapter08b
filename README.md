# Learn Microservices with Spring Boot 3 - Chapter 8 - 2/4
This repository contains the source code of the practical use case described in the book [Learn Microservices with Spring Boot 3 (3rd Edition)](https://link.springer.com/book/10.1007/978-1-4842-9757-5).
The book follows a pragmatic approach to building a Microservice Architecture. You start with a small monolith and examine the pros and cons that come with a move to microservices.

## Chapter 8 version 2/4

The Chapter 8's source code is divided into four parts for a better understanding of how the system evolves when we start introducing _Common Patterns in Microservice Architectures_.

In this second part, we introduce Service Discovery and Load Balancing, supported by the microservices' health checks. These patterns allow us to scale up our system, and to make it more resilient.

![Logical View - Chapter 8 2/4](resources/microservice_patterns-GW-SD-View-2.png)

The main concepts included in this first part of the chapter are:

* Why do we need Service Discovery, a Load Balancer and a Health endpoint? The problems, explained.
* Basic concepts: Client-Side vs. Server-Side Discovery, Load Balancers, the Service Registry, detecting unhealthy instances, etc.
* Spring Cloud integrations: Spring Cloud Consul, Spring Cloud Actuator, Spring Cloud Load Balancer.
* Retry patterns and resilience using the Service Registry.
* Verifying how the system keeps working under chaos.

As usual, the book follows a hands-on approach, so you learn everything based on this microservice case study.

## Running the app

Requirements:

* JDK 17
* Node.js v18.16.0
* npm 9.7.1
* RabbitMQ 3.12.2
* Consul 1.16.0

1. You need a RabbitMQ server running. Run the server according to the instructions for your OS, for example:
    ```bash
    $ rabbitmq-server
    ```
1. You also need Consul up and running (in development mode). Follow the instructions for your OS, for example:
    ```bash
    $ consul agent -node=learnmicro -dev
    ```
1. To start the Multiplication microservice, you can use the command line with the included Maven wrapper:
    ```bash
    multiplication$ ./mvnw spring-boot:run
    ```
2. To start the Gamification microservice, you do the same from its corresponding folder:
    ```bash
    gamification$ ./mvnw spring-boot:run
    ```
3. To start the Gateway microservice, you do the same from its corresponding folder:
    ```bash
    gateway$ ./mvnw spring-boot:run
    ```
2. The React application can be started with npm. First, you need to download the dependencies with:
    ```bash
    challenges-frontend$ npm install
    ```
3. Then, you start the server with:
    ```bash
    challenges-frontend$ npm start
    ```

> **_Note:_**
> 
> In the [final version of our code](https://github.com/Book-Microservices-v3/chapter08d), we use Docker to start our complete system easily. However, it's not yet introduced at this point in the book, so we're starting all these components manually.

Once the backend and the fronted are started, you can navigate to `http://localhost:3000` in your browser and start resolving multiplication challenges.

## Retrieving health status using the Actuator Endpoint
Run the following command from your terminal or command line window: 

```bash
$ http :8080/actuator/health
```

## Requesting list of registered services using the Consul API
Open terminal or command line window in your system and type the following command: 
```bash
$ http -b :8500/v1/agent/services
```
## More advanced scenarios

Starting with this version, you can try some interesting scenarios. For example, you can start a second instance of both the Multiplication and Gamification microservices, and then start killing some of these application processes. You'll see how Consul detects these failing services, and also how the Retry pattern in the Gateway makes everything work under failures.

To start a second instance of a microservice, you can use for example:

```bash
multiplication$ ./mvnw spring-boot:run -Dspring-boot.run.arguments="--server.port=9080"
```

To kill an instance, you can use `kill -9` for example, followed by the process id of the Java application (that you can find also in the Spring Boot app logs).

## Questions

* Do you have questions about how to make this application work?
* Did you get the book and have questions about any concept explained within this chapter?
* Have you found issues using updated dependencies?

Don't hesitate to create an issue in this repository and post your question/problem there. 

## Purchase
You can buy the book online from these stores:
* [Apress](https://link.springer.com/book/10.1007/978-1-4842-9757-5)
* [Amazon](https://www.amazon.com/Learn-Microservices-Spring-Boot-Containerization/dp/1484297563)
and other online stores.
