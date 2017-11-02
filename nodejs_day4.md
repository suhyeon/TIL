# NODEJS DAY4 TIL
## 1. EXPRESS MIDDLEWARE
Middleware? 
```javascript
// 미들웨어 = 함수
function helloMiddleware(res, req, next) {
  console.log('hello')
  next()
}

app.use(helloMiddleware)
```
- `함수`
  - 안에서 어떤 작업이든 가능
- request 객체, response객체, `next함수`를 인자로 받음
- request 객체, response객체를 조작해서 기능 구현
- `다음 미들웨어`를 동작시키기 위해 `next함수를 인자 없이 호출`
- `등록된 순서대로` 실행됨
- `등록된 순서도 중요하고, 의존도도 중요하다.`

> app.use
- 미들웨어를 앱 전체에서 동작하도록 주입
```javascript
app.use(helloMiddleware)
```
- 특정 경로에서만 동작하도록 주입
```javascript
app.use('/some-path', helloMiddleware)
```
- 한 번에 여러개 주입
```javascript
app.use(middleware1, middleware2, middleware3, ...)
```

### 1. 미들웨어로 하는일
- 로깅
- http body를 객체로 변환
- 사용자 인증
- 권한 관리

### 2. 미들웨어의 사용이유
- 미들웨어로 할 수 있는 모든 일은 라우트 핸들러에서도 할수 있다.
  - 하지만, 여러 라우터에서 사용해야 하는 기능을 중복 작성하는 불편을 덜기 위해
- `코드를 재사용하기 위해`

