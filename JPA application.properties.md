```
spring:
  datasource:
    url: 
    username: 
    password:
    driver-class-name: org.h2.Driver
    initialization-mode: always

  jpa:
    open-in-view: false
    hibernate:
      ddl-auto: create
    properties:
      hibernate:
        show_sql: true
        format_sql: true
        default_batch_fetch_size: 1000 #최적화 옵션
    defer-datasource-initialization: true


logging.level:
  org.hibernate.SQL: debug
#  org.hibernate.type: trace
```



- OSIV가 true
사용자에게 응답 또는 view가 렌더링 될 때까지 영속성컨텍스트를 유지한다.

- OSIV가 false
Transaction이 끝나면 영속성컨텍스트 또한 닫힌다

- "src/main/resources/data.sql"에 Import 데이터를 작성하면, 서버 실행 시 자동으로 실행된다.
initialization-mode: always
defer-datasource-initialization: true


TODO : default_batch_fetch_size

TODO : 로그설정

