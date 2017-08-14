# JAVASCRIPT - DOM
## 1. DOM(Document Object Model)

브라우저 : 웹문서(HTML, XML, SVG)를 로드하고 파싱해 DOM(문서 객체 모델)을 생성  

- HTML 문서에 대한 모델 구성
  - 브라우저는 HTML문서를 로드한 후 해당 문서에 대한 모델을 메모리에 생성
    - 이 때 모델은 객체의 트리로 구성된다. : DOM TREE
- HTML 문서내의 각 요소에 접근/수정
  - DOM은 모델 내의 각 객체에 접근하고 수정할 수 있는 프로퍼티와 메소드를 제공
    - DOM이 수정되면 브라우저를 통해 사용자가 보게 될 내용 또한 변경된다.

## 2. DOM TREE
브러우저가 HTML 문서를 로드한 후 생성하는 모델을 의미

> 객체의 트리로 구조화 되어 있기 때문에 DOM TREE라 부른다.
```javascript
<!DOCTYPE html>
<html>
  <head>
    <style>
      .red  { color: #ff0000; }
      .blue { color: #0000ff; }
    </style>
  </head>
  <body>
    <div>
      <h1>Cities</h1>
      <ul>
        <li id="one" class="red">Seoul</li>
        <li id="two" class="red">London</li>
        <li id="three" class="red">Newyork</li>
        <li id="four">Tokyo</li>
      </ul>
    </div>
  </body>
</html>
```

- 문서노드
  - dom에서 모든 요소, 어트리뷰트, 텍스트 노드에 접근하려면 무서노드를 통해야 한다. 
    - 즉, dom tree에 접근하기 위한 시작점(entry point)이다.
- 요소 노드 
  - html 요소를 표현한다.
    - html 요소는 중첩에 의해 부자관계를 가지며 이 부자관계를 통해 정보를 구조화한다.
      - 어트리뷰트, 텍스트 노드에 접근하려면 먼저 요소 노드를 찾아 접근해야 한다.

> 모든 요소노드는 요소별 특성을 표현하기 위해 html element 객체를 상속한 객체로 구성된다.
- 어트리뷰트 노드
  - html 요소의 어트리뷰트를 표현한다.
    - 어트리뷰트 노드는 해당 어트리뷰트가 지정된 요소의 자식이 아니라 해당 요소의 일부로 표현된다.
      - 해당 요소노드를 찾아 접근하면 어트리뷰트를 참조, 수정할 수 있다.
- 텍스트 노드
  - html 요소의 텍스트를 표현한다.
    - 텍스트 노드는 요소 노드의 자식이며 자신의 자식 노드를 가질 수 없다.
> 텍스트 노드는 DOM TREE의 최종단이다.


- `DOM을 통한 웹페이즈를 조작하기 위해서는 다음과 같은 수순이 필요`
  - 조작하고자 하는 요소를 선택 또는 탐색
  - 선택된 요소의 컨텐츠 또는 어트리뷰트를 조작

## 3. DOM QUERY / TRAVERSING(요소에의 접근)
### 1. 하나의 요소노드 선택(DOM QUERY)
`document.getElementById(id)`
- id 어트리뷰트 값으로 요소노드를 한개 선택한다.
  - 복수개가 선택된 경우, 첫째 요소만 반환
- return : HTMLElemet를 상속받은 객체
- 모든 브라우저에서 동작

```javascript
// id로 하나의 요소를 선택한다.
var elem = document.getElementById('one');
// 클래스 어트리뷰트의 값을 변경한다.
elem.className = 'blue';

// 그림: DOM tree의 세부 구성 참고
console.log(elem.__proto__);           // HTMLLIElement
console.log(elem.__proto__.__proto__); // HTMLElement
console.log(elem.__proto__.__proto__.__proto__);           // Element
console.log(elem.__proto__.__proto__.__proto__.__proto__); // Node
```
`document.querySelector(cssSelector)`
- CSS셀렉터를 사용해 요소노드를 한개 선택한다.
  - 복수개가 선택된 경우, 첫째 요소만 반환한다.
