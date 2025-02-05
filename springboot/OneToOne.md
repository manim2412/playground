# OneToOne 양방향
```java
import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

@Getter
@Setter
@Entity
public class Member {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String username;

    @OneToOne(mappedBy = "member", cascade = CascadeType.ALL, orphanRemoval = true)
    private RefreshToken refreshToken;
}
```

```java
import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

@Getter
@Setter
@Entity
public class RefreshToken {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String token;

    @OneToOne
    @JoinColumn(name = "member_id")
    private Member member;
}
```

# OneToOne 단방향 (Member -> RefreshToken)
```java
@OneToOne(cascade = CascadeType.ALL)
@JoinColumn(name = "refresh_token_id")
private RefreshToken refreshToken;
// RefreshToken에 Member 필드가 없어야 합니다.
```

# OneToOne 단방향 (RefreshToken -> Member)
```java
@OneToOne
@JoinColumn(name = "member_id")
private Member member;
// Member에 RefreshToken 필드가 없어야 합니다.
```
