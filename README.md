# Kotlin - Springboot 게시판 서비스
---

## 1. 프로젝트 정보
>(1) 개발환경
>>- Intellij IDEA Ultimate
>>- SpringBoot 3.3.1
>>- Kotlin 1.9.24 (JVM 21)
>>- Gradle
>>- jar

>(2) Dependencies
>>- Web
>>- JPA
>>- MySQL
>>- h2
>>- Kotlin JDSL
>>- Kotest
>>- Ktlint
>>- Swagger

>(3) Project Package
>>- Group : com.kotlinspring
>>- Artifact : board
>>- Package : com.kotlinspring.board
>>- Github : https://github.com/mykim8710/kotlin-springboot-board
---

## 2. 요구사항 정의 및 API
>(1) 전체 기능 목록
>>- 게시글 생성/수정
>>>- [생성] 제목, 작성자, 내용을 입력한다.
>>>- [생성] 정상 생성시 게시글 id를 반환한다.
>>>- [수정] 작성자가 동일하지 않으면 (수정할수 없는 게시물) 예외가 발생한다.
>>>- [수정] 제목, 수정자, 내용을 입력한다. (게시글 id)
>>>- [수정] 정상 수정시 게시글 id가 반환한다.
>>- 게시글 삭제
>>>- 삭제시 id, 작성자를 입력한다.
>>>- 작성자가 동일하지 않으면 (삭제할 수 없는 게시물) 예외가 발생한다.
>>>- 정상 삭제시 게시글 id가 반환한다.
>>- 게시글 상세 조회
>>>- 조회 시 게시글 id를 입력한다.
>>>- 조회 결과 ID, 제목, 작성자, 작성 시간, 내용을 반환한다.
>>- 게시글 목록 조회
>>>- 조회 시 제목, 작성자로 검색할 수 있다. : Search
>>>- 조회 결과 ID, 제목, 작성자, 작성시간의 페이지를 반환한다. : Pagination
>>>- 조회 결과는 작성시간의 역순으로 정렬된다. : Sort

>(2) API
>>- 게시글 생성/수정
>>```
>>[POST] /api/posts
>>
>>request
>>{
>>    "title" : "",
>>    "content" : "",
>>    "createdBy" : "",
>>}
>>
>>response
>>{
>>    "status" : HttpStatus.OK
>>    "code" : 200
>>    "message" : "",
>>    "data" : 1L  // postId
>>}
>>
>>[PUT] /api/posts/{id}
>>request
>>{
>>     "title" : "",
>>     "content" : "",
>>     "updatedBy" : "",
>>}
>>
>>response
>>{
>>     "status" : HttpStatus.OK
>>     "code" : 200
>>     "message" : "",
>>     "data" : 1L  // postId
>>}
>>```
>>- 게시글 삭제
>>```
>>[DELETE] /api/posts/{id}
>>
>>request
>>{
>>    "createdBy" : "",
>>}
>>
>>response
>>{
>>    "status" : HttpStatus.OK
>>    "code" : 200
>>    "message" : "",
>>    "data" : 1L  // postId
>>}
>>```
>>- 게시글 상세 조회
>>```
>>[GET] /api/posts/{id}
>>
>>response
>>{
>>    "status" : HttpStatus.OK
>>    "code" : 200
>>    "message" : "",
>>    "data" : {
>>        "id" : 1L,
>>        "title" : "",
>>        "createdBy" : "",
>>        "createdAt" : 2024-01-01,
>>    }
>>}
>>```
>>- 게시글 목록 조회
>>```
>>[GET] /api/posts?page=1&size=10&title=aa&createdBy=aa
>>
>>response
>>{
>>    "status" : HttpStatus.OK
>>    "code" : 200
>>    "message" : "",
>>    "data" : [{
>>        "id" : 1L,
>>        "title" : "",
>>        "createdBy" : "",
>>        "createdAt" : 2024-01-01,
>>        },{},{}....]
>>    }
>>```