- Return : HTMLElement를 상속받은 객체
- IE8이상의 브라우저에서 동작
```javascript
// CSS 셀렉터를 이용해 요소를 선택한다
var elem = document.querySelector('li.red');
// 클래스 어트리뷰트의 값을 변경한다.
elem.className = 'blue';
```
### 2. 여러개의 요소노드 선택(DOM Query)
`document.getElementByClassName(class)
- class 어트리뷰트 값으로 요소노드를 모두 선택한다.
  - 공백으로 구분해 여러개의 class를 지정할 수 있다.
- Return : HTMLCollection(live)
- IE9이상의 브라우저에서 동작

```javascript
// HTMLCollection을 반환한다.
var elems = document.getElementsByClassName('red'), i;

for (i = 0; i < elems.length; i++) {
  // 클래스 어트리뷰트의 값을 변경한다.
  elems[i].className = 'blue';
}
// 예상대로 동작하지 않는다.(두번째 요소만 클래스 변경이 되지 않는다.)
// elems.length : 3 (3번의 loop가 실행)
```
getElementsByClassName 메소드 반환값 : HTML Collection
- 반환값이 복수인 경우, htmlelement의 리스트를 담아 반환하기 위한 객체로 배열과 비슷한 사용법을 가지고 있지만 유사배열이다.  
- 실시간으로 node의 상태 변경을 반영한다.(live HTMLCollection)

`위 예제가 예상대로 동작하지 않은이유`
- i가 0일 때, elems의 첫 요소(li#one.red)의 class 어트리뷰트 값이 className프로퍼티에 의해 red에서 blue로 변경
  - 더이상 class명이 red가 아니므로 elems에서 첫째 요소는 제거(실시간으로 node의 상태 변경을 반영)
- i가 1일 때, elems에서 첫째 요소는 제거되었으므로 elems[1]은 3번째 요소(li#three.red)가 된다.
  - li#three.red의 class 어트리뷰트 값이 blue로 변경
  - 마찬가지로 HTMLCollection에서 제외
- i가 2일때, HTMLCollection 의 1,3번째 요소가 실시간으로 제거되었으므로 2번째 요소(li#two.red)만 남았다. elems[2]는 undefined이다.

> 이처럼 HTMLCollection은 실시간으로 Node의 상태 변경을 반영하기 때문에 loop가 필요한 경우 주의가 필요
`회피 방법`
- 반복문을 역방향으로 돌린다.
```javascript
var elems = document.getElementsByClassName('red'), i;
for (i = elems.length - 1; i >= 0; i--) {
  elems[i].className = 'blue';
}
```
- while 반복문을 사용한다. 이때 elems에 요소가 남아 있지 않을 때까지 무한반복하기 위해 index는 0으로 고정시킨다.
```javascript
var elems = document.getElementsByClassName('red');
var i = 0;
while (elems.length > i) { // elems에 요소가 남아 있지 않을 때까지 무한반복
  elems[i].className = 'blue';
  // i++;
}
```
- HTMLCollection을 배열로 변경한다.
```javascript
var elems = document.getElementsByClassName('red'), i;

// 유사배열을 배열로 변환
var arr = [].slice.call(elems);

console.log(arr); 
// [li#one.red, li#two.red, li#three.red]
// 각 요소는 HTMLLIElement

