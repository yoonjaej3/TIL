## Junit 예외처리

### Using assertThatThrownBy()

```
assertThatThrownBy(() -> {
    List<String> list = Arrays.asList("String one", "String two");
    list.get(2);
}).isInstanceOf(IndexOutOfBoundsException.class)
  .hasMessageContaining("Index: 2, Size: 2");
  ```
  
  ```
  .hasMessage("Index: %s, Size: %s", 2, 2)
.hasMessageStartingWith("Index: 2")
.hasMessageContaining("2")
.hasMessageEndingWith("Size: 2")
.hasMessageMatching("Index: \\d+, Size: \\d+")
.hasCauseInstanceOf(IOException.class)
.hasStackTraceContaining("java.io.IOException");
```


### Separating the Exception From the Assertion
An alternative way to write our unit tests is writing the when and then logic in separate sections:
```
// when
Throwable thrown = catchThrowable(() -> {
    // ...
});

// then
assertThat(thrown)
  .isInstanceOf(ArithmeticException.class)
  .hasMessageContaining("/ by zero");
```

출처 : https://www.baeldung.com/assertj-exception-assertion#1-using-assertthatthrownby
