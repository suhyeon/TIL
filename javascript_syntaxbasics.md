# JAVASCRIP - SYNTAX BASICS
## 1. hello world

.---() : 메소드
.--- : 프로퍼티

`DOM 트리에서 만들어진 데이터를 스크립트엔진이 가져오는 구조`
-궁금증 : DOM트리에서 만들어진 데이터를 스크립트 엔진이 가져 오는 과정에서 트리가 손상되거나 그럴 가능성이 있는가?

보틀넥현상이 일어나는 것을 방지하기 위해 html5부터 스크립트 태그에 async & defer 어트리뷰트가 추가 되었다.
```
<script async src="extern.js"></script>
<script defer src="extern.js"></script>
```

async :
웹페이지 파싱과 외부 스크립트 파일의 다운로드가 동시에 진행된다. 스크립트는 다운로드 완료 직후 실행된다. IE9 이하 버전은 지원하지 않는다.

defer : <IE9 이상에 사용하면 적합></IE9>
웹페이지 파싱과 외부 스크립트 파일의 다운로드가 동시에 진행된다. 스크립트는 웹페이지 파싱 완료 직후 실행된다. IE9 이하 버전에서 정상적으로 동작하지 않을 수 있다.

## JAVASCRIPT SYNTAX BASICS
### 1. 구문

스크립트는 컴퓨터에 의해 단계별로 수행될 명령들의 집합
(엄밀히, 웹 브라우저에 의해)

```
var x = 5;   //var : 변수
var y = 6;
var z = x + y;   
document.getElementById('demo').innerHTML = z;
```

### 2. 변수
값을 저장,참조하기 위해 사용된다.
한번 쓰고 버리는 값이 아닌 유지할 필요가 있는 값의 경우, 변수를 사용한다.
변수 == identifier

var x; //변수의 선언과 초기화  
x = 6; //정수값의 할당
변수를 선언하면 메모리를 확보하려 한다. 처음에 선언하자마자 메모리에 자리가 들어가는 자리과정 : 초기화

> 자바스크립트는 자바와 달리 값의 데이터타입을 명시하지 않는다.  

```
// literal : Number
10.50
1001

// literal : String
'Hello'
"World"

// literal : Object
{ name: 'Lee', gender: 'male' }

// literal : Array
[ 'Black', 'Gray', 'White' ];
```

### 3. 연산자
하나 혹은 그 이상의 값을 하나의 값으로 만들 때 사용한다.

```
// 비교 연산자
var foo = 3 > 5; // false
// 논리 연산자
var bar = (5 > 3) && (2 < 4);  // true
```