for (i = 0; arr.length > 0; i++) {
  arr[i].className = 'blue';
}
```
- querySelectorAll 메소드를 사용해 non-live NodeList를 반환
```javascript
// Nodelist(non-live)를 반환한다. IE8+
var elems = document.querySelectorAll('.red'), i;
for (i = 0; i < elems.length; i++) {
  elems[i].className = 'blue';
}
```
- document.getElementsByTagName(tagName)
  - 태그명으로 요소노드를 모두 선택
  - return : HTMLCollection(live)
  - 모든 브라우저에서 동작
```javascript
// HTMLCollection을 반환한다.
var elems = document.getElementsByTagName('li'), i;
for (i = 0; i < elems.length; i++) {
  elems[i].className = 'blue';
}
```
- document.querySelectorAll(selector)
  - 지정된 css선택자를 사용해 요소노드를 모두 선택
  - return : NodeList(non-live)
  - IE8이상의 브라우저에서 동작
```javascript
// Nodelist를 반환한다.
var elems = document.querySelectorAll('li.red'), i;
for (i = 0; i < elems.length; i++) {
  elems[i].className = 'blue';
}
```

### 3. DOM Traversing(탐색)
- parentNode
  - 부모 노드를 탐색
  - return : HTMLElement를 상속받은 객체
  - 모든 브라우저에서 동작
```javascript
var elem = document.getElementById('two');
var parentNode = elem.parentNode;
parentNode.className = 'blue';
```
- firstChild, lastChild
  - 자식노드를 탐색
  - return : HTMLElement를 상속받은 객체
  - IE9이상의 브라우저에서 동작
```javascript
var elem = document.getElementsByTagName('ul')[0];
var firstChild = elem.firstChild;
var lastChild = elem.lastChild;

firstChild.className = 'blue';
lastChild.className = 'blue';
```
- hasChildNodes()
  - 자식 노드가 있는지 확인하고 boolean값을 반환
  - return : boolean값
  - 모든 브라우저에서 동작
- childNodes
  - 자식 노드의 컬렉션을 반환
  - return : NodesList(non-live)
  - 모든 브라우저에서 동작
```javascript
var elem = document.querySelector('ul');
console.log(elem); // ul

if (elem.hasChildNodes()) {
  console.log(elem.childNodes);
  // [text, li#one.red, text, li#two.red, text, li#three.red, text, li#four, text]
  elem.childNodes[1].className = 'blue';
}
```
- previousSibling, nextSibling
  - 형제 노드를 탐색
  - return : HTMLElement 를 상속받은 객체
  - IE9이상의 브라우저에서 동작
```javascript
var elem = document.getElementById('two');
var previousSibling = elem.previousSibling;
var nextSibling = elem.nextSibling;

previousSibling.className = 'blue';
nextSibling.className = 'blue';
//예상대로 동작하지 않는다.
```
- 이유 : IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈문자를 텍스트 노드로 취급하기 때문
- 회피방법
  - jQuery:.prev()와 jQuery:.netx()를 사용
  - HTML에 공백을 제거
```javascript
<ul><li
  id='one' class='red'>Seoul</li><li
  id='two' class='red'>London</li><li
  id='three' class='red'>Newyork</li><li
  id='four'>Tokyo</li></ul>
```

### 4. DOM Manipulation(조작)
#### 1. 텍스트 노드에의 접근/수정
요소의 텍스트는 텍스트 노드에 저장되어 있다.  

`텍스트 노드에 접근하려면 아래와 같은 순서가 필요`
- 해당 텍스트 노드의 부모 노드를 선택
  - 텍스트 노드는 요소 노드의 자식이다.
- firstChild 프로퍼티를 사용해 텍스트 노드를 탐색
- 텍스트 노드의 유일한 프로퍼티(nodeValue)를 이용해 텍스트를 취득
- nodeValue를 이용해 텍스트를 수정

- nodeValue
  - 노드의 값을 반환
  - return : 텍스트노드의 경우 : 문자열, 요소 노드의 경우 : null반환
  - IE6이상의 브라우저에서 동작
```javascript
// 해당 텍스트 노드의 부모 요소 노드를 선택한다.
var one = document.getElementById('one');
console.dir(one); // HTMLLIElement: li#one.red

// firstChild 프로퍼티를 사용하여 텍스트 노드를 탐색한다.
var textNode = one.firstChild;

