## JAVA8 날짜계산


### 기계용 날짜 API :: Instant

```
// 현재 시간을 유닉스 에포크 시간으로 나타내는 코드 (모든 시간을 초로 환산하여 표시)
System.out.println(Instant.now().getEpochSecond());

// 유닉스 에포크 시간의 기준시를 나타내는 코드(기준시기 때문에 초로 환산해도 0으로 출력된다)
System.out.println(Instant.ofEpochSecond(0).getEpochSecond());
```


### 사람용 날짜 API :: LocalDate, LocalTime, LocalDateTime

```
// LocalDateTime 객체를 사용한 코드
LocalDateTime plusTenDay = LocalDateTime.now().plusDays(10L);

// Date 객체를 사용한 코드
Date today = new Date();
today.setDate(today.getDate() + 10);
```


### 날짜와 시간의 간격을 나타내는 API :: Duration, Periord

```
LocalDateTime now = LocalDateTime.now();
LocalDateTime newYear = LocalDateTime.of(2020, 12, 31, 12, 30);

// 시간의 차이를 비교
Duration duration = Duration.between(now, newYear);
System.out.println(duration.getSeconds());

// 날짜의 차이를 비교
Period period = Period.between(now.toLocalDate(), newYear.toLocalDate());
System.out.println(period.getDays());
```

### 날짜 포맷을 위한 새로운 클래스 :: DateTimeFormatter

```
System.out.println(
    LocalDateTime
        .now()
        .format(DateTimeFormatter
                .ofPattern("오늘은 y-mm-dd일 (E)이고, 현재시간은 a h:s분입니다.")
                .withLocale(Locale.KOREA))
);
```

출처 : https://bbubbush.tistory.com/23
