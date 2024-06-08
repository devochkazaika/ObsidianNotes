Чтобы тестилось без security filter chain
Можно просто добавить новый конфиг к тестам
```java
@Configuration  
public class TestSecurityConfig {  
    @Bean  
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {  
        http.csrf().disable()  
                .authorizeRequests()  
                .anyRequest().permitAll();  
        return http.build();  
    }  
}```

И еще добавить аннотации к контроллерам
```java
@ExtendWith(SpringExtension.class)  
@WebMvcTest(value = HelloWorldController.class)  
@ComponentScan
```
