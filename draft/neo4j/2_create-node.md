# Creating a node

Create, match 등의 명령어는 대/소문자 구분 영향 없으므로 원하는대로 편하게 쓰면 됨

만들어져 있는 노드 삭제할 때는
match (n)
detach
delete n
연결 해제하는 명령어를 중간에 넣어주는 거였음!


빈 노드 만들기
create ()

빈 노드 만들고 바로 리턴하게 하기
create (n) return n
n은 아무거나 내가 원하는 변수명 쓰면 됨. 다만 이건 db에 저장되는거 아니고 지금 이 명령 내에서만 유효한 문자열임

빈 노드 여러 개 만들기 & 리턴하기
create (n), (m), (q)
return n, m


label이 있는 노드 만들기 - : 연산자를 발견하면 라벨 만들어줘? ㅇㅋ 상태가 됨
create (:Person)
Person 이라는 라벨과 그 라벨을 가진 노드를 생성함
(라벨도 생성..한다고 하긴 애매하지만 여튼 그 라벨을 가진 노드를 생성하는 거고, 브라우저 좌측에 Person 라벨 태그가 추가됨)

Label 있는 노트 만들고 리턴하기
create (anne:Person)
return anne

여러개의 라벨을 한번에 달아 생성 가능
create (anne:Person:Employee:Footballer)
return anne


property가 있는 노드 만들기 - {key: value} 를 이용
create (n:{name: “Alice”})
return n

create (n:Person{name: “Anne”, age: 20})
return n


Label과 property가 있는 노드 만들기
create (n:Dancer:Supplier{name:”Li”, age:22})
return n


여러개의 노드를 생성할 땐 , 로 구분한다고 했지
relationship을 생성할 때도 , 로 구분 가능함
create (n:Supplier{name: “a”}), (m:Client{name: “b”}), (n)-[:supplied]->(m)
return n, m

리턴에서는 ()를 안써도 되는데 연결 설정할 땐 써야되는건가
-> 맞음. 연결할 때 () 안쓰면 syntax error
왜?


asterisk(*) 의 쓰임
create 하고 이것저것 variable로 만들고 모든 걸 리턴하고 싶을 때,
각 변수명을 나열할 필요 없이 return * 하면 됨
다만, variable로 선언한 것만 전부 리턴한다는 점!

match (n) return * 으로도 사용 가능함ㅋㅋㅋ


relationship을 나타내는 arrow는 <-[:Follows]- 와 같이 반대방향으로 사용해도 문제 없음
의미에 맞는 방향을 가리키도록 생성하면 된다!

create (p:Person{name: "Peter"}) -[:Married] -> (a:Person{name: "Anne”})
create (p)-[:Has]->(h:Estate{name:"House"}) 
return *
이런식으로 create를 두번 해도 되지만,

create (h:Estate{name:"House"}) <-[r:Has]-(p:Person{name: "Peter"}) -[:Married] -> (a:Person{name: "Anne”})
return *
이렇게 방향을 적절히 설정해서 한줄로 쓸수도다는 말임

웬만한 관계들은 _ 이용해서 어느 정도 표현 가능할텐데, 좀 많이 uncommon한 관계를 표현하게 됐을 땐 `` 백틱을 이용할 수도 있음
create (a:Person{name: "Anne"}) <-[:`the forgotten friend of`]-(m:Person{name: "Mary"})
return *

relationship은 variable로 만들어서 그 변수를 다른 관계에 또 사용할 순 없는 것인가..
(계속 syntax error남)

return *을 하면 only defined variables가 return 되니까 좀 번거로움. 모두 변수로 선언해줘야 하니까
-> 리턴할 문장? 자체를 변수로 선언할 수도 있음!
create np = (:Supplier{name:'A'})-[:supplied]->(:Client{name:'B'})
return np

create path = (n:Supplier{name: 'A'}),
           (m:Client{name: 'B'}),
           (n)-[:supplied]->(m)
return path 하면 n만 리턴됨 ('A'라는 이름을 가진 노드만)

create p = (n:Supplier{name: 'A'}),
       q = (m:Client{name: 'B'}),
       r =(n)-[:Supplied]->(m)
return p, q, r  하면 위 세개 관련 노드와 관계가 모두 리턴됨