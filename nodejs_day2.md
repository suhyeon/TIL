# HTTP 
- 웹브라우저와 웹 서버간의 통신을 위해 개발된 통신규약
- 최근에는 restAPI의 부상과 함께 다른 용도로도 널리 사용됨
  - 모바일 앱 : 서버간 통신
  - 서버 : 서버간 통신
- 80번 포트를 기본으로 사용 
# HTTPS
- HTTP over SSL
- HTTP통신을 암호화해 주고받는 내용을 중간에서 가로챌 수 없도록함
- 443번 포트를 기본으로 사용
# HTTP/2
- 구글의 SPDY프로토콜을 기반으로 2015년에 확정된 새로운 HTTP표준
- 속도개선에 중점을 두고 개발됨
- 반드시 HTTPS를 사용해야 함
- 현재 전체 웹사이트중 16%이상이 사용중
# HTTP 구성요소

## REQUEST & RESPONSE
- 웹 브라우저 또는 다른 클라이언트는 웹서버에 요청을 보냄
- 그에 따라 서버는 클라이언트에 응답을 보냄
- 웹브라우저의 경우, HTML문서 형태의 응답이 오면 해당 문서를 분석한후 문서에 포함된 모든 자원에 대한 요청을 각각 추가로 보냄
  - 이미지, 동영상, 오디오, CSS, JS, 폰트...

### REQUEST METHODS
- `HTTP명세에는 8종류`가 등록
- 각각의 역할과 충족해야 하는 성질이 명시되어 있다.
- 웹 브라우저는 `특정상황에서 특정 메소드로 요청을 보내도록 만들어져 있다.`
- AJAX와 같이 `요청을 보내는 코드를 직접 짤 때`는 요청 메소드를 선택할 수 있다.
- `자료의 본문을 요청하는 GET메소드`와 `새로운 자료를 등록하는 POST 메소드`가 가장 많이 쓰임

#### 서버가 충족시켜야 하는 메소드의 성질
- SAFE
  - 요청이 서버의 상태에 영향을 미치지 않아야 한다.
  - 읽기 전용이어야 한다.
- IDEMPOTENT
  - 여러번 같은 요청을 해도 한번 요청한 것과 같은 효과여야 한다.
  - 네트워크가 불안정해도 안전하게 요청을 보낼 수 있다.
- CACHEABLE
  - 특정 조건을 만족하면 응답을 클라이언트에 저장해두었다가 다음번 요청때 다시 쓸 수 있다.
[반드시 이성질을 따르도록 서버를 구현해야 하는 것은 아니지만, 이대로 구현하는 것이 좋다.](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Summary_table)
> PUT : 지정된 리소스참조를 요청 PAYLOAD로 치환.(통째로 이 리소스로 만들어 달라는 요청)
> PATCH : 리소스의 부분만을 수정하는데 쓰인다.

