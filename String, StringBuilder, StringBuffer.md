## String, StringBuilder, StringBuffer

```
String result = "";
result += "A";
result += " ";
result += "B";
```
```
StringBuilder sb = new StringBuilder();
sb.append("A");
sb.append(" ");
sb.append("B");
String result = sb.toString();
```

일반적으로 문자열을 String으로 사용하는데 이는 장단점이 있다.

String 자료형은 한번 값이 생성되면 변경될수 없는 immutable 특징을 가지고 있기때문에 +연산이 있을때마다 새로운 String 객체를 만들어 낸다. 

문자열 변경 작업이 없는 경우에 좋다.(상대적으로 가볍기 떄문)

하지만 문자열의 추가나 변경이 많을 경우에는 mutable한 StringBuffer나 StringBuilder를 사용하는게 좋다.

StringBuffer는 멀티 스레드 환경에서 안전하다는 장점이 있고 StringBuilder는 StringBuffer보다 성능이 우수한 장점이 있다. 

따라서 동기화를 고려할 필요가 없는 상황에서는 StringBuffer 보다는 StringBuilder를 사용하는 것이 유리하다
