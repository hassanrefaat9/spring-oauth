# spring-oauth
OAuth2 Login with Google and GitHub using Spring Security

## dependencies
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
```

## Google OAuth2 Login
1. Create a new project in Google Cloud Platform
2. Enable Google+ API
3. Create OAuth2 credentials
4. Add Authorized redirect URIs
5. Add OAuth2 Client ID and Client Secret to application.properties
6. Add GoogleOAuth2UserService to Spring Security configuration
```properties
spring.security.oauth2.client.registration.google.client-id=...
spring.security.oauth2.client.registration.google.client-secret=...
```

## GitHub OAuth2 Login
1. Create a new OAuth App in GitHub
2. Add GitHub Client ID and Client Secret to application.properties
3. Add GitHubOAuth2UserService to Spring Security configuration
```properties
spring.security.oauth2.client.registration.github.client-id=...
spring.security.oauth2.client.registration.github.client-secret=...
```
## Security Configuration
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception{
        return http
                .authorizeHttpRequests(auth ->{
                    auth.requestMatchers("/").permitAll();
                    auth.anyRequest().authenticated();
                })
                .oauth2Login(withDefaults())
                .formLogin(withDefaults())
                .build();
    }
}
```

