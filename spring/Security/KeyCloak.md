docker-compose
```yml
keycloak:  
  image: quay.io/keycloak/keycloak:latest  
  container_name: keycloak  
  environment:  
    KEYCLOAK_ADMIN: admin  
    KEYCLOAK_ADMIN_PASSWORD: admin_password  
  ports:  
    - "8484:8080"  
  command:  
    - start-dev
```
realm - контекст безопасности с правилами
![[Pasted image 20240520164703.png]]
![[Pasted image 20240520164742.png]]

### Создание нового пользователя
Вкладка Users
![[Pasted image 20240520164858.png]]

Пароли для user
![[Pasted image 20240520164933.png]]
![[Pasted image 20240520165015.png]]
Temporary - временный или не временный пароль

### Создание клиентов
![[Pasted image 20240520165119.png]]
Нужно только Client Id
![[Pasted image 20240520165159.png]]
Rost Url - адрес приложения
![[Pasted image 20240520165258.png]]

![[Pasted image 20240522165952.png]]
### Тестовый запрос
```
POST http://localhost:8484/realms/content-maker/protocol/openid-connect/token  
Content-Type: application/x-www-form-urlencoded  
  
client_id=maker&client_secret=hTgqr1l2cyzNG0n76Okpwja5E9z7zahq&username=testUser&password=password&grant_type=password
```
Должно быть что-то типа
![[Pasted image 20240520165823.png]]



### Добавить импорт
```
keycloak:      
	KEYCLOAK_IMPORT: /opt/jboss/keycloak/standalone/configuration/realm-export.json    
	volumes:      
		- ./realm-export.json:/opt/jboss/keycloak/standalone/configuration/realm-export.json
```