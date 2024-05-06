### На основе статьи - https://habr.com/ru/companies/otus/articles/506788/

# Настройка зависимостей для Flyway
Maven
```
<plugin>
		<groupId>org.flywaydb</groupId>
		<artifactId>flyway-maven-plugin</artifactId>
		<version>4.0.3</version>
</plugin>
```
Gradle 
```
// https://mvnrepository.com/artifact/org.flywaydb/flyway-maven-plugin
implementation 'org.flywaydb:flyway-core'
```
К нему обязательно нужен JPA
```
<!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-entitymanager -->
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-entitymanager</artifactId>
    <version>5.6.15.Final</version>
</dependency>
```

```
// https://mvnrepository.com/artifact/org.hibernate/hibernate-entitymanager
implementation 'org.hibernate:hibernate-entitymanager:5.6.15.Final'
```


В ресурсах в директории db.migration создаем
![[Pasted image 20240506155351.png]]
Пример таблицы
```sql
CREATE TABLE product  
(  
    id SERIAL PRIMARY KEY,  
    name VARCHAR(30),  
    price DECIMAL(13, 10),  
        PRIMARY KEY (id)  
);
```
Для настройки используем application
![[Pasted image 20240506155438.png]]
Пример для postgres.12. Но уже для созданной db.
```yml
server:  
  port: 8080  
  
spring:  
  datasource:  
    url: jdbc:postgresql://localhost:5432/product  
    username: admin  
    password: 229csx229CSX  
#    driverClassName: org.postgresql.Driver  
  flyway:  
    enabled: true  
    locations:  
      - db.migration  
    validate:  
      -off  
      -migrate=false  
#  jpa:  
#    database-platform: org.hibernate.dialect.PostgreSQL10Dialect
```
Порт 5432 - для локалки. Для бд из контейнера для запуска на локалке использовать внешний порт, для запуска внутри контейнера - внутренний
Пример
![[Pasted image 20240506155736.png]]
Для такого контейнера для запуска на локалке использовать 5430. Для запуска в контейнере 5432

docker-compose.yml для данной бд
```yml
version: '3.9'  
services:  
  # Сервис для разворачивания контейнера с базой данных  
  postgres:  
    container_name: postgres  
    image: postgres:12  
    hostname: database  
    volumes:  
      - ./postgres:/docker-entrypoint-initdb.d  
    environment:  
      - POSTGRES_DB=product  
      - POSTGRES_USER=admin  
      - POSTGRES_PASSWORD=229csx229CSX  
    ports:  
      - "5430:5432"
```


Пример для создания Entity
![[Pasted image 20240506160542.png]]
Используется ломбок также
Product.java
```java
package com.flyway.entity;  
import jakarta.persistence.*;  
import lombok.Getter;  
import lombok.Setter;  
  
@Entity  
@Getter  
@Setter  
@Table(name = "product")  
public class Product {  
    @Id  
    @GeneratedValue(strategy = GenerationType.IDENTITY)  
    Long id;  
    @Column(name = "name")  
    String name;  
    @Column(name = "price")  
    Double price;  
}
```
Репозиторий
```java
package com.flyway.repository;  
import com.flyway.entity.Product;  
import org.springframework.data.jpa.repository.JpaRepository;  
import org.springframework.stereotype.Repository;  
  
@Repository  
public interface ProductRepository extends JpaRepository<Product, Long> {  
}
```




