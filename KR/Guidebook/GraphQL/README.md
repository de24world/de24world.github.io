
[GraphQL 알아보기] 
======================

* 관련 참조 문서   
  - [REST API vs GraphQL 차이점](https://github.com/de24world/the-classic-of-development/blob/main/KR/Guidebook/RESTful%26GraphQL/README.md)
  - [GraphQL 알아보기](https://github.com/de24world/the-classic-of-development/tree/main/KR/Guidebook/GraphQL)

---

# GraphQL 는?
* GraphQL은 `API`를 위한 쿼리 언어이며 이미 존재하는 데이터로 쿼리를 수행하기 위한 런타임 입니다. GraphQL은 API에 있는 데이터에 대한 완벽하고 이해하기 쉬운 설명을 제공하고 클라이언트에게 필요한 것을 정확하게 요청할 수 있는 기능을 제공하며 시간이 지남에 따라 API를 쉽게 진화시키고 강력한 개발자 도구를 지원합니다.

`API(Application Programming Interface)란?`: API는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 `인터페이스`를 뜻한다.   
`인터페이스(Interface)란?` : 인터페이스(interface)는 컴퓨터 시스템끼리 정보를 교한하는 공유 경계를 의미한다, 터치 스크린과 같은 일부 컴퓨터 하드웨어 장치들은 인터페이스를 통해 데이터를 송수신 할 수 있으며, 마우스나 마이크론 폰가 같은 장치들은 오직 시스템에 데이터를 전송만 하는 인터페이스를 제공한다.

# GraphQL 특징?

1. 필요한 것을 구체적으로 요청하세요
API에 GraphQL 쿼리를 보내고 필요한 것만 정확히 얻으세요. GraphQL 쿼리는 항상 예측 가능한 결과를 반환합니다. GraphQL을 사용하는 앱은 서버가 아닌 데이터를 제어하기 때문에 빠르며 안정적입니다.   
<img src="/KR/Guidebook/GraphQL/sample1.gif" alt="GraphQL_query" title="GraphQL_query"></img>

2. 단일 요청으로 많은 데이터를 얻으세요
GraphQL 쿼리는 하나의 리소스 속성에 액세스할 뿐만 아니라 이 리소스 간의 참조를 자연스럽게 이해합니다. 일반적인 REST API는 여러 URL에서 데이터를 받아와야 하지만 GraphQL API는 한번의 요청으로 앱에 필요한 모든 데이터를 가져옵니다. GraphQL을 사용하는 앱은 느린 모바일 네트워크 연결에서도 빠르게 수행할 수 있습니다.   
<img src="/KR/Guidebook/GraphQL/sample2.gif" alt="GraphQL_query2" title="GraphQL_query2"></img>

3. 타입 시스템으로 가능한 것을 살펴보세요
GraphQL API는 엔드포인트가 아닌 타입과 필드로 구성됩니다. 단일 엔드포인트에서 데이터의 모든 기능에 접근하세요. GraphQL은 타입 시스템을 사용하여 앱이 가능한 것을 요청하고 명확하고 유용한 오류를 제공하는 것을 보장합니다. 앱은 타입을 사용하여 수동 파싱 코드 작성을 피할 수 있습니다.   
<img src="/KR/Guidebook/GraphQL/sample3.gif" alt="GraphQL_query3" title="GraphQL_query3"></img>

* [GraphQL 한국어 번역 페이지](https://graphql-kr.github.io/)

## GraphQL 기본 요소

1. 쿼리 (Query)
- `CRUD`에서 R(ead)에 속하는 부분으로써, 데이터를 읽는데 사용한다.

* `CRUD(Create, Read, Update and Delete)`? - CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create, Read, Update, Delete를 묶어서 일컫는 말이다. 사용자 인터페이스가 갖추어야 할 기능을 가리키는 용어로서도 사용된다. 


예시
```graphql
# Read Data with Query
query HeroNameAndFriends {
  hero {
    name
    friends {
      name
    }
  }
}


# return Data 
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "friends": [
        {
          "name": "Luke Skywalker"
        },
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        }
      ]
    }
  }
}
```

2. 뮤테이션 (Mutation)
- `CRUD`에서 (Create, Update, Delete) 속하는 부분으로써, 데이터를 변조한다.

예시
```graphql
# create Data with Mutation
mutation CreateReviewForEpisode($ep: Episode!, $review: ReviewInput!) {
  createReview(episode: $ep, review: $review) {
    stars
    commentary
  }
}


# variables
{
  "ep": "JEDI",
  "review": {
    "stars": 5,
    "commentary": "This is a great movie!"
  }
}

# return
{
  "data": {
    "createReview": {
      "stars": 5,
      "commentary": "This is a great movie!"
    }
  }
}
```


3. 스키마/타입(Schema/Type)
- 쿼리 & 뮤테이션이 요청한 데이터의 구조를 미리 결정해둔다.

Schema
```graphql
# 오브젝트 타입과 필드
schema {
  query: Query
  mutation: Mutation
}
```
* 모든 GraphQL 서비스는 query 타입을 가지며 mutation 타입은 가질 수도 있고 가지지 않을 수도 있습니다. 이러한 타입은 일반 객체 타입과 동일하지만 모든 GraphQL 쿼리의 진입점(entry point) 을 정의하므로 특별합니


Type
```graphql
# 오브젝트 타입과 필드
type Character {
  name: String!
  appearsIn: [Episode!]!
}
```
* 오브젝트 타입 : Character
* 필드 : name, appearsIn
* 스칼라 타입 : String, ID, Int 등
* 느낌표(!) : 필수 값을 의미(non-nullable)
* 대괄호([, ]) : 배열을 의미(array)

4. 리졸버(resolver)
- 쿼리 & 뮤테이션이 요청한 데이터에 대한 응답 방식을 결정한다. (함수)


---
## ○ 참조 문서 및 사이트
* [GraphQL 튜토리얼 동영상](https://www.howtographql.com/basics/0-introduction/)
* [GraphQL 개념잡기](https://tech.kakao.com/2019/08/01/graphql-basic/)
