# Spring boot 예외 전역 처리 example code

## GlobalControllerAdvice.java
```java
@RestControllerAdvice
public class GlobalControllerAdvice {
    @ExceptionHandler(RegistrationException.class)
    public ResponseEntity<Map<String, String>> registrationException(RegistrationException exception) {
        Map<String, String> map = new HashMap<>();
        map.put("message", exception.getMessage());
        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(map);
    }
}

```

## RegistrationException.java
```java
public class RegistrationException extends RuntimeException {
    public RegistrationException(String message) {
        super(message);
    }
}
```

## UserService.java
```java
            ... 중략 ...
            throw new RegistrationException("Account Already Exist");
```

## [PostMan] Response Body
```json
{
    "message": "Already exist EMAIL"
}
```
