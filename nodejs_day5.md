# NodeJs - DAY5
## AJAX
`비동기적인 웹 어플리케이션`의 제작을 위한 `클라이언트 측 웹 개발 기법`
> 요즘은 의미가 변형되어 `웹브라우저에서 xmlHttpRequest` 혹은 `fetch`를 이용해서 보내는` HTTP 요청`을 통칭하기도 함

### 장점
- 화면 전체를 다시 로드하지 않고도 내용을 갱신할 수 있어 더 나은 사용자 경험 제공
- 서버의 응답을 기다리는 동안에도 여전히 웹 어플리케이션을 사용 가능
- 필요한 자원만 서버에서 받아오게 되므로 트래픽이 줄어듬

### 단점
- 클라이언트 구현이 굉장히 복잡해짐

## Axios
- `promise based` HTTP client
- 브라우저와 Node.js 에서 `모두 사용가능`
- XMLHTTPREQUEST, FETCH에 비해 사용하기 편하고 기능이 더 많음

[참고: 내가 FETCH-API를 쓰지 못했던 이유](https://medium.com/little-big-programming/%EB%82%B4%EA%B0%80-fetch-api%EB%A5%BC-%EC%93%B0%EC%A7%80-%EB%AA%BB%ED%96%88%EB%8D%98-%EC%9D%B4%EC%9C%A0-3c23f0ec6b82)

## AXIOS + JSON-SERVER 예제
[예제 GLITCH](https://glitch.com/edit/#!/alike-coin)
```javascript
// GET
axios.get('/api/todos')
  .then(res => {
    prettyPrint(res.data)
  })

// POST
axios.post('/api/todos', {title: "ajax 공부"})
  .then(res => {
    prettyPrint(res.data)
  })

// PATCH
axios.patch('/api/todos/3', {title: "axios 공부"})
  .then(res => {
    prettyPrint(res.data)
  })

// DELETE
axios.delete('/api/todos/3')
  .then(res => {
    prettyPrint(res.data)
  })

// GET/API/TODOS/?TITLE=REACT
// config 객체
axios.get('/api/todos', {
  params: { // query string
    title: 'react 공부'
  },
  headers: { // 요청 헤더
    'X-Api-Key': 'my-api-key'
  },
  timeout: 1000 // 1초 이내에 응답이 오지 않으면 에러로 간주
}).then(res => {
    prettyPrint(res.data)
  })

//응답객체
// config.params
axios.get('/api/todos/1')
  .then(res => {
    console.log(`status code: ${res.status}`)
    console.log('headers:')
    prettyPrint(res.headers)
    console.log('data:')
    prettyPrint(res.data)
  })
```
## 쿠키를 통한 인증 예제
[예제 GLITCH](https://glitch.com/edit/#!/erratic-owner)
```javascript
 
const jsonServer = require('json-server')
const fs = require('fs')
const cookieSession = require('cookie-session')
const bodyParser = require('body-parser')

// json-server의 구성요소들을 생성합니다.
const server = jsonServer.create()
const router = jsonServer.router('.data/db.json')
const middlewares = jsonServer.defaults()

// 쿠키를 glitch에서 사용하기 위해 필요한 설정입니다.
server.set('trust proxy', 1)

// cookie-session 미들웨어를 주입합니다.
server.use(cookieSession({
  name: 'session',
  secret: 'secret'
}))

// json-server가 제공하는 미들웨어를 주입합니다.
server.use(middlewares)

// 사용자 데이터를 관리할 데이터베이스가 필요한데
// json-server로 관리되는 데이터에 접근하기 어렵기 때문에
// 사용자 데이터만 아래와 같이 따로 배열로 관리합니다.
const users = [
  {username: 'fast', password: 'campus'},
  {username: 'node', password: 'js'},
  {username: 'react', password: 'facebook'}
]

// 인증을 위한 라우트 핸들러입니다.
server.post('/auth', bodyParser.json(), (req, res) => {
  const {username, password} = req.body //디스트럭처링
  const matched = users.find(user => user.username === username && user.password === password)
  if (matched) {
    req.session.username = username
    //res.send({ok: true, data: {...}}) 이러한 방법의 코드도 있다.
    res.end()
  } else {
    res.status(400)
    //res.send({ok: false, error: '400 Bad Request'}) 이러한 방법의 코드도 있다.
    res.end()
  }
})

// 로그아웃을 위한 라우트 핸들러입니다.
server.delete('/auth', (req, res) => {
  req.session = null
  res.end()
})

// `/api` 경로의 인증을 담당하는 미들웨어입니다.
function authMiddleware(req, res, next) {
  if (!req.session.username) {
    res.status(401)
    res.send('401 Unauthorized')
  } else {
    next()
  }
}

server.use('/api', authMiddleware, router)

server.listen(3000, () => {
  console.log('JSON Server is running')
})

```
### 막간 팁!!
String -> 정수
- *1
  - undefined * 1 : NaN
  - NaN 판별법
    - isNaN, number.isNaN()사용
- parseInt()
  - 버그를 최대한 줄여줄 수 있다.
  - 에러가 나야하는 상황에서는 에러를 내줘야 좋다.

## CORS
### Same-Origin Policy
동일 출처 정책
- 웹페이지에서 리소스를 불러올 때, `리소스의 출처가 웹페이지의 출처와 같으면 안전`하다고 보고, `출처가 다르면 해당 리소스는 안전하지 않다`고 보는 원칙
- `출처`?
  - `프로토콜 + 도메인 + 포트번호의 결합`을 가리킴
  - `세개가 다 같아야 동일 출처`라고 할 수 있고, 셋중에 하나라도 다르면 동일 출처로 간주되지 않음
- `웹 보안의 기본 원칙`
  - 웹브라우저의 많은 요소에 적용됨

### Same-Origin Policy 실습
```javascript
> const child = window.open('http://www.fastcampus.co.kr')
// 새로 열린 웹 페이지의 콘솔에서
> window.foo = 'bar'
// 이전 웹 페이지의 콘솔에서
> child.foo
// 출처가 같다면 접근 가능, 아니면 불가
```

### Content-Security-Policy
이 헤더를 이용하면, `동일하지 않은 출처에 대한 리소스를 불러올지 말지` 결정할 수 있다.
[링크](https://developers.google.com/web/fundamentals/security/csp/?hl=ko)

## CORS 정의
Cross - Origin Resource Sharing
- `클라이언트 측 cross-origin 요청`을 `안전하게 보낼 수 있는 방법`을 정한 표준
- `스크립트가 전혀 다른 출처를 갖는 API서버를 사용하려고 하는 상황`에선 뭔가 `추가적인 처리`를 해주어야 한다.

## 요청의 위험성
- 가정
  - mywebsite.com 에서 서비스 중인 웹사이트는 mywebsite.com/api에서 rest api를 통해 필요한 정보를 얻는다.
  - api경로에 대한 인증은 쿠키로 이루어진다.
- 만약
  - evil.com 웹사이트의 스크립트에서 mywebsite.com api에 요청을 마음대로 보낼 수 있다면
  - my-website.com도메인에 대해 브라우저에 저장된 쿠키를 이용해서 api를 마음대로 호출할 수 있을 것이다.

## 요청 예제
- IE8이상의 모던 웹 브라우저는 `CROSS-ORIGIN 요청에 대해 여러가지 제한`을 두고 있다.
- CROSS-ORIGIN 요청을 허용하려면,
  - 서버가 특별한 형태의 응답을 전송해야한다.
- 서버가 CROSS-ORIGIN 요청을 허용하지 않으면
  - 웹브라우저는 에러를 발생시킨다.
[예제](https://glitch.com/edit/#!/pewter-motorboat)

### CORS에 관여하는 응답 헤더
- Access-Control-Allow-Origin
  - evel.com은 cros거부, angel.com은 cros허용
- Access-Control-Expose-Headers
- Access-Control-Max-Age
- Access-Control-Allow-Credentials
  - `CROSS-ORIGIN요청에는 기본적으로 포함이 안된다.`
  - 쿠키를 포함시키는 옵션을 줄 수 있다
  - 이 때 CORS요건이 더 엄격해진다.
- Aceess-Control-Allow-Methods
- Acdess-Control-Allow-Headers

### CORS에 관여하는 요청 헤더
- Origin
- Access-Control-Request-Method(preflighted 전용)
- Access-Control-Request-Headers(preflighted 전용)

### CORS - SAFE, UNSAFE
- GET,HEAD 요청
  - SAFE(읽기 전용)
  - 서버에 요청이 도달한다고 해서 서버의 상태에 영향을 미칠 일은 없다.
  - 웹브라우저는 우선 해당요청을 보낸다.
  - 서버가 CROSS-ORIGIN을 허용한다
    - 응답을 그대로 사용
  - 허용하지 않는다.
    - 에러를 낸다.
- POST, PUT, PATCH, DELETE등의 메소드 
  - 서버에 전송되는 것 자체가 위험
    - 실제 요청을 보내기전에 서버가 CORSS-ORIGIN을 허용하는지 알아보기 위해 시험적으로 요청을 한번 보내본다.
  - PREFLIGHTED REQUEST : 시험적으로 요청을 한번 보내보는 요청

> 기존 HTML FORM의 동작 방식 : APPLICATION/X-WWW-FORM-URLENCODED 또는 MULTIPART/FORM-DATA 형태의 POST요청은 PREFLIGHTED REQUEST가 발생하지 않는다.
[다른 원인에 의해 PREFLIGHTED REQUEST 발생 경우](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS#Preflighted_requests)

### 복잡하다면
- 프론트엔드와 API서버를 같은 도메안으로 제공
- 불가피하게 둘은 다른 도메인으로 제공해야 한다.
  - CORS를 허용
    - CORS 미들웨어를 사용하면 간단
  - CORS를 허용했다
    - 쿠키를 쓰지 않는다.

### 쿠키 없이 인증
[ACCESS TOKEN & JWT](https://seungha-kim.github.io/wpsn-handout/2-2-3-jwt.html)

### 쿠키의 단점
- 쿠키를 지원하는 클라이언트에서밖에 사용할 수 없다.
- 적절히 관리 되지 않은 쿠키는 보안에 취약
  - 관리를 하려고 해도 CORS 대응이 복잡하다.

### TOKEN BASED AUTH
- 토큰
  - 사용자의 자격증명을 통해 인증이 이루어진후, 특정자원에 대한 자격증명으로 대신 사용되는 인증수단
- 서버에 요청을 할 때 마다 토큰을 요청에 직접 포함시켜서 전송
  - 주로 AUTHORIZATION헤더에 넣어서 전송

### 토큰 사용의 장점
- 다양한 인증수단의 인증결과를 토큰이라는 하나의 수단으로 통일할 수 있다.
  - 전화번호, 공인인증서, 생체정보
- 쿠키를 사용하지 않음으로
  - CORS관련 문제를 회피할 수 있다.

### 토큰 사용의 단점
- 매 요청에 토큰이 포함되게 되므로 적당히 짧은 길이를 유지
- 토큰 유출에 대한 대비책이 필요
  - 토큰에 유효기간을 두거나, 유출된 토큰을 강제로 무효화하는 등의 방법을 사용
- 쿠키와는 다르게, 클라이언트에서 직접 토큰을 저장하고 관리해야 한다.

### WEB STORAGE
- 브라우저에서 키-값 쌍을 저장할 수 있는 저장소
- 쿠키에 비해 사용하기 편리하고 저장가능한 용량도 크다.(10MB 가량)
- 브라우저 탭이 닫히면 내용이 삭제되는 SESSION STORAGE, 브라우저 탭이 닫혀도 내용이 유지되는 LOCAL STORAGE가 있다.

### 보안상 주의사항
- 토큰을 LOCALSTORAGE에 저장하게 되면 자바스크립트로 토큰을 탈취할 수 있게 되므로 XSS에 노출되지 않도록 신경써야 한다.
- 직접 DOM API를 사용하는 대신 EJS, REACT같은 템플릿 언어를 사용하기만 해도 XSS에 대한 방어는 충분

### JSON WEB TOKEN
- 최근 널리 사용되고 있는 토큰 형식의 표준
- 토큰 안에 JSON 형식으로 정보를 저장
- 보안을 위해 서명 또는 암호화를 사용할 수 있다.
[JWT.IO](https://jwt.io/)

#### JWT 예제 실습
[실습 코드](https://glitch.com/edit/#!/dazzling-zinc)
```javascript
const express = require('express')
const bodyParser = require('body-parser')

/** 
 * JWT의 사용을 위해 두 패키지가 필요합니다.
 * jsonwebtoken: JWT의 생성과 검증을 위한 범용 패키지입니다. 여기에서는 JWT 생성을 위해 사용하고 있습니다.
 * express-jwt: JWT가 요청에 포함되어 서버에 들어왔을 때, 해당 토큰을 검증 및 변환해서 `req.user`에 저장해주는 express 미들웨어입니다.
 */
const jwt = require('jsonwebtoken')
const expressJwt = require('express-jwt')


// 토큰의 서명을 위해 필요한 비밀 키를 저장해둡니다.
const SECRET = 'mysecret'

const app = express()
const jsonMiddleware = bodyParser.json()

app.use(express.static('public'))

/**
 * 인증 미들웨어 생성
 * 
 * `expressJwt()`로 생성된 미들웨어의 기능은 다음과 같습니다.
 *
 * 1. `Authorization: Bearer <token>` 형태로 jwt가 들어왔는지 검사하고
 * 2. 토큰이 없으면 401 Unauthorized 응답을 보낸다.
 * 3. 토큰이 있으면 토큰에 들어있는 JSON 정보를 객체로 변환한 후 `req.user`에 저장한다.
 *
 * 미들웨어 생성 시에 서명에 필요한 secret을 전달해 줍니다.
 */
const authMiddleware = expressJwt({secret: SECRET})

const users = [
  {
    username: 'fast',
    password: 'campus',
    isAdmin: true
  },
  {
    username: 'foo',
    password: 'bar'
  }
]

/**
 * `/auth` 경로로 들어온 사용자 이름과 비밀번호를 users 배열과 대조한 후
 * 일치하는 계정이 있다면 해당 계정 정보를 가지고 JWT 토큰을 만들어서 응답한다.
 */
app.post('/auth', jsonMiddleware, (req, res) => {
  const {username, password} = req.body
  const matched = users.find(user => user.username === username && user.password === password)
  if (matched) {
    // `jwt.sign` 메소드는 새로운 JWT 토큰을 생성한다.
    // 토큰에 넣을 객체와 서명에 필요한 secret을 전달한다.
    const token = jwt.sign({username, isAdmin: matched.isAdmin}, SECRET)
    res.send({
      ok: true,
      token
    })
  } else {
    // 일치하는 계정이 없으면 400 응답
    res.status(400)
    res.send({
      ok: false,
      error: 'No matched user'
    })
  }
})

/**
 * 토큰에 들어있는 정보를 그대로 반환하는 라우트 핸들러
 */
app.get('/auth', authMiddleware, (req, res) => {
  res.send(req.user)
})

/**
 * JWT로 인증이 된 요청만 API를 사용할 수 있게 해준다.
 */
app.get('/some-api', authMiddleware, (req, res) => {
  res.send({
    ok: true,
    message: 'Hello JWT!'
  })
})

let count = 0
app.post('/count', authMiddleware, (req, res) => {
  count += 1
  res.send({
    ok: true,
    count
  })
})

app.listen(3000, () => {
  console.log('listening...')
})

```
## FETCH API
- 웹브라우저의 xmlHttpRequest를 대체하기위해 만들어진 새로운 http client표준
- 비교적 최근에 도입되었다
  - IE및 구형 안드로이드 브라우저는 지원하지 않는다.
- [FETCH POLYFILL](https://github.com/github/fetch)
- [ISOMORPHIC-FETCH](https://www.npmjs.com/package/isomorphic-fetch)

### AXIOS VS FETCH API
- FETCHAPI
  - INSTANCE와 같은 설정을 재사용하거나 요청중인 연결을 취소하는 편의기능이 없다.
  - SERVICE WORKER를 사용하려면 FETCHAPI를 사용해야 한다.
- AXIOS
  - 현재의 가장 좋은 선택
  - 내부적으로 XMLHTTPREQUEST를 사용하고 있다.
  - SERVICE WORKER등의 웹최신 기술이 XMLHTTPREQUEST를 지원하지 않는다.
 
### FETCH API 멋있는것!!
[링크](http://hacks.mozilla.or.kr/2015/05/this-api-is-so-fetching/)