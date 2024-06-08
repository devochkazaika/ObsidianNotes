Делаем конфигурацию со следующим бином
```java
@Bean  
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception{  
    return http.authorizeHttpRequests(authorizaHttpRequest -> authorizaHttpRequest  
          .anyRequest().denyAll()  
          .dispatcherTypeMatchers(DispatcherType.FORWARD,
		    DispatcherType.ERROR).permitAll()
          .requestMatchers("/permit-all").permitAll()  
          .requestMatchers("/anonymous").anonymous()  
          .requestMatchers("authenticated").authenticated()  
          .requestMatchers("/remember-me").rememberMe()  
          .requestMatchers("/fully-authenticated").fullyAuthenticated()  
          .requestMatchers("has-view-authority").hasAuthority("view")  
          .requestMatchers("/has-update-or-delete-authority").hasAnyAuthority("update", "delete")  
          .requestMatchers("/has-admin-role").hasRole("admin")  
          .requestMatchers("/has-customer-or-manager-role").hasAnyRole("customer", "manager")  
          .requestMatchers("/has-access").access(((authentication, object) ->  
                new AuthorizationDecision("c.norris".equals(authentication.get().getName())))  
          )  
    ).build();  
}
```
`anyRequest()` - правило авторизации для всех запросов
`dispathcerTypeMatcher` - Для перенаправления запросов
`requestMatchers(str)` - правило для конкретного запроса
`permitAll()` - разрешить всем
`authenticated()` - только для аутентифицированных
`rememberMe()` - пользователи с долгоживущей сессией
`fullyAuthenticated()` - для полностью аутентифицированных()
`hasAuthority("view")` - только пользователи с правом view
`hasAnyRole()` - пользователи с любой из перечисленных ролей
`hasRole()` - только пользователь с указанной ролью
`access` - функциональный подход к доступу. 


Если `requestMatchers` не принимает строки тогда можно юзать `antMatchers`