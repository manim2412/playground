# jwt 구성 요소
## 1. header
어떠한 알고리즘으로 암호화 할 것인지, 어떠한 토큰을 사용할 것 인지에 대한 정보가 들어 있음
## 2. payload
전달하려는 정보(claim)가 들어 있음
## 3. signature
**header**와 **payload**를 합친 후 지정한 **secret key**로 암호화 시켜 토큰을 변조하기 어렵게 만

### dependency (Spring Boot 3 기준)
```
dependencies {
	implementation 'io.jsonwebtoken:jjwt-api:0.12.6'
	runtimeOnly 'io.jsonwebtoken:jjwt-impl:0.12.6'
	runtimeOnly 'io.jsonwebtoken:jjwt-jackson:0.12.6'
}
```

### token 생성
```java
        return Jwts.builder()
                .subject(user.getUsername())
                .issuer(issuer)
                .issuedAt(new Date())
                .expiration(new Date(System.currentTimeMillis() + expirationMinute * 60 * 1000))
                .signWith(key())
                .compact();
```

### token 검증
```java
        Jws<Claims> claims = Jwts.parser().setSigningKey(key()).build().parseSignedClaims(token);
//        System.out.println(claims.getPayload().getSubject());
//        System.out.println(claims.getPayload().getExpiration());
//        System.out.println(claims.getPayload().getIssuedAt());
//        System.out.println(claims.getPayload().getIssuer());

    private Key key() {
        return Keys.hmacShaKeyFor(Decoders.BASE64.decode(secretKey));
    }
```
