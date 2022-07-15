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

### 연습문제

```
public static class Trader {

            private final String name;
            private final String CITY;

            public Trader(String name, String CITY) {
                        this.name = name;
                        this.CITY = CITY;
            }

            public String getName() {
                        return name;
            }

            public String getCITY() {
                        return CITY;
            }

            @Override
            public String toString() {
                        return "Trader{" + "name='" + name + '\'' + ", CITY='" + CITY + '\'' + '}';
            }
}


public static class Transaction {

            private final Trader trader;
            private final int year;
            private final int value;

            public Transaction(Trader trader, int year, int value) {
                        this.trader = trader;
                        this.year = year;
                        this.value = value;
            }

            public Trader getTrader() {
                        return trader;
            }

            public int getYear() {
                        return year;
            }

            public int getValue() {
                        return value;
            }

            @Override
            public String toString() {
                        return "Transaction{" + "trader=" + trader + ", year=" + year + ", value=" + value + '}';
            }
}


public static void main(String[] args) throws Exception {

            Trader raoul = new Trader("Raoul", "Cambridge");
            Trader mario = new Trader("Mario", "Milan");
            Trader alan = new Trader("Alan", "Cambridge");
            Trader brian = new Trader("Brian", "Cambridge");

            List<Transaction> transactions = Arrays.asList(new Transaction(brian, 2011, 300),
                                    new Transaction(raoul, 2012, 1000), new Transaction(raoul, 2011, 400),
                                    new Transaction(mario, 2012, 710), new Transaction(mario, 2012, 700), new Transaction(alan, 2012, 950));

            // 1. 2011년에 일어난 모든 트랜잭션을 찾아 값을 오름차순으로 정렬하시오.
            // CODE
            List<Integer> answer1 = transactions.stream().filter(i -> i.getYear() == 2011).map(Transaction::getValue)
                                    .sorted().collect(Collectors.toList());
            System.out.println(answer1);
            // 2. 2011년에 일어난 모든 트랜잭션을 찾아 값을 기준으로 오름차순으로 정렬하시오.
            // CODE
            List<Transaction> answer2 = transactions.stream().filter(i -> i.getYear() == 2011)
                                    .sorted(Comparator.comparing(Transaction::getValue)).collect(Collectors.toList());
            System.out.println(answer2);
            // 3. 거래자가 근무하는 모든 도시를 중복 없이 나열하시오.
            // CODE
            List<String> answer3 = transactions.stream().map(Transaction::getTrader).map(Trader::getCITY).distinct()
                                    .collect(Collectors.toList());
            System.out.println(answer3);
            // 4. 케임브리지에서 근무하는 모든 거래자를 찾아서 이름순으로 정렬하시오.
            // CODE
            List<Trader> answer4 = transactions.stream().map(Transaction::getTrader)
                                    .filter(i -> i.getCITY().equals("Cambridge")).sorted(Comparator.comparing(Trader::getName))
                                    .collect(Collectors.toList());
            System.out.println(answer4);
            // 5. 모든 거래자의 이름을 알파벳 역순으로 정렬해서 반환하시오.
            // CODE
            List<String> answer5 = transactions.stream().map(Transaction::getTrader).map(Trader::getName)
                                    .sorted(Comparator.reverseOrder()).collect(Collectors.toList());
            System.out.println(answer5);
            // 6. 밀라노에 거래자가 있는가?
            // CODE
            boolean answer6=transactions.stream().map(Transaction::getTrader).anyMatch(i->i.getCITY().equals("Milan"));
            System.out.println(answer6);
            // 7. 케임브리지에 거주하는 거래자의 모든 트랜잭션 값을 출력하시오.
            // CODE
            List<Integer>answer7=transactions.stream().filter(i->i.getTrader().getCITY().equals("Cambridge")).map(Transaction::getValue).collect(Collectors.toList());
            System.out.println(answer7);
            // 8. 전체 트랜잭션 중 최댓값은 얼마인가?
            // CODE
            Integer answer8=transactions.stream().map(Transaction::getValue).reduce(0, Integer::max);
            System.out.println(answer8);

}
```

연습문제 출처 : https://p829911.tistory.com/21

