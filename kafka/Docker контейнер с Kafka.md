### на основе статьи - https://habr.com/ru/articles/738874/

Для kafka и zookeeper
```yml
version: "3.9"  
services:  
  zookeeper:  
    image: confluentinc/cp-zookeeper:latest  
    environment:  
      ZOOKEEPER_CLIENT_PORT: 2181  
      ZOOKEEPER_TICK_TIME: 2000  
    ports:  
      - 22181:2181  
  
  kafka:  
    image: confluentinc/cp-kafka:latest  
    depends_on:  
      - zookeeper  
    ports:  
      - 9092:9092  
    hostname: kafka  
    environment:  
      KAFKA_BROKER_ID: 1  
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181  
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092  
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT  
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT  
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 2
```
![[Pasted image 20240512104113.png]]
Настройка для 1 сервиса
```yml
producer:  
  build:  
    context: producer  
    dockerfile: ./Dockerfile  
  ports:  
    - 8080:8080
```
* contex - путь до директории с сервисом
Dockerfile
```Dockerfile
FROM openjdk:17-jdk-slim  
LABEL authors="Основной"  
COPY build/libs/data-generator-microservice-0.0.1-SNAPSHOT.jar /opt/service.jar  
EXPOSE 8080  
CMD exec java -jar /opt/service.jar
```
* COPY - скопировать jar файл
* CMD exec java -jar /opt/service.jar - выполнить его в контейнере