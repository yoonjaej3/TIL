## JAVA Optional

### 자바에서 NULL로 인해 발생할 수 있는 문제는
- 런타임에 NPE(NullPointerException)라는 예외를 발생시킬 수 있습니다.
- NPE 방어를 위해서 들어간 null 체크 로직 때문에 코드 가독성과 유지 보수성이 떨어집니다.

### OPTIONAL의 효과
- NPE를 유발할 수 있는 null을 직접 다루지 않아도 됩니다.
- 수고롭게 null 체크를 직접 하지 않아도 됩니다.
- 명시적으로 해당 변수가 null일 수도 있다는 가능성을 표현할 수 있습니다. (따라서 불필요한 방어 로직을 줄일 수 있습니다.)

### 메소드의 반환값이 존재하지 않을 때 전통적인 처리 패턴
#### null 반환
```
String city = cities.get(4); // returns null
int length = city == null ? 0 : city.length(); // null check
System.out.println(length);
```

```
Optional<String> maybeCity = Optional.ofNullable(cities.get(4)); // Optional
int length = maybeCity.map(String::length).orElse(0); // null-safe
System.out.println("length: " + length);
```
#### 예외처리
```
String city = null;
try {
	city = cities.get(3); // throws exception
} catch (ArrayIndexOutOfBoundsException e) {
	// ignore
}
int length = city == null ? 0 : city.length(); // null check
System.out.println(length)
```

```
public static <T> Optional<T> getAsOptional(List<T> list, int index) {
	try {
		return Optional.of(list.get(index));
	} catch (ArrayIndexOutOfBoundsException e) {
		return Optional.empty();
	}
}

Optional<String> maybeCity = getAsOptional(cities, 3); // Optional
int length = maybeCity.map(String::length).orElse(0); // null-safe
System.out.println("length: " + length);
```

### ifPresent() 메소드
- 이 메소드는 특정 결과를 반환하는 대신에 Optional 객체가 감싸고 있는 값이 존재할 경우에만 실행될 로직을 함수형 인자로 넘길 수 있습니다.
- 동기 메소드의 콜백 함수처럼 작동합니다
```
Optional<String> maybeCity = getAsOptional(cities, 3); // Optional
maybeCity.ifPresent(city -> {
	System.out.println("length: " + city.length());
});
```

출처: https://www.daleseo.com/java8-optional-effective/
