# JPA를 왜 사용해야 할까

---

1. sql 중심적인 개발에서 객체 중심적인 개발이 가능하다.

   sql 코드의 반복, 객체지향과 관계지향 데이터베이스의 페러다임 불일치

   Object -> [SQL 변환] -> RDB에 저장[개발자 == SQL 매퍼] 라고 할만큼 SQL 작업을 너무 많이 하고 있다.

2. 생산성이 증가


    간단한 메소드로 CRUD가 가능하다

3. 유지보수가 쉽다기존: 필드 변경 시 모든 SQL을 수정해야 한다.JPA: 필드만 추가하면 된다. SQL은 JPA가 처리하기 때문에 손댈 것이 없다.

1. Object와 RDB 간의 패러다임 불일치 해결

[[JPA] JPA를 사용하는 이유 - Heee's Development Blog](https://gmlwjd9405.github.io/2019/08/03/reason-why-use-jpa.html)