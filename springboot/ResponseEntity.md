# ResponseEntity example

```java
    @PostMapping("/register")
    public ResponseEntity<RegistrationResponse> registrationRequest(@Valid @RequestBody RegistrationRequest request) {
        RegistrationResponse response = userService.registration(request);
        return ResponseEntity.status(HttpStatus.CREATED).body(response);
    }
```

```java
    @ExceptionHandler(RegistrationException.class)
    public ResponseEntity<Map<String, String>> registrationException(RegistrationException exception) {
        Map<String, String> map = new HashMap<>();
        map.put("message", exception.getMessage());
        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(map);
    }
```