// nodeValue 프로퍼티를 사용하여 노드의 값을 취득한다.
console.log(textNode.nodeValue); // Seoul

// nodeValue 프로퍼티를 이용하여 텍스트를 수정한다.
textNode.nodeValue = 'Pusan';
```
> nodeName, nodeType을 통해 노드의 정보를 취득할 수 있다.

#### 2. 어트리뷰트 노드에의 접근/수정
어트리뷰트 노드를 조작할 때 사용할 수 있다.

- className
  - class 어트리뷰트의 값을 취득 또는 변경
    - className프로퍼티에 값을 할당하는 경우, class 어트리뷰트가 존재하지 않으면 class어트리뷰트를 생성하고 지정된 값을 설정한다.
    - class어트리뷰트의 값이 여러개일 경우, 공백으로 구분된 문자열이 반환되므로 string메소드split(' ')를 사용해 배열로 변경해 사용
  - 모든 브라우저에서 동작
```javascript
var elems = document.getElementsByTagName('li');

for (var i = elems.length - 1; i >= 0; i--) {
  // class 어트리뷰트의 값을 취득하여 확인
  if (elems[i].className === 'red') {
    // class 어트리뷰트의 값을 변경한다.
    elems[i].className = 'blue';
  } else {
    // class 어트리뷰트의 값을 변경한다.
    elems[i].className = 'red';
  }
}
```
- id
  - id 어트리뷰트의 값을 취득 또는 변경
    - id 프로퍼티에 값을 할당하는 경우, id 어트리뷰트가 존재하지 않으면 id어트리뷰트를 생성하고 지정된 값을 설정
  - 모든 브라우저에서 동작
```javascript
// h1 태그 요소 중 첫번째 요소를 취득
var heading = document.getElementsByTagName('h1')[0];
console.dir(heading); // HTMLHeadingElement: h1
console.log(heading.firstChild.nodeValue); // Cities

// id 어트리뷰트의 값을 변경
heading.id = 'heading';
console.log(heading.id); // heading
```
- hasAttribute(attribute)
  - 지정한 어트리뷰트를 가지고 있는지 검사
  - return : boolean
  - IE8이상의 브라우저에서 동작
- getAttribute(attribute)
  - 어트리뷰트의 값을 취득
  - return : 문자열
  - 모든 브라우저에서 동작
- setAttribute(attribute, value)
  - 어트리뷰트와 어트리뷰트 값을 설정
  - return : undefined
  - 모든 브라우저에서 동작
- removeAttribute(attribute)
  - 지정한 어트리뷰트를 제거
  - return : undefined
  - 모든 브라우저에서 동작
```javascript
var four = document.getElementById('four');

// four에 class 어트리뷰트가 존재하지 않으면
if (!four.hasAttribute('class')) {
  // four에 name 어트리뷰트를 추가하고 값으로 'user'를 설정
  four.setAttribute('class', 'blue');
} else { // four에 class 어트리뷰트가 존재하면
  four.className = 'blue';
}

// four에 lang 어트리뷰트의 값을 취득
console.log(four.getAttribute('class')); // blue

// four에서 name 어트리뷰트를 제거
four.removeAttribute('class');

// inputUser에서 name 어트리뷰트의 존재를 확인
console.log(four.hasAttribute('class')); // false
```

#### 3. HTML 컨텐츠 조작(MANIPULATION)
HTLM 컨텐츠를 조작하기 위해 아래의 프로퍼티 또는 메소드를 사용할 수 있다.
> 마크업이 포함된 컨텐츠를 추가하는 행위 : 크로스 스크립트 공격(XSS: CROSS-SITE SCRIPTING ATTACKS)에 취약하므로 주의가 필요

 - textContent
  - 요소의 텍스트 컨텐츠를 취득 또는 변경
    - 이때 마크업은 무시
    - textContent를 통해 요소에 새로운 텍스트를 할당하면 텍스트를 변경할 수 있다.
    - 순수한 텍스트만 지정해야 하며 마크업을 포함시키면 문자열로 인식되 그대로 출력된다.
  - IE9이상의 브라우저에서 동작한다.

```javascript
var ul = document.getElementsByTagName('ul')[0];

