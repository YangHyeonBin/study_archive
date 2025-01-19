# Creating a node

Create, match 등의 명령어는 대/소문자 구분 영향 없으므로 원하는대로 편하게 쓰면 됨

만들어져 있는 노드 삭제할 때는
Match (n)
Detach
Delete n
연결 해제하는 명령어를 중간에 넣어주는 거였음!


빈 노드 만들기
Create ()

빈 노드 만들고 바로 리턴하게 하기
Create (n) return n
n은 아무거나 내가 원하는 변수명 쓰면 됨. 다만 이건 db에 저장되는거 아니고 지금 이 명령 내에서만 유효한 문자열임

빈 노드 여러 개 만들기 & 리턴하기
Create (n), (m), (q)
Return n, m


label이 있는 노드 만들기 - : 연산자를 발견하면 라벨 만들어줘? ㅇㅋ 상태가 됨
Create (:Person)
Person 이라는 라벨과 그 라벨을 가진 노드를 생성함
(라벨도 생성..한다고 하긴 애매하지만 여튼 그 라벨을 가진 노드를 생성하는 거고, 브라우저 좌측에 Person 라벨 태그가 추가됨)

Label 있는 노트 만들고 리턴하기
Create (Anne:Person)
Return Anne

여러개의 라벨을 한번에 달아 생성 가능
Create (anne:Person:Employee:Footballer)
Return anne


property가 있는 노드 만들기 - {key: value} 를 이용
Create (n:{name: “Alice”})
Return n

Create (n:Person{name: “Anne”, age: 20})
Return n


Label과 property가 있는 노드 만들기
Create (n:Dancer:Supplier{name:”Li”, age:22})
Return n


여러개의 노드를 생성할 땐 , 로 구분한다고 했지
relationship을 생성할 때도 , 로 구분 가능함
Create (n:Supplier{name: “a”}), (m:Client{name: “b”}), (n)-[:supplied]->(m)
Return n, m

리턴에서는 ()를 안써도 되는데 연결 설정할 땐 써야되는건가
-> 맞음. 연결할 때 () 안쓰면 syntax error
왜?


Asterisk(*) 의 쓰임
Create 하고 이것저것 variable로 만들고 모든 걸 리턴하고 싶을 때,
각 변수명을 나열할 필요 없이 return * 하면 됨
다만, variable로 선언한 것만 전부 리턴한다는 점!

Match (n) return * 으로도 사용 가능함ㅋㅋㅋ


relationship을 나타내는 arrow는 <-[:Follows]- 와 같이 반대방향으로 사용해도 문제 없음
의미에 맞는 방향을 가리키도록 생성하면 된다!

create (p:Person{name: "Peter"}) -[:Married] -> (a:Person{name: "Anne”})
create (p)-[:Has]->(h:Estate{name:"House"}) 
return *
이런식으로 create를 두번 해도 되지만,

create (h:Estate{name:"House"}) <-[r:Has]-(p:Person{name: "Peter"}) -[:Married] -> (a:Person{name: "Anne”})
return *
이렇게 방향을 적절히 설정해서 한줄로 쓸수도 있다는 말임
