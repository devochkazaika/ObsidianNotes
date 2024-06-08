### Состоит из
* - **Заголовок** - хранит тип токена и алгоритм шифрования
* - **Полезная нагрузка** - данные пользователя, разрешения и тд (может быть всё что угодно)
* - **Подпись** - обеспечивает целостность данных, путём проверки, что токен не был изменён после создания
```xml
```
```xml
<dependency>        
	<groupId>io.jsonwebtoken</groupId>        
	<artifactId>jjwt-api</artifactId>    
</dependency>    
<dependency>        
	<groupId>io.jsonwebtoken</groupId>       
	<artifactId>jjwt-impl</artifactId>    
</dependency>    
<dependency>       
	<groupId>io.jsonwebtoken</groupId>       
	<artifactId>jjwt-jackson</artifactId>    
</dependency>
```
```gradle
implementation 'io.jsonwebtoken:jjwt-api:0.11.5'  
runtimeOnly 'io.jsonwebtoken:jjwt-impl:0.11.5'  
runtimeOnly 'io.jsonwebtoken:jjwt-jackson:0.11.2'
```
Подпись для токена для application,yml
Лучше не хранить в application.yml ключ для подписи
```yml
token:  
	signing:    
		key: 
			53A73E5F1C4E0A2D3B5F2D784E6A1B423D6F247D1F6E5C3A596D635A75327855
```

Генерация токена
```java
private String generateToken(Map<String, Object> extraClaims, UserDetails userDetails) {  
	return Jwts.builder().setClaims(extraClaims).setSubject(userDetails.getUsername()) 
          .setIssuedAt(new Date(System.currentTimeMillis()))  
          .setExpiration(new Date(System.currentTimeMillis() + 100000 * 60 * 24))  
          .signWith(getSigningKey(), SignatureAlgorithm.HS256).compact();  
}

public String generateToken(UserDetails userDetails) {  
    Map<String, Object> claims = new HashMap<>();  
    if (userDetails instanceof User customUserDetails) { 
	//Поля для токена 
       claims.put("id", customUserDetails.getId());  
       claims.put("email", customUserDetails.getEmail());  
       claims.put("role", customUserDetails.getRole());  
    }  
    return generateToken(claims, userDetails);  
}
```

### Работа с времене токена
Проверка просроченности токена
```java
private boolean isTokenExpired(String token) {  
    return extractExpiration(token).before(new Date());  
}
```
Узнать время жизни токена
```java
private Date extractExpiration(String token) {  
    return extractClaim(token, Claims::getExpiration);  
}
```