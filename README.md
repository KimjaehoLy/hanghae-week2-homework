# hanghae-week2-homework
hanghae homework week2 / login post like

프로젝트 링크(진행 상황: lv.2)

상태 : 프론트와 백앤드 연결 후 기능 테스트 진행중

진행 : 프로젝트 추가 해야할 사항
* 예외처리
- 전체적인 예외처리
- 에러에 따른 status 전송

* 게시물 삭제시
- 파일 삭제

이후 작업
* test 프로그램 작성


필수과제

전체 공통

프레임워크와 라이브러리의 차이점

Framework(프레임워크)
뼈대나 기반 구조를 뜻하고, 제어의 역전 개념이 적용된 대표적인 기술
소프트웨어에서의 프레임워크는 '소프트웨어의 특정 문제를 해결하기 위해서 상호 협력하는 클래스와 인터페이스의 집합'
이라고 할 수 있으며, 완성된 어플리케이션ㅇ 아닌 프로그래머가 완성시키는 작업을 해야합니다.
객체 지향 개발을 하게 되면서 통합성, 일관성의 부족이 발생되는 문제를 해결할 방법중 하나라고 할 수 있습니다.

Library(라이브러리)
단순 활용가능한 도구들의 집합을 말합니다.
즉, 개발자가 만든 클래스에서 호출하여 사용, 클래스들의 나열로 필요한 클래스를 불러서 사용하는 방식을 취하고 있습니다.

프레임워크와 라이브러리의 차이점
제어 흐름에 대한 주도성이 누구에게/어디에 있는가에 있습니다.
즉, 어플리케이션의 Flow(흐름)를 누가 쥐고 있느냐에 달려 있습니다.
프레임워크는 전체적인 흐름을 스스로가 쥐고 있으며 사용자는 그 안에서 필요한 코드를 짜 넣으며 반면에 라이브러리는 사용자가
전체적인 흐름을 만들며 라이브러리를 가져다 쓰는 것이라고 할 수 있습니다.
다시 말해, 라이브러리는 라이브러리를 가져다가가 사용하고 호출하는 측에 전적으로 주도성이 있으며 프레임워크는 그 틀안에 이미 
제어 흐름에 대한 주도성이 내재(내포)하고 있습니다.
프레임워크는 가져다가 사용한다기보다는 거기에 들어가서 사용한다는 느낌/관점으로 접근할 수 있습니다.

출처: https://webclub.tistory.com/458

코드를 구현할때 예외처리를 위해 무엇을 했나요?
기본적인 기능 작동을 우선 순위를 두고 다양한 사용자 입장에서 불필요한 행위를 진행하지 못 하도록
제어하며 그 행위에 대한 제약을 노출시킵니다.

현재 프로젝트에서는 JWT토큰 방식을 이용한 페이지 접근 제한 또는 로그인 사용자만 가능한 기능 등이 있습니다.


백엔드 공통

Restful이란?
일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
- 'REST API'를 제공하는 웹 서비스를 'RESTful'하다고 할 수 있다.
RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
- 즉, REST원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.

출처 : https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

왜 Restful하게 짜야하나요?

RESTful한 URL
RESTful : https://www.hompage.com/dog/kind/bodercollie/weight/11
Non-RESTful : https://www.hompage.com/dog?kind=bodercollie&weight=11



Restful의 대안은?
GraphQL
- Graph Query Language로 facebook에서 개발한 쿼리 언어
- API를 더욱 빠르고 유연하며 개발자 친화적으로 만들기 위해 설계됨
- 통합 개발 환경 내에 배포될 수도 있음
- REST를 대체할 수 있는 GraphQL은 개발자가 단일 API호출로 다양한 데이터 소스에서 데이터를
  끌어오는 요청을 구성할 수 있도록 지원

Restful하게 짜기 위해 무엇을 고려했나요?

GET, POST, PUT, DELETE



Spring 과제

Entity 설계를 위해 무엇을 하였나요?

연관관계에 근거하여 설명해주세요.


설명 해야할 내용(lv.2)  --프로젝트 진행중--

N + 1 문제와 해결법

연관 관계에서 발생하는 이슈로 연관 관계가 설정된 엔티티를 조회할 
경우에 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 
추가로 발생하여 데이터를 읽어오게 된다. 이를 N + 1 문제라고 한다.

Fetch join
사실 원하는 코드는 select * from Owner left join cat on cat.owner_id = owner 일 것이다.
최적화된 쿼리를 우리가 직접 사용할 수 있다. 하하지만
jpaRepository에서 제공해주는 것은 아니고 JPQL로 작성해야 한다.
@Query("select o from Oner o join fetch o.cats")
List<Owner> findAllJoinFetch();
  
  

레이지 로딩(Lazy Loading), 이거 로딩(Eager Loading)의 원리

레이지 로딩(Lazy Loading)
필요할 때만 계산을 수행합니다. 이전 예에서는 결과 행렬의 요소에 액세스할 때까지 계산을 수행하지 않습니다.

이거 로딩(Eager Loading)
요청하면 모든 작업을 수행합니다. 전형적인 예는 두 행렬을 돕할 때입니다. 모든 계산을 수행합니다.
  
  
설명 해야할 내용(lv.3)  ---미진행---
Unit test와 Integration의 개념, 차이
  
우리 프로젝트의 테스트 커버율
  
Integration test 시나리오
 
설명 해야할 내용(lv.4)  --미진행--
Builder 패턴의 장/단점
