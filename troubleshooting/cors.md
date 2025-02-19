# https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F
# https://docs.spring.io/spring-framework/reference/web/webmvc-cors.html

## 1. client
Http request에 **Origin** 전달
## 2. server
http response에 **Acess-Control-Allow-Origin** 전달
## 3. client
client request Origin과
server response Access-Control-Allow-Origin 비교

```java
@Configuration
@EnableWebMvc
public class CorsConfig implements WebMvcConfigurer {
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://localhost:3000")
                .allowedMethods("POST", "GET", "OPTIONS")
                .allowCredentials(true);
    }
}
```

[application.properties]
```java
logging.level.org.springframework.web.cors=DEBUG
```
