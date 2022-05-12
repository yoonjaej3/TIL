## 자바8 스트림 

### Map

- map 메서드는 입력 컬렉션을 출력 컬렉션으로 매핑하거나 변경할때 유용하다.

```
final List<String> names = Arrays.asList("Sehoon", "Songwoo", "Chan", "Youngsuk", "Dajung");
            //java 7
            System.out.println("java 7");
            for(String name : names) {
                System.out.println(name.toUpperCase());
            }
 
            System.out.println("");
 
            //java 8 Lambda
            System.out.println("java 8");
            names.stream()
                .map(name -> name.toUpperCase())
                .forEach(name -> System.out.println(name));

```

### filter

- filter 메서드는 컬렉션을 조건에 의한 선택을 할때 유용하다. filter 메서드는
boolean 결과를 리턴하는 람다표현식이 필요하다.

```
final Listt<String> names = Arrays.asList("Sehoon", "Songwoo", "Chan", "Youngsuk", "Dajung");
 
        //java 7
        System.out.println("java 7");
        final List<string> startsWithN1 = new ArrayList<string>();
        for (String name : names) {
            if (name.startsWith("S")) {
                startsWithN1.add(name);
            }
        }
 
        System.out.println(startsWithN1);
 
        System.out.println("");
 
        //java 8 Lambda
        System.out.println("java 8");
        final List<string> startsWithN2 = 
                names.stream().filter(name -> name.startsWith("S"))
                                .collect(Collectors.toList());
 
        System.out.println(startsWithN2)
```

### reduce
- reduce 메서드는 엘리먼트를 비교하고 컬렉션에서 하나의 값으로 연산한다.
람다 예제 소스를 보면 첫번째로 리스트에 있는 처음 두개 엘리먼트를 사용한다. 그리고 람다 표현식의 결과는 다음호출에 사용된다.
두번째 호출에서는 name1은 이전 호출의 결과이며 name2는 컬렉션의 세번째 엘리먼트 이다.

```
final List<String> names = Arrays.asList("Sehoon", "Songwoo", "Chan", "Youngsuk", "Dajung");
 
//java 7
String LongerEliment1  = "";
for (String name : names) {
    if(("hoone".length() <= name.length()) && (LongerEliment1.length() <= name.length())) {
        LongerEliment1 = name;
    }
}
 
System.out.println("java 7 "+LongerEliment1);
 
//java 8 Lambda
String LongerEliment2 = names.stream()
        .reduce("hoone", (name1, name2) ->
            name1.length() >= name2.length() ? name1 : name2);
System.out.println("java 8 "+LongerEliment2);
```

### collect
- collect 메서드는 reduce() 메서드와 동일하게 값을 하나로 모으는 다른형태인데, collect는 여러 convenience method를 제공한다.
아래 예제는 리스트의 엘리먼트를 콤마로 구분하여 출력하는데, 기존 for문으로는 마지막 엘리먼트에 콤마를 안붙이는게 쉽지는 않다. 
하지만 collect 머서드를 사용하면 간단하게 만들 수 있다

```
final List<String> names = Arrays.asList("Sehoon", "Songwoo", "Chan", "Youngsuk", "Dajung");
 
System.out.println("java 7");
//java 7
for(int i = 0; i < names.size() - 1; i++) {
    System.out.print(names.get(i).toUpperCase() + ", ");
}
 
if(names.size() > 0) {
    System.out.println(names.get(names.size() - 1).toUpperCase());
}
 
System.out.println("java 8");
//java 8 Lambda
System.out.println(names.stream()
            .map(String::toUpperCase)
            .collect(Collectors.joining(", ")));
```



