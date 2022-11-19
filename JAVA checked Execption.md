## Checked,Unchecked Exception 차이

![image](https://user-images.githubusercontent.com/57666307/202846961-b5be345c-b748-4756-9f6d-63ff24989360.png)


![image](https://user-images.githubusercontent.com/57666307/202847004-8c7bfd4c-c887-4a85-8f49-e452bca94889.png)

Checked, Unchecked은 개발자들이 만든 애플리케이션 코드에서 예외가 발생했을 경우에 사용하게 됩니다.

위 상속 구조를 처럼 Unchecked Exception는 RuntimeException을 상속하고 Checked Exception는 RuntimeException을 상속하지 않습니다.

이것으로 두 Exception을 구분하는 중요한 포인트입니다.

- Unchecked Exception
명시적인 예외 처리를 강제하지 않는 특징이 있기 때문에 Unchecked Exception이라 하며, catch로 잡거나 throw로 호출한 메서드로 예외를 던지지 않아도 상관이 없습니다.

- Checked Exception
반드시 명시적으로 처리해야 하기 때문에 Checked Exception이라고 하며, try catch를 해서 에러를 잡든 throws를 통해서 호출한 메서드로 예외를 던져야 합니다.
