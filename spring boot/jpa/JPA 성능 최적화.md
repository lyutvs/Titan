# JPA 성능 최적화

---

## 트랜잭션을 지원하는 쓰기 지연(transactional write-behind) - 버퍼링

### **INSERT**

```java
/** 1. 트랜잭션을 커밋할 때까지 INSERT SQL을 모음 */

transaction.begin(); // [트랜잭션] 시작

em.persist(memberA);

em.persist(memberB);

em.persist(memberC);

// -- 여기까지 INSERT SQL을 데이터베이스에 보내지 않는다.

// 커밋하는 순간 데이터베이스에 INSERT SQL을 모아서 보낸다. --

/** 2. JDBC BATCH SQL 기능을 사용해서 한번에 SQL 전송 */

transaction.commit(); // [트랜잭션] 커밋
```

1. [트랜잭션]을 commit 할 때 까지 INSET SQL을 메모리에 쌓는다.

   이렇게 하지 않으면 DB에 INSERT Query를 날리기 위한 네트워크를 3번 타게 된다.

2. JDBC Batch SQL 기능을 사용해서 한번에 SQL을 전송한다.

   JDBC Batch 를 사용하면 코드가 굉장히 지저분해진다.

   지연로딩 전락(Lazy Loading) 옵션을 사용한다.


### **UPDATE**

```java
/** 1. UPDATE, DELETE로 인한 로우(ROW)락 시간 최소화 */

transaction.begin(); // [트랜잭션] 시작

changeMember(memberA);

deleteMember(memberB);

비즈니스_로직_수행(); // 비즈니스 로직 수행 동안 DB 로우 락이 걸리지 않는다.

// 커밋하는 순간 데이터베이스에 UPDATE, DELETE SQL을 보낸다.

/** 2. 트랜잭션 커밋 시 UPDATE, DELETE SQL 실행하고, 바로 커밋 */

transaction.commit(); // [트랜잭션] 커밋
```

1. UPDATE, DELETE로 인한 로우(ROW)락 시간 최소화
2. 트랜잭션 커밋 시 UPDATE, DELETE SQL 실행하고, 바로 커밋

---

## **1차 캐시와 동일성(identity) 보장 - 캐싱 기능**

같은 트랜잭션 안에서는 같은 엔티티를 반환 - 약간의 조회 성능 향상 (크게 도움 X)

```java
    String memberId = "100";

    Member m1 = jpa.find(Member.class, memberId); // SQL

    Member m2 = jpa.find(Member.class, memberId); // 캐시 (SQL 1번만 실행, m1을 가져옴)

    println(m1 == m2) // true
```

결과적으로, SQL을 한 번만 실행한다.

DB Isolation Level이 Read Commit이어도 애플리케이션에서 Repeatable Read 보장

## 지연 로딩(Lazy Loading)

객체가 실제로 사용될 때 로딩하는 전략

![https://media.vlpt.us/images/adam2/post/c34d236e-6375-40c3-86a9-211dcda2c0e3/Untitled%209.png](https://media.vlpt.us/images/adam2/post/c34d236e-6375-40c3-86a9-211dcda2c0e3/Untitled%209.png)

memberDAO.find(memberId)에서는 Member 객체에 대한 SELECT 쿼리만 날린다.

Team team = member.getTeam()로 Team 객체를 가져온 후에 team.getName()처럼 실제로 team 객체를 건드릴 때!

즉, 값이 실제로 필요한 시점에 JPA가 Team에 대한 SELECT 쿼리를 날린다.

Member와 Team 객체 각각 따로 조회하기 때문에 네트워크를 2번 타게 된다.

Member를 사용하는 경우에 대부분 Team도 같이 필요하다면 즉시 로딩을 사용한다.

## **즉시 로딩**

JOIN SQL로 한 번에 연관된 객체까지 미리 조회하는 전략

![https://media.vlpt.us/images/adam2/post/a4818fa8-c7cc-49c4-9329-df5a6a200e7f/Untitled%2010.png](https://media.vlpt.us/images/adam2/post/a4818fa8-c7cc-49c4-9329-df5a6a200e7f/Untitled%2010.png)

Join을 통해 항상 연관된 모든 객체를 같이 가져온다.

애플리케이션 개발할 때는 모두 지연 로딩으로 설정한 후에, 성능 최적화가 필요할 때에 옵션을 변경하는 것을 추천한다.