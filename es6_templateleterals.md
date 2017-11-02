# ECMA6 - TEMPLATE LITERALS
템플릿 리터럴이라고 불리는 새로운 문자열 표기법을 도입하였다.
> 템플릿 리터럴은 일반 문자열과 비슷해 보이지만, '또는 " 같은 통상적인 따옴표 문자 대신 백틱문자 `를 사용한다.
```javascript
const template = `템플릿 리터럴은 '작은따옴표(single quotes)'과 "큰따옴표(double quotes)"를 혼용할 수 있다.`;

//리터럴 : 우변에만 값이 들어가고, 값이 전부다 그 자체로만 존재한다. 상수와 다른 개념. 상수는 그것을 가리키는 포인트지만, 리터럴은
//프리미티브 타입 힙에 올라간다. : 레퍼런스 타입 별칭이 존재, 스택에 올라가고 힙을 가리킨다.
//순수함수 : 입출력이 같아야한다, 등등의 룰들을 이용 
//now scale url 1: 서버를 꺼지지 않게 
//now alias url alias이름 : 이름 바꿔주기
//zeig - pkg
//zeit = next.js 
console.log(template);

//일반적인 문자열과 달리 여러줄에 걸쳐 문자열을 작성할 수 있으며 템플릿 리터럴 내의 모든 white스페이스는 있는 그대로 적용된다.
const template = `<ul class="nav-items">
  <li><a href="#home">Home</a></li>
  <li><a href="#news">News</a></li>
  <li><a href="#contact">Contact</a></li>
  <li><a href="#about">About</a></li>
</ul>`;

console.log(template);

//템플릿 리터럴은 +연산자를 사용하지 않아도 간단한 방법으로 새로운 문자열을 삽입할 수 있는 기능을 제공한다.
const first = 'Ung-mo';
const last = 'Lee';

// 기존의 문자열 연결
console.log('My name is ' + first + ' ' + last + '.');

// ES6 String Interpolation
console.log(`My name is ${first} ${last}.`); // My name is Ung-mo Lee.
```
> ${expression}을 템플릿 대입문이라 한다. 템플릿 대입문에는 문자열 뿐만 아니라 javascript 표현식을 사용할 수 있다.
```javascript
// 템플릿 대입문에는 문자열뿐만 아니라 표현식도 사용할 수 있다.
console.log(`1 + 1 = ${1 + 1}`); // 1 + 1 = 2

const name = 'ungmo';

console.log(`Hello ${name.toUpperCase()}`); // Hello UNGMO
```