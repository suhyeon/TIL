# 1주차
# 처음만나는 NODE.JS
## 1일차 
- REST API - 실습
- Node.js
- Asynchronous Javascript

### REST API & NODE.JS
REST API 실습

#### POSTMAN
MAKES API DEVELOPMENT FASTER EASIER AND BETTER
- REST API를 시험해 볼 수 있는 도구
- 다양한 편의 기능 제공

#### GITHUB API
[GITHUB API](https://developer.github.com/v3/)
 
HTTP GET
GET /user/respos
Authorization: basic Auth, Digest, Bearer

#### Node.js
nvm ls : 시스템에 무엇이 깔려있는지, 버전이 몇 인지
nvm use : 원하는 버전으로 사용할 것이라는 명령어
node 6.11.x : 이전에 사용했던 프로그램들은 이 버전에 종속
node 8.4.0 : 이전에 사용했던 프로그램들은 사용할 수 없음

window : use한 버전으로만 지정해도 default 지정이 된다.
mac , linux : nvm alias default x.x.x 버전을 한번더 지정해주어야 사용할 수 있다.

node.js module 사용하기
> const os = require('os')
undefined
> os.platform()
'win32' 
> os.freemem()
3968794624 //남아있는 메모리

$ node (파일 경로) : node.js 로 파일 실행시키기

path 모듈 : 운영체제마다 경로를 처리하는 방식이 다 다른데, 그 처리를 같이 할 수 있게 하는 모듈(운영체제와 상관없이 처리할 수 있게 해주는 기능)
>const path = require('path');

#### info
node.js is `javascript runtime` built on chrome's `v8 javascript engine`. node.js uses an `event-driven, non-blocking I/O model` that makes it lightweight and efficient. Node.js pacakge ecosystem, `npm`, is the largest ecosystem of open source libraries in the world.

### JAVASCRIPT RUNCTIME
- JAVASCRIPT : 언어
- JAVASCRIPT RUNTIME : JS를 구동하기 위해 필요한 실행 환경
- 프로그래머는 런타임이 제공하는 도구를 응용해서 프로그램을 개발
- 웹 브라우저나 NODE.JS 도 JAVASCRIPT 런타임의 일종

`종류`
- CHROME이 제공하는 웹브라우저용 런타임
- NODE.JS 가 제공하는 서버용 런타임
- MONGODB가 제공하는 데이터 처리용 런타임
- PHOTOSHOP이 제공하는 전용 런타임

`V8 JAVASCRIPT ENGINE`
- JIT(JUST-IN-TIME) COMPILATION
- CODE OMTIMIZATION
- USED IN 
  - GOOGLE CHROME
  - NODE.JS
  - MONGODB

- HOW V8 ENGINE WORKS

- EVENT-DRIVEN PROGRAMMING
  - 프로그램의 흐름이 외부 요인에 의해 일어나는 사건에 의해 결정되는 프로그래밍 양식
  - 약속된 방식으로 이벤트 핸들러를 작성함으로 외부 이벤트가 일어났을 때 코드를 실행
    - 마우스 입력
    - 키보드 입력
    - 다른프로그램/컴퓨터로부터의 통신
```javascript
//DOM 이벤트 핸들러 등록(웹 브라우저)
domElement.addEventListener('click', function(e){
  e.stopPropagation();
  alert('hello');
});

//서버도 똑같다.
// 단, 프레임 워크를 쓸 때는 직접 이벤트를 다룰 일이 별로 없다.
// HTTP 응답 이벤트 핸들러 등록(NODE.JS)
httpResponse.on('data', data => {
  console.log(data);
});
//앞으로는 프레임 워크를 사용할 것이기 때문에 직접 등록해서 사용할 일은 거의 없다.
```
- blocking I/O 
  - 스레드가 입/출력이 완료될때 까지 기다렸다가 다음 코드를 실행
- Non-blocking I/O 
  - 스레드가 입/출력을 기다리지 않고 코드를 계속 실행
`I/O 성능 향상 & 복잡한 코드`

- Node.js Module
```javascript
// name.js

// `module.exports`에 저장한 값은 다른 모듈에서 불러올 수 있음
// 미리 빈객체가 module.exports에는 들어있다.
module.exports = {
  familyName: '조',
  givenName: '수현',
  fullName: function() {
    return this.familyName + this.givenName
  }
}

// calc.js

// `exports`로도 참조 가능
exports.add = (x, y) => x + y
exports.sub = (x, y) => x - y
```
> node.js 모듈은 각각의 스코프가 따로 있다.(모듈 스코프)
> 다른 모듈에서 쓰려면 무조건 module.exports 안에 들어 있어야 한다.
#### NPM
Node.js 패키지 관리 도구 + 클라우드 패키지 저장소
- 의존 패키지 관리
- 스크립트 실행
- 패키지 설정
- npm에 패키지 배포
- node.js 종합 작업 도구
$ mkdir hello-npm
$ cd hello-npm
$ npm innit -y
$ code .
```json
// package.json
{
  "name": "hello-npm",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
package.json
- 패키지 정보를 담고 있는 파일
- dependencies
  - `npm install --save` 명령으로 설치한 패키지가 기록된다.
- scipts
  - 원래 목적은 패키지 생명주기마다 자동적으로 실행되는 명령을 등록하기 위함이나 개발자 편의를 위해 `자주 사용되는 명령을 등록`하는 용도로 더 많이 사용된다.  

```json
// package.json
...
  "scripts": {
    "start": "node index.js" //명령어를 단축 지정할 수 있다.
  }
...
```
#### CONCURRENCY (동시성)
동시성 모델 : 프로그램이 생애 주기가 겹치는 여러 실행과정을 통해 실행된다 하더라도 프로그램의 결과에는 영향을 미치지 않는 성질
- 생애주기가 겹치는 `여러 실행과정`이 `자원을 공유`할 때 어떻게 `충돌`이 생기지 않도록 할 것인가?

- resources
  - cpu
  - 메모리
  - 네트워크
- thread
  - 코드 실행의 가장작은 단위
  - 프로그램은 하나이상의 스레드로 이루어짐
  - cpu코어 하나는 한번에 하나의 스레드를 실행
- cpu cores & threadsd
```javascript
$ sysctl -n hw.ncpu # OSX
$ nproc # linux
$ mmc devmgmt.msc # Windows
$ top -H # Shows the total number of threads
```

동시성을 위한 도구
- 운영체제 차원의 도구
  - process
  - thread
  - mutex (Mutual Exclusion)
- 언어 차원의 도구
  - python = asyncio
  - Go = goroutine
  - erlang = actor
  - javascript = ..?

`자바스크립트의 동시성`
> single threaded event Loop
- 자바스크립트를 실행시키는 스레드가 하나뿐
- 실행과정(보통 콜백 연쇄)의 생애주기가 겹칠수는 있지만 어떤 경우에도 두 자바스크립트 실행과정이 동시에 실행되는 경우는 없음
- 내부적으로 메세지큐를 활용하고 있지만 모든 처리가 자동으로 이루어짐

- 장점
  - 프로그래머가 동시성에 대해 신경쓸 필요가 없어짐
  - 프로그램 작성이 쉬어짐
- 단점
  - cpu를 많이 쓰는 작업에 부적절
  - 오래걸리는 자바스크립트 코드가 실행되면 전체 프로그램에 영향을 미침
- 전략
  - 오래걸리는 일은 외부에 위임하고 넘어간뒤, 나중에 결과를 받아 처리하기
    - Database
    - nodejs - external libraries
    - web browser - webAssembly
  - 긴 실행 과정을 여러개의 함수를 쪼개서 한번의 함수 실행이 금방 끝나게 만들기 (promise로 잘게 쪼갠다)

#### Asynchrounous Javascript

비동기식 callback
- 함수를 호출할 때, 콜백까지 같이 인자에 넣어서 호출하는 비동기 프로그래밍 양식
- 콜백에서 에러인자를 받는 방식으로 에러처리를 함
- Node.js 내장 모듈 전체가 이 방식을 사용하도록 만들어져 있음
> `주의! 모든 콜백이 비동기인 것은 아님`
```javascript
> [1,2,3].map(x => x*x)
[ 1, 4, 9 ]
```

> readfile 사용하기
```javascript
// readFile.js
const fs = require('fs') // Node.js 내장 모듈
fs.readFile('./calc.js', 'utf8', (err, data) => {
  console.log(data)
})
console.log('done!')

// readFileSync.js
const fs = require('fs') // Node.js 내장 모듈
const data = fs.readFileSync('./calc.js', 'utf8')
console.log(data)
console.log('done!')
```

nodejs = err가 없다면 err파라미터에 null을 전달한다.

PROMISE : 비동기 작업의 결과를 담는 객체
> 정확히 언제가 될지 모르지만 결국 성공 또는 실패의 상태를 갖게 됨
- 가장 유명한 라이브러리 : bluebird
```javascript
// tenSec.js
module.exports = function tenSec(value) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(value)
    }, 10000)
  })
}

