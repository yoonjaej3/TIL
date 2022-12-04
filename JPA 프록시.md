### JPA 에서 프록시

- 영속성 컨텍스트는 자신이 관리하는 영속 엔티티의 동일성을 보장한다.

- 프록시는 원본 엔티티를 상속받아서 만들어지므로 엔티티를 사용하는 클라이언트는 엔티티가 프록시인지 원본 엔티티인지 구분하지 않고 사용할 수 있다.

```
Member refMember = em.getReference(Member.class, "member1");
Member findMember = em.find(Member.class, "member1");
```

=> em.find() 의 결과는 member1 의 프록시 객체

```
Member findMember = em.find(Member.class, "member1");
Member refMember = em.getReference(Member.class, "member1");
```

=> em.getReference() 의 결과는 member의 엔티티


- 즉, 영속성 컨텍스트에 원본 엔티티이든, 프록시이든 먼저 조회해 놓은 것을 이후에도 반환한다.
- 영속성 컨텍스트는 자신이 관리하는 영속 엔티티의 동일성을 보장한다.

### 프록시 타입 비교

```
Member refMember = em.getReference(Member.class, "member1");
Assert.assertFalse(Member.class == refMember.getClass()); // false
Assert.assertTrue(refMember instanceof Member); // true
```
- 프록시는 원본 엔티티를 상속받아서 만들어지므로 프록시로 조회한 엔티티의 타입을 비교할 때는 == 비교 대신 instanceof 를 사용해야 한다.

- refMember.getClass() 결과는 class jpabook.advanced.Member_$$_jvsteXXX이다. _$$_jvsteXXX 가 붙어 있으면 프록시라는 의미이다.

- Member.class == refMember.getClass()는 부모 클래스와 자식 클래스를 == 비교한 셈이다.

- 프록시는 원본 엔티티의 자식 타입이므로 instanceof 연산을 사용해야 한다.





https://www.nowwatersblog.com/jpa/ch15/15-3
