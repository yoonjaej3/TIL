## 원시타입(Primitive Type)

정수, 실수, 문자 리터럴등의 실제 데이터 값을 저장하는 타입

![image](https://user-images.githubusercontent.com/57666307/160528088-cdc53456-7ee6-4b55-84db-6ebadd24ba6f.png)

## 참조타입(Reference Type)

원시 타입을 제외한(문자열, 배열, 열거, 클래스, 인터페이스) 타입. 객체의 주소를 저장하는 타입으로 메모리 번지값을 통해서 객체를 저장하는 타입

## 차이점

![image](https://user-images.githubusercontent.com/57666307/160528115-843dbb86-17b0-4679-8a94-f7a58705355f.png)

Primitive Type은 스택영역에 기본타입 변수가 할당되고,  변수의 실제 값들이 저장된다.

Reference Type은 스택영역에 힙영역에서 생성된 주소값들이 저장된다. 즉 스택에는 참조값(주소값)만 있고, 실제 값은 힙 메모리에 있다. 

값이 필요할떄마다 언박싱 과정을 거쳐야 하니 Primitive Type과 비교해서 접근 속도가 느려지게 됩니다.(예외적으로 엄청 큰 숫자를 복사해야 된다면, 참조값만 넘길 수 있는 Reference Type이 더 좋을 수 있음)

![image](https://user-images.githubusercontent.com/57666307/160528144-0b20736e-a6d7-4814-9469-1bacd0e6755a.png)
