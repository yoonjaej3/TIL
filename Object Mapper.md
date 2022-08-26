## Object Mapper

### 기본적인 읽기 및 쓰기

- readValue (JSON 콘텐츠를 Java 객체로 구문 분석하거나 역직렬화하는 데 사용)

```
String json = "{ \"color\" : \"Black\", \"type\" : \"BMW\" }";
Car car = objectMapper.readValue(json, Car.class);
```
```
Car car = objectMapper.readValue(new File("src/test/resources/json_car.json"), Car.class)
```
```
Car car = 
  objectMapper.readValue(new URL("file:src/test/resources/json_car.json"), Car.class);
````
- writeValue (모든 Java 객체를 JSON 출력으로 직렬화)


```
ObjectMapper objectMapper = new ObjectMapper();
Car car = new Car("yellow", "renault");
objectMapper.writeValue(new File("target/car.json"), car)
```

- 출력 
 {"color":"yellow","type":"renault"}


```
String carAsString = objectMapper.writeValueAsString(car);
```
- Java 객체에서 JSON을 생성하고 생성된 JSON을 문자열 또는 바이트 배열로 반환


### 날짜 형식 처리

```
public class Request 
{
    private Car car;
    private Date datePurchased;

    // standard getters setters
}

ObjectMapper objectMapper = new ObjectMapper();
DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm a z");
objectMapper.setDateFormat(df);
String carAsString = objectMapper.writeValueAsString(request);
// output: {"car":{"color":"yellow","type":"renault"},"datePurchased":"2016-07-03 11:43 AM CEST"}
```


### 컬랙션 처리
```
String jsonCarArray = 
  "[{ \"color\" : \"Black\", \"type\" : \"BMW\" }, { \"color\" : \"Red\", \"type\" : \"FIAT\" }]";
ObjectMapper objectMapper = new ObjectMapper();
List<Car> listCar = objectMapper.readValue(jsonCarArray, new TypeReference<List<Car>>(){});
// print cars
```


출처 : https://recordsoflife.tistory.com/599