### 3. 미들웨어 생태계
[EXPRESS RESOURCE](https://expressjs.com/ko/resources/middleware.html)
[NPM SEARCH](https://www.npmjs.com/search?q=express+middleware)

### 4. 예제
- NEXT 함수
  - 미들웨어: REQ,RES,NEXT함수를 추가로 인자로 받는다.
- NEXT함수를 호출하면 다음 미들웨어로 처리를 넘기는 효과가 있다.
- 만약 미들웨어가 NEXT함수를 호출하지도 않고 응답도 보내지 않으면
  - `클라이언트는 응답을 받지 못한다.`
[예제 GLITCH](https://tangy-dentist.glitch.me/)

### 5. 커링 - 함수를 반환하는 함수
```javascript
function makeAdder(x){
    return function(y){
        return x + y
    }
}
undefined
add = makeAdder(1)
ƒ (y){
        return x + y
    }
add(2)
3
add(3)(4)
7

makeAdder2 = x => y => x+y
x => y => x+y
```

### 6. 미들웨어 vs 라우트 핸들러
- 라우트 핸들러도 미들웨어
- 즉, NEXT함수를 인자로 받는것이 가능
```javascript
app.get('/', (req, res, next) => {
  if (!someCondition) {
    next() // 요청을 처리를 하지 않고 다른 핸들러로 넘김
  } else {
    res.send('hello')
  }
})
```
[404예제](https://glitch.com/edit/#!/join/0469b273-bd2f-4dd4-8a16-02b129284d35)
> 404페이지 에러처리는 가장 마지막에 해주어야한다.

[에러처리 미들웨어](https://expressjs.com/ko/guide/error-handling.html)
>애러가 발생하면 슬랙에 메시지로 연동하거나, 버그스낵서비스를 이용할 수 있다.

- 미들웨어 사용하는 곳에 사용
- 프로젝트 소스 정보를 메소드를 이용해 생성한 후 , app.use로 버그스낵을 사용하면 알아서 서버에서 렌더링을 해준다.

## 2. COOKIE

### 1. 쿠키의 필요성
`개별 클라이언트`의 `여러 요청`에 걸친 `정보의 유지`
- 장바구니
- 로그인/로그아웃
- 방문기록
- ...

> 짤막 팁
> Editor Config : 서로사용하는 editor가 다르기 때문에 어느정도의 형식을 맞춰줄수 있는 확장자

### 2. HTTP Cookie
- `서버가 응답을 통해 웹 브라우저에 저장`하는 이름+값 형태의 정보
- 웹 브라우저는 쿠키를 저장하기 위한 `저장소`를 가지고 있다.
- 저장소는 `자료의 유효기간`과 `접근 권한`에 대한 `다양한 옵션`을 제공

### 3. 쿠키 전송 절차
- 1. 서버는 브라우저에 저장하고 싶은 정보를 응답과 같이 실어보낸다.(SET COOKIE헤더)
```javascript
HTTP/1.1 200 OK
Set-Cookie: cookieName=cookieValue; Secure; Max-Age=60000
...
```
- 2. 브라우저는 같은 서버에 요청이 일어날 때마다 해당 정보를 요청에 같이 실어서 서버에 보낸다. (cookie 헤더)
```javascript
GET / HTTP/1.1
Cookie: cookieName=cookieValue; anotherName=anotherValue
...
```

### 4. Set-Cookie Options
- Expires, Max-Age
  - 쿠키의 지속시간 설정
- Secure
  - HTTPS 를 통해서만 쿠키가 전송되도록 설정
- HttpOnly
  - 자바스크립트에서 쿠키를 읽지 못하도록 설정
- Domain, Path
  - 쿠키의 scope 설정(쿠키가 전송되는 URL을 제한)

### 5. Express + Cookie
- 쿠키읽기
  - req.cookies
  - 요청에 실려온 쿠키가 객체로 변환되어 req.cookies에 저장됨
  - cookie-parser 미들웨어 필요
- 쿠키 쓰기
  - res.cookie(name,value)
  - 쿠키의 생성 혹은 수정

### 6. 쿠키예제
```javascript
const express = require('express')
const cookieParser = require('cookie-parser')

const app = express()

app.set('trust proxy', 1)
app.use(cookieParser())

app.get('/', (req, res) => {
  res.send(req.cookies)
})

app.get('/somePath', (req, res) => {
  res.send(req.cookies)
})

// 별다른 옵션 없이 쿠키를 저장하는 응답을 보냅니다.
app.get('/set', (req, res) => {
  res.cookie('cookieName', 'cookieValue')
  res.redirect('/')
})

// httpOnly 옵션은 해당 쿠키를 자바스크립트에서 접근할 수 없게 합니다.
app.get('/httpOnly', (req, res) => {
  res.cookie('httpOnlyCookie', 'value', {
    httpOnly: true
  })
  res.redirect('/')
})

// secure 옵션은 http 프로토콜을 통한 요청에는 쿠키가 포함되지 않게 합니다. (https로 했을 때만 포함시킴)
app.get('/secure', (req, res) => {
  res.cookie('secureCookie', 'value', {
    secure: true
  })
  res.redirect('/')
})

// maxAge 옵션은 쿠키가 해당 시간이 지났을 때 삭제되도록 합니다.
app.get('/maxAge', (req, res) => {
  res.cookie('maxAgeCookie', 'value', {
    maxAge: 5000
  })
  res.redirect('/')
})

// domain 옵션은 해당 도메인 및 서브도메인으로 쿠키가 전송되도록 합니다.
app.get('/domain', (req, res) => {
  res.cookie('domainCookie', 'value', {
    domain: 'glitch.me'
  })
  res.redirect('/')
})

// path 옵션은 쿠키가 지정된 경로 및 그 하위 경로에 요청이 일어났을 때만 전송되도록 합니다.
app.get('/path', (req, res) => {
  res.cookie('pathCookie', 'value', {
    path: '/somePath'
  })
  res.redirect('/')
})

// 여러 옵션을 한꺼번에 지정할 수도 있습니다.
app.get('/multiple-options', (req, res) => {
  res.cookie('multipleOption', 'value', {
    secure: true,
    httpOnly: true,
    maxAge: 5000
  })
  res.redirect('/')
})

app.listen(3000, function() {
  console.log('listening...')
})

```

### 7. Javascript + Cookie
`자바스크립트로도 쿠키를 읽고 쓰는 방법이 존재`하지만, 보안상 문제를 일으킬 수 있으므로 이런 접근 방식은 거의 사용 되지 않는다.
> 자바스크립트에서 쿠키에 접근하지 못하도록 `HttpOnly를 항상 설정한는 것이 best practice`

### 8. 쿠키의 한계점
- US-ASCII밖에 저장하지 못함
  - `보통, PERCENT ENCODING사용`
- `4000바이트` 내외(영문 4000자, PERCENT ENCODING된 한글 444자 가량)밖에 저장하지 못함
- 브라우저에 저장됨
  - `여러브라우저에 걸쳐 공유되어야 하는 정보`
  - `웹브라우저가 아닌 클라이언트(모바일앱)`에 저장되어야 하는정보는 부적절

## 3. SESSION
사전적 의미 : (특정 활동을 위한)시간, (의회 등의)회기; (법정의)개정(기간)  
실질적 의미: `시작조건`과 `종료조건`이 있는 시간, 또는 회기
> `정보교환이 지속되는`시간, 또는 회기

### 1. 세션의 예
- HTTP SESSION
  - 요청 - 응답
- 로그인 세션
  - 로그인 - 로그아웃
- GOOGLE ANALYTICS 세션
  - 페이지 접속 - 30분간 접속이 없으면 종료로 간주(커스터마이징 가능)

### 2. 웹서비스를 위한 세션의 구현
- 1. 세션이 시작되면, `세션이 시작되었다는 사실`을 `쿠키에 저장`
- 2. 세션에 대한 정보를 여러 요청에 걸쳐서 지속시키기 위해, 정보를 `어딘가에 저장`
- 3. 세션이 만료되면, `세션이 만료되었다는 사실을 쿠키에 반영`

> 위 방식은 널리 사용되는 방식일 뿐, 반드시 위와 같이 구현해야 하는 것은 아닙니다.

### 3. 세션 스토어
세션에 대한 정보를 저장하는 `어딘가`
- 쿠키
- 데이터베이스
- 파일
- 기타 정보를 저장할 수 있는 곳 어디든

#### 1. 세션스토어의 선택
`서비스의 요구사항`에 맞춰서 `적절한 저장소를 선택`하면 됨
- 쿠키
  - 정보의 형태가 간단하고 자주 바뀔 일이 없다면
- 데이터 베이스
  - 저장해야 할 정보의 양이 많다면.
- 메모리 기반 저장소
  - 정보가 굉장히 자주 변경된다면.

#### 2. 세션? 세션스토어?
`세션`과 `세션 스토어`는 엄연히 다른말
> `세션에 정보를 저장한다`는 말은 `세션 스토어에 정보를 저장한다`는 말과 같은 뜻이다.

### 4. EXPRESS + SESSION
- COOKIE-SESSION
  - 쿠키에 모든 정보를 저장한느 세션 스토어
  - 첫 방문시 무조건 세션 시작
- EXPRESS-SESSION
  - 쿠키에는 세션 식별자만 저장하고 실제 정보의 저장은 외부저장소를 이용하는 세션스토어
  - 데이터베이스등
  - 외부저장소에 대한 별도 설정 필요

### 5. 예제(COOKIE-SESSION)
[예제](https://glitch.com/edit/#!/noon-whiskey)
- 구현 규칙
  - 1. req.session.username === undefined이면 로그인된 사용자가 없는것으로 간주
  - 2. 사용자가 로그인 폼을 전송하면 accounts배열에 저장된 계정정보중에 일치하는 것이 있는지 확인하고, 있다면 req.session.username에 해당 사용자 이름을 저장합니다. 만약 일치하는 계정이 없으면 400 bad request 응답을 보낸다.
  - 3. req.session.username에 저장된 값이 있다면 해당 사용자로 로그인 되어 있다고 간주
  - 4. 로그아웃을 하기위해 req.session = null과 같이 대입헤서 세션을 초기화 한다.
```javascript
const express = require('express')
const cookieSession = require('cookie-session')

const app = express()

app.set('trust proxy', 1) 
app.set('view engine', 'ejs')

// cookie-session 설정
// name: 쿠키 이름으로 사용할 문자열
// secret: 세션 정보를 서명할 때 사용할 키
app.use(cookieSession({ //쿠키세션 미들웨어
  name: 'session',
  secret: process.env.SECRET
}))

// req.session.count를 처리하는 미들웨어
const countMiddleware = (req, res, next) => {
  if ('count' in req.session) {
    // count 속성이 있으면 1으.
    req.session.count += 1
  } else {
    // count 속성이 없으면 처음 방문한 것이므로 1로 설정한다.
    req.session.count = 1
  }
  next()
}

// 첫 방문 후, 쿠키 관련 헤더가 요청과 응답에 잘 포함되는지 살펴보고,
// 실제로 쿠키가 어떻게 저장되어있는지 살펴보세요.
app.get('/', countMiddleware, (req, res) => {
  res.render('index.ejs', {count: req.session.count})
})

app.post('/reset-count', (req, res) => {
  delete req.session.count
  res.redirect('/')
})

app.listen(3000, function() {
  console.log('listening...')
})
```
```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <div>
      <%= count %>번 째 방문하셨습니다.
    </div>
    <form action="/reset-count" method="post">
      <button type="submit">
        초기화
      </button>
    </form>
  </body>
</html>
```

### 6. 인증/인가 실습
[예제](https://glitch.com/edit/#!/poised-jumbo)
```javascript
const express = require('express')
const cookieSession = require('cookie-session')
const bodyParser = require('body-parser')

const app = express()
const urlencodedMiddleware = bodyParser.urlencoded({extended: false})

app.set('trust proxy', 1) 
app.set('view engine', 'ejs')

const accounts = [
  {
    username: 'suhyeon',
    password: 'jo',
    name: '조수현'
  },
  {
    username: 'flora123',
    password: 'flora123',
    name: '조수현짱 ',
    admin: true
  }
]

app.use(cookieSession({
  name: 'session',
  secret: process.env.SECRET
}))

app.use((req, res, next) => {
  if (req.session.username) {
    req.user = res.locals.user = accounts.find(acc => acc.username === req.session.username)
  } else {
    req.user = res.locals.user = null
  }
  next()
})

app.get('/', (req, res) => {
  res.render('index.ejs')
})

app.post('/login', urlencodedMiddleware, (req, res) => {
  
  // 인증 과정을 작성해주세요.
  const match = accounts.find(acc => acc.username === req.body.username && acc.password === req.body.password)
  if(match){
    req.session.username = match.username
    req.session.admin = match.admin
    res.redirect('/')
  }else{
    res.status(400)
    res.send('아이디와 비밀번호를 확인하세요')
  }
})

function onlyAdminMiddleware(req, res, next) {
  // `/secret`에 접속했을 때 이 미들웨어가 작동합니다.
  // 관리자가 아니면 403 Forbidden 응답을 보내도록 작성해주세요.
  //const admin_match = accounts.find(acc => acc.username === req.session.username)
  if(req.session.admin){ //로그인했을 때 이미 res.session.admin을 저장했기 때문에 가능하다
    //res.send('권한이 있습니다.')
    next()
  }else{
    res.status(403)
    res.send('권한이 없습니다.')
  }
}

app.get('/secret', onlyAdminMiddleware, (req, res) => {
  res.send('It is my secret')
})

app.post('/logout', urlencodedMiddleware, (req, res) => {
  req.session = null
  res.redirect('/')
})

app.listen(3000, function() {
  console.log('listening...')
})
```

>signature 를 이용해서 보안성 을 확보해야한다. session.sig 