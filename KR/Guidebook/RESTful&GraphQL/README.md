
[REST API vs GraphQL 차이점] 
======================

* 관련 참조 문서   
  - [REST API vs GraphQL 차이점](https://github.com/de24world/the-classic-of-development/blob/main/KR/Guidebook/RESTful%26GraphQL/README.md)
  - [GraphQL 알아보기](https://github.com/de24world/the-classic-of-development/tree/main/KR/Guidebook/GraphQL)

---

# REST(ul) API vs GraphQL?
* GraphQL은 REST API에 대안으로 페이스북에서 만든 데이터 전송방식. GraphQL은 `API`를 위한 쿼리 언어이며 이미 존재하는 데이터로 쿼리를 수행하기 위한 런타임 입니다. GraphQL은 API에 있는 데이터에 대한 완벽하고 이해하기 쉬운 설명을 제공하고 클라이언트에게 필요한 것을 정확하게 요청할 수 있는 기능을 제공하며 시간이 지남에 따라 API를 쉽게 진화시키고 강력한 개발자 도구를 지원합니다.

## REST API 란?
* Representational State Transfer의 약자로 좁은 의미로 HTTP Method(post, get, put, delete)를 통해 CRUD를 실행하는 API를 뜻한다. REST API는 그 형식(주소)만으로 대략 이게 무슨 요청인지 알게 해준다.
```
글 관련 API = /posts
글 작성 = POST /posts
글 수정 = PATCH /posts/[postid]
글 삭제 = DELETE /posts/[postid]
댓글 관련 API = /posts/[postid]/comments
댓글 작성 = POST /posts/[postid]/comments
댓글 수정 = PATCH /posts/[postid]/comments/[commentid]
댓글 삭제 = DELETE /posts/[postid]/comments/[commentid]
```
* 즉 RESTful하다라는 것은 REST API의 설계의도를 명확하게 지켜주는 것이다. 슬래시를 통해 계층관계를 표시한다던가 숫자는 id를 나타낸다든가 동사보단 명사를 위주로 쓴다든가 하는 등

## REST API 과 GraphQL의 차이점?
1. GraphQL API는 주로 하나의 Endpoint를 사용한다.
2. GraphQL API는 요청할 때 사용한 Query 문에 따라 응답의 구조가 달라진다.
3. GraphQL API는 유연하다 백엔드에서 지정해놓는 틀이 거이 없기 때문이다.
* GraphQL 은 뷔페 음식, RESTful API는 세트메뉴와 같다. 뷔페는 내가 먹고 싶은 것만 먹을 수 있지만 세트메뉴는 내가 필요하지 않은 것도 들어있다.

## RESTful 장점
* REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일이다.
1. HTTP 프로토콜을 사용하므로 REST API 사용을 위한 인프라를 구축할 필요가 없다.
2. HTTP 표준프로토콜을 따르는 모든 플랫폼에서 호환된다. (범용성)
3. REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
4. 서버와 클라이언트의 역할을 명확하게 분리한다.

## RESTful 단점
1. 표준이 존재하지 않는다.
2. 사용할 수 있는 메소드가 4가지 밖에 없다.
3. 구형의 브라우저가 아직 지원하지 못하는 부분이 존재한다.
4. Overfetcing, 즉 특정 데이터만 불러오고 싶은데 불필요한 데이터가 불러온다.
5. Underfetcing, 즉 Resource 종류 별로 요청을 해야해서 요청횟수가 많아진다.

## GraphQL 장점
1. HTTP 요청 횟수를 줄일 수 있다. - Underfetcing
    * RESTful 은 각 Resource 종류 별로 요청을 해야하고, 따라서 요청 횟수가 필요한 Resource 의 종류에 비례한다.
    * 반면 GraphQL 은 원하는 정보를 하나의 Query 에 모두 담아 요청하는 것이 가능하다.

2. HTTP 응답의 Size 를 줄일 수 있다. - Overfetcing
    * RESTful 은 응답의 형태가 정해져있고, 따라서 필요한 정보만 부분적으로 요청하는 것이 힘들다.
    * 반면 GraphQL 은 원하는 대로 정보를 요청하는 것이 가능하다.

### 튜토리얼 영상
- [GraphQL is the better REST](https://www.howtographql.com/basics/1-graphql-is-the-better-rest)  

## GraphQL 단점
1. File 전송 등 Text 만으로 하기 힘든 내용들을 처리하기 복잡하다.
2. 고정된 요청과 응답만 필요할 경우에는 Query 로 인해 요청의 크기가 RESTful API 의 경우보다 더 커진다.
3. 재귀적인 Query 가 불가능하다. (결과에 따라 응답의 깊이가 얼마든지 깊어질 수 있는 API 를 만들 수 없다.)

## REST API, GraphQL 선택 기준

### GraphQL
    * 서로 다른 모양의 다양한 요청들에 대해 응답할 수 있어야 할 때
    * 대부분의 요청이 CRUD(Create-Read-Update-Delete) 에 해당할 때
    - 사용 프로젝트 예시 : Data 양이 많은 데이터 앱들(코로나 현황앱, 기상청 기후알림 앱 등), Overfetcing&Underfetcing 피하기 위함

### RESTful
    * HTTP 와 HTTPs 에 의한 Caching 을 잘 사용하고 싶을 때 (GraphQL도 캐싱이 가능하다)
    * File 전송 등 단순한 Text 로 처리되지 않는 요청들이 있을 때
    * 요청의 구조가 정해져 있을 때
    - 사용 프로젝트 예시 : 회원정보(가입 및 로그인)를 caching 해야하는 앱, 혹은 URL 파라미터가 확실한 게시판 앱 등


<img src="/KR/Guidebook/RESTful&GraphQL/GraphQL-vs-REST-Infographic.jpg" alt="GraphQL-vs-REST-Infographic" title="GraphQL-vs-REST-Infographic"></img>



---
## ○ 참조 문서 및 사이트
* [REST API 와 GraphQL](https://velog.io/@bclef25/REST-API-%EC%99%80-graphQL)  
* [REST API, GraphQL 차이점 알아보기](https://velog.io/@djaxornwkd12/REST-API-vs-GraphQL-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
* [REST VS GraphQL - Which Should be Used to Develop a Web API and Why?](https://www.promptbytes.com/blog/rest-vs-graphql-web-api-development)
