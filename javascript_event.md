# JAVASCRIPT - EVENT
브라우저에서의 이벤트 : 사용자가 버튼을 클릭했을 때, 웹페이지가 로드되었을 때와 같은 것 
> DOM 요소와 관련이 있다.

```javascript
var elem = document.getElementById('myButton');
elem.addEventListener('click', function() {
  console.log('Clicked!');
});
```
LOAD : DOM 생성이 완료된 후 Javascript를 실행할 수 있게 하는 것. 이것이 좋을 거 같다.

## 5. Event listner
### DOM Level 2 Event Listener
```javascript
//존재의 여부를 확인하는 조건문
if (elem.addEventListener) {    // IE 9 ~
  elem.addEventListener('click', func); 
} else if (elem.attachEvent) {  // ~ IE 8
  elem.attachEvent('onclick', func);
}
```
```html
<!DOCTYPE html>
<html>
<body>
  <script>
    addEventListener('click', function() {
      alert('Clicked!');
      //앞에 타겟이 없다면 window스코프이다.
    });
  </script>
</body>
</html>
```
- input 요소를 blur 이벤트에 바인딩하였다. 사용자 이름이 최소 2자 이상이야한다는 규칙을 세우고 이에 부합하는지 확인하는 처리를 한다.
```html
<!DOCTYPE html>
<html>
<body>
  <label for="username">User name </label>
  <input type="text" id="username">
  <em id="message"></em>
  <script>
    var elem = document.getElementById('username');
    var msg  = document.getElementById('message');

    elem.addEventListener('blur', function () {
      if (elem.value.length < 2) { //value를 잡아오면 사용자가 입력한 value를 잡아온다.
        msg.innerHTML = '이름은 2자 이상 입력해 주세요';
      } else {
        msg.innerHTML = '';
      }
    });
  </script>
</body>
</html>
```

## 7. EVENT FLOW (이벤트의 흐름)
버블링 : 이벤트가 발생한 요소에서 위로 순서가진행된다.
캡처링 : 위에서 이벤트가 발생한 요소까지 순서가 진행된다.

## 8. EVENT Object (이벤트 객체)

```javascript
<!DOCTYPE html>
<html>
<body>
  <p>클릭하세요. 클릭한 곳의 좌표가 표시됩니다.</p>
  <em id="message"></em>
  <script>
  function showCoords(e) { // e: event object
    var msg = document.getElementById('message');
    msg.innerHTML =
      'clientX value: ' + e.clientX + '<br>' +
      'clientY value: ' + e.clientY;
  }
  addEventListener('click', showCoords);
  </script>
</body>
</html>
```
>this 는 언제나 current target 과 같다.
- display : none : 공간 조차 사라진다.
- visibility : hidden : 시야에서만 사라진다.