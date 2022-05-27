## Lombook(@Data)

### 어노테이션

- @NorgsConstructor : 파라미터가 없는 기본 생성자 생성

- @AllArgsConstructor : 모든 필드 값을 파라미터로 받는 생성자를 만들어 준다.

- @RequiredArgsConstructor : final이나 @NonNull 인 필드 값만 파라미터로 받는 생성자를 만들어 준다.

- @ToString(exclude = "id") : exclude를 사용하면 toString() 결과에서 id를 제외시킬 수 있다.

- @EqualsAndHashCode

    1) equals :  두 객체의 내용이 같은지, 동등성(equality) 를 비교하는 연산자

    2) hashCode : 두 객체가 같은 객체인지, 동일성(identity) 를 비교하는 연산자

    3) (callSuper = true) : 부모 클래스 필드 값들도 동일한지 체크하며, false(기본값)일 경우 자신 클래스의 필드 값만 고려한다.

- @Data : @Getter, @Setter, @RequiredArgsConstructor, @ToString, @EqualsAndHashCode를 한번에 설정해주는 어노테이션이다.
