Добавление зависимости
```java
@Bean  
public Keycloak getAdminKeycloakUser() {  
    return KeycloakBuilder.builder()  
            .serverUrl("http://localhost:8081")  
            .grantType(OAuth2Constants.PASSWORD)  
            .realm("master")  
            .clientId("maker")  
            .username("admin")  
            .password("password")  
            .build();  
}
```
serverUrl - адрес сервера keycloak
grantType - Тип аутентификации
realm - имя реалма
clientId  - имя клиента
username - или пользователя или можно админа
password
По сути большая часть храниться в application.yml, через аннотацию @Value можно их прогружать в проект и записывать в бин срауз

Для автоматической настройки конфигураций из application.yml
```java
@Bean  
public KeycloakSpringBootConfigResolver keycloakConfigResolver() {  
    return new KeycloakSpringBootConfigResolver();  
}
```


в application.yml должно быть
```yml
keycloak:  
  #сам keycloak(нужно поменять порт на внутренний для докера)  
  auth-server-url: http://localhost:8282/auth  
  #имя реалма из экспорта или созданного  
  realm: content-maker  
  #имя клиента  
  resource: maker
```
