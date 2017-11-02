# NODEJS - DAY6

## HTTP CACHE
### CACHE
- 무기등의 은닉처
- 은닉하다

> 컴퓨터 분야에서의 캐시는 `데이터를 미리 복사해 놓는 임시 저장소`, 혹은 `그 임시 저장소에 데이터를 저장하는 행위`를 가리킴`(주로 접근속도의 개선을 위해)`

`컴퓨터의 아주많은 부분(CPU, GPU, HDD, 네트워크, 웹, 디비)에서 사용됨`

### HTTP CACHE
자원의 효율적 로딩을 위한 웹 표준
- 서버에서 가져온 자원(HTML, CSS, JS, 이미지,...)를 가까운 곳(브라우저, 다른서버)에 저장해놓고 재사용
- 캐시를 할 것인지 말것인지, 어떻게 할 것인지를 결정하는 규칙이 복잡하고 브라우저마다 조금씩 다르다.

### COMMOM PROBLEM
`캐시된 자원`과 `실제 자원`의 내용이 달라지는 문제를 어떻게 해결할 것인가?

### SOLUTION
- EXPIRATION(만료)
  - 정해진 시간이 지나면 `캐시가 자동으로 삭제`되도록 설정
- VALIDATION(검증)
  - 서버에 요청을 보내서 `캐시를 계속 사용할 수 있는지 확인`
  - 복사본 캐시와 실제 자원의 내용이 다른지를 확인

### CACHE 관련 헤더
[CACHE 범주](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers#Caching)
[CONDITIONALS 범주](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers#Conditionals)

- `cache-control`
  - `요청과 응답`에 포함되는 헤더
  - 캐시와 관련된 다양한 기능을 하는 지시자를 포함
  - no-cache, max-age가 많이 사용된다.
  - no-cache, max-age=0 지시자는 캐시를 사용하지 않도록하거나, 캐시를 아직도 쓸 수 있는지 검증하기 위해 사용된다.
- `ETag`
  - `응답`에 포함되는 헤더
  - 캐시의 검증을 위해 사용되는 자원의 식별자
  - 주로 자원의 해시값이 사용되지만, 마지막으로 수정된 시각, 혹은 버전 넘버를 사용하기도 한다.
- `Expires`
  - `응답`에 포함되는 헤더
  - 캐시를 만료시킬 시각을 서버에서 명시적으로 지정
- `Last-modified`
  - `응답`에 포함되는 헤더
  - 원래 자료가 마지막으로 수정된 시각
- `if-None-Match`
  - `요청`에 포함되는 헤더
  - 검증을 위해 사용된다.
  - 이전에 저장해두었던 자원의 `Etag값을 if-none-match헤더의 값으로 요청에 포함시켜서 보내면`, 서버는 해당 경로에 있는 자원의 `Etag와 비교해보고 자원의 전송여부를 결정`
- `If-None-Match`
  - 요청에 포함되는 헤더
  - 검증을 위해 사용된다.
  - 이전에 저장해두었던 자원의 `last modified값을 if-modified-since헤더의 값으로 요청에 포함시켜서 보내면` 서버는 해당경로에 있는 자원의 `Last-modified`와 `비교해보고 자원의 전송여부를 결정`

## GRAPHQL

## SINGLE-PAGE APPLICATION

[github 예제](https://github.com/suhyeon/simple-todo-spa)