// REPL
> const tenSec = require('./tenSec')
> const p = tenSec(1)
> p // 만든지 10초가 지나기 전
Promise {
  [pending],
  ...
> p // 만든지 10초가 지난 후
Promise {
  1,
  ...
```
.then을 이용하면 promise가 성공했을 때 실행할 동작을 명령할 수 있다.
- then 안에서 promise를 리턴하면 앞에서 리턴한 promise를 벗기는 효과가있다.(안의 값만 들어간다.)
- then안에서 비동기식 작업을 이어나갈수 있다.
then 의 장점
- 가독성이 매우 큰 장점이다.
- 동시성에서 코드를 잘게 쪼갤 때도 사용할 수 있다.
- 계산을 많이 사용할 때 중간중간 틈을 줄 때 promise를 쓴다.
```javascript
// chaining.js
const tenSec = require('./promise')
tenSec('hello promise')
  .then(value => {
    console.log(value)
    return 1 // 위 `.then`은 값이 1인 Promise를 반환함
  })
  .then(value => {
    console.log(value)
    return tenSec('new promise') // Promise도 반환할 수 있음
  })
  .then(value => { //promise가 아닌값은 그냥 그대로 value로 들어가고
    console.log(value) //promise 인 값은 그 안의 값만 value로 들어간다.
  })
  .then(() => {
    throw new Error('error in promise')
  })
  .catch(err => { //catch위에 있던 코드에서 에러가 나면 catch가 실행
    console.error(err)   //catch역시 promise반환
  })
  .then(() => { // 에러 처리 이후에도 코드 실행 가능
    console.log('done')
  })

readFile - promise
// readfilePromise.js
const {promisify} = require('util') // Node.js 8.0.0부터 추가됨
const fs = require('fs')
const readFile = promisify(fs.readFile) //파일을 다읽으면 promise를 반환
readFile('./calc.js', 'utf8')
  .then(data => {  
    console.log(data)
  })
  .catch(err => {
    console.error(err)
  })
Promise의 특징
이미 resolve 된 Promise에도 콜백을 실행할 수 있음

> const resolved = Promise.resolve(1) //new를 사용하지 않고 바로 성공하는 상태의 promise 생성
> resolved.then(v => console.log(v))
`.then`에 넘겨진 콜백은 무조건 다음 루프에 실행됨

> (function() { //실제는 비동기식으로 실행된다.
... Promise.resolve(1).then(v => console.log(v))
... console.log('done!')
... })()
/* 출력:
done!
1
*/
promise.all([p1,p2])
// 배열안에 넘기는 값들이 모두 성공해야 성공한다.
promise.race([p1, p2])
//배열안에 넘기는 값들중 제일 빨리 성공하는 것을 나타낸다.
```
promise.all
```javascript
// npm install --save request-promise
const rp = require('request-promise') //request get처럼 똑같이 get메소드를 통해서 http를 날리는데 뒤에 콜백을 받는게 아니라 promise를 반환한다.
const apiUrl = 'https://api.github.com'
const option = {
  json: true,
  auth: {
    'user': 'username',
    'pass': 'password',
  },
  headers: {
    'User-Agent': 'request'
  }
}

const userPromise = rp.get(`${apiUrl}/user`, option)
const reposPromise = rp.get(`${apiUrl}/user/repos`, option)
const issuesPromise = rp.get(`${apiUrl}/issues`, option)

// 배열 내의 모든 Promise 객체가 완료되었을 때
// resolve 되는 Promise를 만든다.
Promise.all([userPromise, reposPromise, issuesPromise])
  .then(([user, repos, issues]) => { //디스트럭처링 배열도 가능
    console.log(`name: ${user.name}`)
    console.log('repos:')
    repos.forEach(repo => {
      console.log(repo.name)
    })
    console.log(`num of assigned issues: ${issues.length}`)
  })
```
Async/Await
```javascript
const tenSec = require('./tenSec')

async function resolveAfterTenSec() {
  await tenSec()
  return 1
}

resolveAfterTenSec().then(value => {
  console.log(value)
})
```
- ES2017에서 도입되어서 비동기식 코드를 동기식 코드처럼 쓸수 있는 문법 제공
- CHROME 55, NODE.JS 8.0.0부터 사용가능
- ASYNC FUNCTION 안에서 반환된 값은 최종적으로 PROMISE 객체로 변환되어 반환된다.
- ASYNC FUNCTION 안에서 쓸수 있는 AWAIT 키워드는 현재 함수를 중단시키고 PROMISE 객체가 충족될 때 까지 기다리지만, 스레드를 BLOCK하지 않는다.
- 에러 처리는 동기식 코드처럼 TRY,CATCH블럭을 통해서한다.