// 요소의 텍스트 취득
console.log(ul.textContent);
// IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급한다
/*
        Seoul
        London
        Newyork
        Tokyo
*/

var one = document.getElementById('one');

// 요소의 텍스트 취득
console.log(one.textContent); // Seoul

// 요소의 텍스트 변경
one.textContent += ', Korea';

console.log(one.textContent); // Seoul, Korea

// 요소의 마크업이 포함된 콘텐츠 변경.
one.textContent = '<h1>Heading</h1>';

// 마크업이 문자열로 표시된다.
console.log(one.textContent); // <h1>Heading</h1>
```
- innerText
  - innerText 프로퍼티를 사용해도 요소의 텍스트 컨텐츠에만 접근할 수 있다.
    - 비표준
    - css에 순종적
    - css를 고려해야하므로 textContent프로퍼티보다 느리다.
- innerHTML
  - innerHtml 프로퍼티를 사용하면 해당 요소의 모든 자식 요소를 포함하는 모든 컨텐츠를 하나의 문자열로 취득할 수있다. 
    - 이 문자열은 마크업을 포함
```javascript
var ul = document.getElementsByTagName('ul')[0];

// innerHTML 프로퍼티는 모든 자식 요소를 포함하는 모든 콘텐츠를 하나의 문자열로 취득할 수 있다. 이 문자열은 마크업을 포함한다.
console.log(ul.innerHTML);
// IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급한다
/*
        <li id="one" class="red">Seoul</li>
        <li id="two" class="red">London</li>
        <li id="three" class="red">Newyork</li>
        <li id="four">Tokyo</li>
*/
```
> innerHTML 프로퍼티를 사용하면 마크업이 포함된 새로운 컨텐츠를 지정해 새로운 요소를 DOM에 추가할 수 있지만 마크업이 포함된 컨텐츠를 추가하는 것은 `크로스 스크립팅 공격`에 취약하다.

```javascript
// 크로스 스크립팅 공격 사례

// 스크립트 태그를 추가하여 자바스크립트가 실행되도록 한다.
// HTML5에서 innserHTML로 삽입된 <script> 코드는 실행되지 않는다.
// 크롬, 파이어폭스 등의 브라우저나 최신 브라우저 환경에서는 작동하지 않을 수도 있다.
elem.innerHTML = '<script>alert("XSS!")</script>';

// 에러 이벤트를 발생시켜 스크립트가 실행되도록 한다.
one.innerHTML = '<img src="#" onerror="alert('XSS')">';
```

#### 4. DOM 조작방식
innerHTML 프로퍼티를 사용하지 않고 새로운 컨텐츠를 추가할 수 있는 방법 : DOM을 직접 조작하는 것
- 한개의 요소를 추가하는 경우 사용한다.
  - 1. 요소 노드 생성
    - createElement() 메소드를 사용해 새로운 요소노드를 생성.
    - createElement() 메소드의 인자로 태그 이름을 전달
  - 2. 텍스트 노드 생성
    - createTextNode() 메소드를 사용해 새로운 텍스트 노드를 생성
    - 경우에 따라 생략될 수 있지만 생략하는 경우, 컨텐츠가 비어있는 요소가 된다.
  - 3. 생성된 요소를 DOM에 추가
    - appendChild()메소드를 사용해 생성된 노드를 DOM tree에 추가한다.
    - removeChild()메소드를 사용해 DOMtree에서 노드를 삭제할 수있다.

- createElemen(tagName)
  - 태그이름을 인자로 전달해 요소를 생성
  - return : HTMLelement를 상속받은 객체
  - 모든 브라우저에서 동작
- createTextNode(text)
  - 텍스트를 인자로 전달해 텍스트 노드를 생성
  - return : Text 객체
  - 모든 브라우저에서 동작
- appendChild(Node)
  - 인자로 전달한 노드를 자식 요소로 DOM 트리에 추가
  - return : 추가한 노드
  - 모든 브라우저에서 동작
- removeChild(Node)
  - 인자로 전달한 노드를 DOM트리에 제거한다.
  - return : 추가한 노드
  - 모든 브라우저에서 동작한다.
```javascript
// 태그이름을 인자로 전달하여 요소를 생성
var newElem = document.createElement('li');
// var newElem = document.createElement('<li>test</li>');
// Uncaught DOMException: Failed to execute 'createElement' on 'Document': The tag name provided ('<li>test</li>') is not a valid name.

