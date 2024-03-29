## querydsl

### fetch
 
1) fetch()

리스트로 결과를 반환하는 방법이다. 만약에 데이터가 없으면 빈 리스트를 반환해준다.

```
List<Member> fetch = queryFactory
		.selectFrom(member)
        	.fetch();
```
 

2) fetchOne()

단건을 조회할 때 사용한다. 결과가 없을때는 null 을 반환하고 결과가 둘 이상일 경우에는 NonUniqueResultException을 던진다.

```
Member fetchOne = queryFactory
		.selectFrom(member)
        	.fetch();
``` 

3) fetchFirst()

처음의 한건을 가져오고 싶을때 사용한다.

```
Member fetchFirst = queryFactory
		.selectFrom(QMember.member)
		//.limit(1).fetchOne()
		.fetchFirst();
 ```

4) fetchResults()

페이징을 위해 사용될 수 있다. 페이징을 위해서 total contents를 가져온다.

```
QueryResults<Member> results = queryFactory
		.selectFrom(member)
		.fetchResults();
``` 

5) fetchCount()

```
long count = queryFactory
		.selectFrom(member)
		.fetchCount();
``` 

### sort

1) 내림차순 정렬 (desc())

```
List<Member> descAge = queryFactory
			.selectFrom(member)
			.where(member.age.eq(50))
			.orderBy(member.age.desc())
			.fetch();
```
 

2) 오름차순 정렬 (asc())

```
List<Member> descAge = queryFactory
			.selectFrom(member)
			.where(member.age.eq(50))
			.orderBy(member.userName.asc())
			.fetch();
``` 

3) 여러 조건으로 정렬 하는 방법

```
List<Member> result = queryFactory
			.selectFrom(member)
			.where(member.age.eq(50))
			.orderBy(member.age.desc(), member.userName.asc())
			.fetch();
``` 

4) null 처리

데이터에 null 이 있을시 가장 뒤에 나오도록 하려면 nullsLast(), 가장 앞에 나오도록 하려면 nullsFirst()

```
List<Member> result = queryFactory
		.selectFrom(member)
		.where(member.age.eq(50))
		.orderBy(member.age.desc(), member.userName.asc().nullsLast())
		.fetch();
``` 

### paging

```
QueryResults<Member> result = queryFactory
		.selectFrom(member)
		.orderBy(member.userName.desc())
		.offset(1)
		.limit(2)
		.fetchResults();
```

long total = result.getTotal(); //전체 컨텐츠 갯수
long limit = result.getLimit(); // 현재 제한한 갯수
long offset = result.getOffset(); // 조회 시작 위치
List<Member> results = result.getResults(); // 조회된 컨텐츠 리스트
  
querydsl 에서는 아래처럼 조금더 심화된 방법으로 paging이 가능하다.

이렇게 만들어 두면 만약에 page의 시작이면서 컨텐츠 사이즈가 페이지 사이즈보다 작거나,

마지막 페이지 인 경우엔 count 쿼리를 생략할 수 있다.

```
public Page<Membmer> search(Pageable pageable) {
List<Membmer> content = queryFactory
              .select(member)
              .from(member)
              .leftJoin(member.team, team)
              .offset(pageable.getOffset())
              .limit(pageable.getPageSize())
              .fetch();

      JPAQuery<Member> countQuery = queryFactory
              .select(member)
              .from(member)
              .leftJoin(member.team, team);

      return PageableExecutionUtils.getPage(content, pageable, countQuery::fetchCount);
}
```
### aggregation

  ```
List<Tuple> result = queryFactory
		.select(
				team.name,
				member.count(),
				member.age.avg(),
				member.age.sum(),
				member.age.min(),
				member.age.max()
		)
		.from(member)
		.join(member.team, team)
		.groupBy(team.name)
		.having(team.name.eq("a"))
		.fetch();

Tuple teamA = result.get(0);

String teamAName = teamA.get(team.name);
Long teamACount = teamA.get(member.count());
Double teamAAvgAge = teamA.get(member.age.avg());
Integer teamASum = teamA.get(member.age.sum());
Integer teamAMin = teamA.get(member.age.min());
Integer teamAMax = teamA.get(member.age.max());
  ```

### 페이징 처리
- offset과 limit를 통해서 페이징을 할 수 있다.
  offset은 0부터 시작하며, 몇 번째 row에서 데이터 조회를 시작할지 정한다.

 ```
@Test
public void paging1() {
   List<Member> result = queryFactory
         .selectFrom(member)
         .orderBy(member.username.desc())
         .offset(1) //offset은 0부터 시작(zero index), 현재 코드에서는 1번부터 데이터를 가져오도록 하므로 맨 처음 데이터는 생략됨
         .limit(2) //최대 2건 조회
         .fetch();
   assertThat(result.size()).isEqualTo(2);
}
 ```

	
###  카운팅 쿼리를 분리한 페이징 최적화	
```
@Override
public Page<MemberTeamDto> searchPageComplex(MemberSearchCondition condition,
Pageable pageable) {
 	List<MemberTeamDto> content = queryFactory
 		.select(new QMemberTeamDto(
 					member.id,
 					member.username,
 					member.age,
 					team.id,
 					team.name))
 		.from(member)
 		.leftJoin(member.team, team)
 		.where(usernameEq(condition.getUsername()),
 				teamNameEq(condition.getTeamName()),
 				ageGoe(condition.getAgeGoe()),
 				ageLoe(condition.getAgeLoe()))
 		.offset(pageable.getOffset())//offset은 page * size
 		.limit(pageable.getPageSize())
 		.fetch();
    
    
    //count 쿼리 분리
            
 	JPAQuery<Member> countQuery = queryFactory
 			.select(member)
 			.from(member)
 			.leftJoin(member.team, team)
 			.where(usernameEq(condition.getUsername()),
 					teamNameEq(condition.getTeamName()),
					ageGoe(condition.getAgeGoe()),
 					ageLoe(condition.getAgeLoe()));
                            
	return PageableExecutionUtils.getPage(content, pageable,countQuery::fetchCount);
}	
```
 
페이징 관련 출처 : https://ttl-blog.tistory.com/228#no_3
	

limit는 한 화면에 보여줄 데이터의 개수이다.

	
출처 : https://devkingdom.tistory.com/243