- URL HTTP ANATOMY
[URL HTTP ANATOMY](https://httpbin.org/get)

---

# PERCENT ENCODING
- URL은 ASCII문자밖에 사용하지 못하기 때문에, NON-ASCII코드를 위한 표현방법이 필요하다.
- PERCENT ENCODING : NON-ASCII코드를 위한 웹 표준 인코딩 방법으로, JAVASCRIPT에 관련 기능이 포함되어 있다.
```javascript
> encodeURIComponent("한글")
"%ED%95%9C%EA%B8%80"
> decodeURIComponent("%ED%95%9C%EA%B8%80")
"한글"
```

# REQUEST TARGET
일반적인 경우 아래와 같은 구조가 사용된다.
- absolute path + query string + fragment id
```javascript
GET /path/to/resource?foo=bar&spam=hoge#fragid HTTP/1.1
```

# response status
응답의 성공, 실패 여부와 종류를 나타내며, 상태 코드 + 상태 메시지의 형태로 응답에 포함됨
```javascript
HTTP/1.1 200 OK
```
[http status code](https://httpstatuses.com/)

- Status Category
  - 200~
    - 성공
  - 300~
    - 추가 작업이 필요함
  - 400~
    - 실패 - 클라이언트 책임
  - 500~ 
    - 실패 - 서버 책임
- code 200~
  - 200 OK
    - 성공
  - 201 created
    - 자료가 성공적으로 생성됨
- code 300~
  - 301 moved permanently(redirection)
    - 자료가 완전히 다른 곳으로 이동했음
  - 302 found(redirection)
    - 자료가 일시적으로 다른곳에 있음
  - 304 not modified(cache)
    - 클라이언트가 이미 가지고 있던 자료가 수정되지 않았다.(그대로 사용하면 됨)
- code 400~
  - 400 bad request
    - 요청의 형태가 잘못되어 응답할 수 없음
  - 403 forbidden
    - 요청한 자료에 접근할 권한이 없다.
  - 404 not found
    - 요청한 자료가 없음
  - 418 i am teapot
    - 만우절 장난 프로토콜ㅋㅋ
- code 500~
  - 500 internal server error
    - 요청을 처리하던중 예상치 못한 오류가 발생
  - 503 service unavailable
    - 서버가 일시적으로 응답할 수 없음

---
# HEADER
- 요청과 응답에 대한 추가정보를 표현하는데 사용됨
- 인증, 캐싱, 쿠키, 보안, 내용 협상, 프록시 등 웹 표준에 정의된 많은 기능을 제어하는데 사용됨

- Authorization
  - 요청의 인증정보
- user-agent
  - 요청중인 클라이언트의 정보
- location
  - 301, 302 응답에서 자료의 위치
- accept
  - 요청이 어떤 형태의 자료를 원하는지 나타냄
- content type
  - 요청 혹은 응답이 어떤 형태의 자료인지 나타냄

> content Negotiation
: 요청의 Accept, Accept-language등의 헤더를 보고 서버가 그에 맞는 형태의 자료를 응답하는 절차를 content negotiation(내용협상)이라고 한다.

---
# EXPRESS 준비단계
Glitch는 웹 브라우저 위에서 Node.js 기반 앱을 만들고, 복제하고, 편집하고, 공동 작업하고, 호스팅할 수 있는 환경을 제공합니다.  
이 앱은 seungha-kim의 소유로, 방문자가 편집할 수 없는 상태입니다.  
이 프로젝트를 편집하고 싶다면 소유자에게 편집 권한을 받거나,  
이 프로젝트를 복제해서 당신이 소유하는 새 프로젝트를 만들어야 합니다.  
이것을 이용해서 EXPRESS 실습을 한다.
[glitch 실습 나만의 url](https://suhyeon-crayon.glitch.me)

## EXPRESS
- NODEJS 생태계에서 가장 널리 쓰이는 웹 프레임 워크
- 내장하고 있는 기능은 매우 적으나, 미들웨어를 주입하는 방식으로 기능을 확장하는 생태계를 가지고 있다.
[공식 매뉴얼 한국어 번역](https://expressjs.com/ko/)

### EXPRESS 앱의 기본구조
```javascript
// Express 인스턴스 생성
const app = express()

// 미들웨어 주입
app.use(sessionMiddleware())
app.use(authenticationMiddleware())

// 라우트 핸들러 등록
app.get('/', (request, response) => {
  response.send('Hello express!')
})

// 서버 구동
app.listen(3000, () => {
  console.log('Example app listening on port 3000!')
})
```

### Routing
```javascript
// HTTP 요청 메소드(GET, POST, ...)와 같은 이름의 메소드를 사용
app.get('/articles', (req, res) => {
  res.send('Hello Routing!')
})
// 특정 경로에만 미들웨어를 주입하는 것도 가능
app.post('/articles', bodyParserMiddleware(), (req, res) => {
  database.articles.create(req.body)
    .then(() => {
      res.send({ok: true})
    })
})
// 경로의 특정 부분을 함수의 인자처럼 입력받을 수 있음
app.get('/articles/:id', (req, res) => {
  database.articles.find(req.params.id) // `req.params`에 저장됨
    .then(article => {
      res.send(article)
    })
})
```

### request 객체
- req.body
  - 요청바디를 적절한 형태의 자바스크립트 객체로 변환해 이곳에 저장(body-parser 미들웨어에 의해 처리됨)
- req.ip
  - 요청한 쪽의 ip
- req.params
  - route parameter
- req.query
  - query string 이 객체로 저장됨

### response 객체
- res.status(...)
  - 응답의 상태코드를 지정하는 메소드
- res.append(...)
  - 응답의 헤더를 지정하는 메소드
- res.send(...)
  - 응답의 바디를 지정하는 메소드 인자에 따라 달리 응답
    - 텍스트 이면 text/html 
    - 객체이면 ,application/json타입으로 응답

[실습 코드](https://glitch.com/edit/#!/wealthy-stallion?path=server.js:58:12)
```javascript
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

// GET method
app.get('/', (req, res) => {
  res.send('Hello, Express!')
})

// POST method
app.post('/', bodyParser.json(), (req, res) => {
  if(req.body.name){
    res.send(`Hello,${req.body.name}!`);  
  }else{
    res.status(400);
    res.send('400 Bad Request');
  }
  /*
  Mission:
  요청의 바디에 실려 온 JSON에 name이라는 속성이 있으면 해당 값을 이용해 응답하고, 없으면 400 Bad Request를 응답한다.
  응답 형태는 'Hello, <name>!' 으로 한다. 
  */
})

// query parameter, res.status
app.get('/add', (req, res) => {
  try{
     let x = parseInt(req.query.x);
     let y = parseInt(req.query.y);  
     const result = (x+y).toString(); //숫자를 send하면 안된다.
    res.send(result);
  }catch(e){
    res.status(400);
    res.send('400 Bad Request');
  }
  /* 
  Mission: 
  query parameter에 x와 y라는 이름을 가진 두 값을 정수로 바꾸어서 더한 후 응답한다.
  값을 정수로 바꿀 수 없다면 400 Bad Request로 응답한다.
  */
});

// req.ip
app.get('/ip', (req, res) => {
  res.send(req.ip);
  /*
  Mission: 
  요청한 쪽의 ip를 응답한다.
  */
})

// req.get, res.set, res.end
app.get('/header', (req, res) => {
  const value= req.get('X-Custom-Header');
  res.append('X-Custom-Header',value);//기존에 있어도 안덮어쓴다
  //res.set('X-Custom-Header', value); //기존에 있으면 덮어쓴다.
  res.end();
  /*
  Mission:
  요청의 X-Custom-Header 헤더를 그대로 응답에 포함시켜 응답한다.
  응답에는 바디를 포함시키지 않도록 한다.
  
  hint 1: res.set 메소드는 응답에 새로운 헤더를 지정한다.
  예) res.set('X-Custom-Header', value)
  
  hint 2: res.end 메소드는 응답을 보낸다. res.send와 비슷하지만, 바디를 인자로 받지 않는다.
  */
})

const listener = app.listen(process.env.PORT, function () {
  console.log('listening on port ' + listener.address().port)
})
```

---
# TEMPLATE LANGUAGE
## STATIC WEB PAGE
누가 어떻게 요청하든 미리 저장되어 있던 HTML 파일을 그대로 응답
## DYNAMIC WEB PAGE
요청한 사람과 요청한 내용에 따라 각각 다른 내용으로 편집 한 HTML을 응답

### 웹 초창기 - CGI
```c
int main(void)
{
  char *data;
  long m,n;
  printf("%s%c%c\n", "Content-Type:text/html",13,10);
  printf("<TITLE>Multiplication results</TITLE>\n");
  printf("<H3>Multiplication results</H3>\n");
  data = getenv("QUERY_STRING");
  if(data == NULL)
    printf("<P> Error in passing data from form to script.");
  else if(sscanf(data,"m=%ld&n=%ld",&m,&n)!=2)
    printf("<P>Error! Invalid data. Data must be numeric.");
  else
    printf("<P>The product of %ld and %ld is %ld.",m,n,m*n);
  return 0;
}
```
## TEMPLATE ENGINE
템플릿과 데이터를 결합해 문서를 생성하는 프로그램, 혹은 라이브러리
> 템플릿을 작성할 때 사용하는 언어를 템플릿 언어라 한다.

### EJS
EMBADDED JAVASCRIPT TEMPLATE
- NODE.JS 생태계에서 가장 많이 사용되는 템플릿 엔진
- 문법이 단순하다
- JAVASCRIPT 코드를 템플릿안에서 그대로 쓸 수 있다.

[.EJS VSCODE Extension](https://marketplace.visualstudio.com/items?itemName=QassimFarid.ejs-language-support)
```javascript
<%# index.ejs %> //ejs 주석태그 , <%=> : 이력서의 빈칸 같은 다른 값을 쓰고 싶을 때
<html>
  <head>
    <title><%= title %></title> 
  </head>
  <body>
    <div class="message">
      <%= message %>
    </div>
    <% if (showSecret) { %>
      <div>my secret</div>
    <% } %>
  </body>
</html>
```
EXPRESS 에서 EJS 사용하기
- EJS 설치
  - $ npm install --save ejs
- template engine 설정
  - app.set('view engine','ejs')
- res.render()
```javascript
const data = {
  title: 'Template Language',
  message: 'Hello EJS!',
  showSecret: true
}
res.render('index.ejs', data)
```

### EJS 예제

#### 템플릿 태그

- <% ... %>: 템플릿의 구조를 제어하기 위해 사용하며, 문자열을 내놓지 않습니다.
- <%= ... %>: 내부의 식을 문자열로 변환해 HTML 문서 안에 삽입합니다.
- <%# ... %>: EJS 주석입니다. HTML 주석과는 다르게 아예 HTML 문서에 포함되지 않습니다.

```javascript
const express = require('express')

const app = express()

// 템플릿 엔진을 ejs로 설정해줍니다.
app.set('view engine', 'ejs')

app.get('/', (req, res) => {
  // 템플릿에서 사용할 데이터입니다.
  // 배열에 요소를 추가하고, true를 false로 바꾸고, 텍스트를 변경해보세요
  const data = {
    items: ['one', 'two', 'three'],
    showSecret: true,
    secret: 'I LOVE NODE.JS!',
    name: req.query.name
  }
  // res.render 함수는 views 디렉토리에 있는 템플릿 파일과 데이터를 합쳐서 응답을 보냅니다.
  res.render('index.ejs', data)
})

app.listen(3000, function() {
  console.log('listening...')
})
 
```

#### Serving Static Files
```javascript
// `public` 폴더에 있는 파일을 `/static` 경로 아래에서 제공
app.use('/static', express.static('public'))

<!-- 템플릿 파일에서 참조할 수 있음 -->
<link rel="stylesheet" href="/static/index.css">
<script type="text/javascript" src="/static/index.js"></script>
```
[ejs 실습](https://upbeat-pound.glitch.me/profile/suhyeon)