// 텍스트 노드를 생성
var newText = document.createTextNode('Beijing');

// 텍스트 노드를 newElem 자식으로 DOM 트리에 추가
newElem.appendChild(newText);

var container = document.getElementsByTagName('ul')[0];

// newElem을 container의 자식으로 DOM 트리에 추가
container.appendChild(newElem);

var removeElem = document.getElementById('one');

// container의 자식인 removeElem 요소를 DOM 트리에 제거한다.
container.removeChild(removeElem);
```
#### 5. insertAdjacentHTML()
- insertAdjacentHTML(position, string)
  - 인자로 전달한 텍스트를 HTML로 파싱하고 그 결과로 생성된 노드를 DOM 트리의 지정된 위치에 삽입
    - 첫번째 인자 : 삽입 위치, 두번째 인자 : 삽입할 요소를 표현한 문자열
    - 첫번째 인사 값
      - beforebegin
      - afterbegin
      - beforeend
      - afterend
  - 모든 브라우저에서 동작
```javascript
var one = document.getElementById('one');

// 마크업이 포함된 요소 추가
one.insertAdjacentHTML('beforeend', '<em class="blue">, Korea</em>');
```
#### 6. innerHTML vs. DOM조작 방식 VS. insertAdjacentHTML()
innerHTML
- 장점
  - DOM조작방식에 비해 빠르고 간편하다.
  - 간편하게 문자열로 정의 여러 요소를 DOM에 추가할 수 있다.
  - 해당 요소의 내용을 덮어쓴다.
    - HTML을 로드하고 다시 파싱한다.(비효율적)
  - 컨텐츠를 취득할 수 있다.
- 단점
  - XSS공격에 취약점이 있기 때문에 사용자로부터 입력받은 컨텐츠를 추가할 때 사용해서는 안된다.

DOM 조작방식
- 장점
  - 특정 노드 한개(노드, 텍스트, 데이터 등)을 DOM에 추가할 때 적합
- 단점
  - innerHTML보다 느리고 더 많은 코드가 필요

insertAdjacentHTML()
- 장점
  - 간편하게 문자열로 정의된 여러 요소를 DOM에 추가할 수 있다.
  - 삽입되는 위치를 선정할 수있다.
- 단점
  - XSS 공격에 취약점이 있기 때문에 사용자로부터 입력받은 컨텐츠를 추가할 때 사용하면 안된다.

> innerHTML과 insertAdjacentHTML()은 XSS에 취약
`따라서 UNTRUSTED DATA경우, 주의하라`
> 텍스트를 추가 또는 변경시에는 TEXTCONTENT, 새로운 요소의 추가 또는 삭제시에 DOM조작방식을 사용하도록 한다.

### 5. STYLE
STYLE 프로퍼티를 사용하면 INLINE스타일 선언을 생성
> 특정요소에 INLINE 스타일을 지정하는 경우 사용한다.
```javascript
var four = document.getElementById('four');

// inline 스타일 선언을 생성
four.style.color = 'blue';

// font-size와 같이 '-'으로 구분되는 프로퍼티는 카멜케이스로 변환하여 사용한다.
four.style.fontSize = '2em';
```