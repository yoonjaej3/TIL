## pen-In-View 또는 Open-Session-In-View 또는 Open-EntityManager-In-View 란?
- 관례상 OSIV 라고 한다.

 ![image](https://user-images.githubusercontent.com/57666307/172003616-0b24aee2-25fd-4454-a500-ee8294ba28d5.png)
- true일 경우 영속성 컨텍스트가 트랜잭션 범위를 넘어선 레이어까지 살아있다.
- Api라면 클라이언트에게 응답될 때까지, View라면 View가 렌더링될 때까지 영속성컨텍스트가 살아있다.
- 기본값은 true 이다

 ![image](https://user-images.githubusercontent.com/57666307/172003643-5fa73fcc-19ff-40ef-9eb5-b021114fdb37.png)

- false일 경우 트랜잭션을 종료할 때 영속성 컨텍스트 또한 닫힌다.

