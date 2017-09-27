# JQUERY - BASICS
## 1. INTRODUCTION
attribute & property
- attribute : html의 속성
- property : 객체의 속성

> DOM 에 className : html의 class : 1:1매핑이 안된다.
- td 요소의 colspan프로퍼티의 경우 어트리뷰트가 존재하지 않는다.
- input 요소의 value 어트리뷰트는 value 프로퍼티와 1:1매핑하지만 서로 다르게 동작한다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="http://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id='content'></div>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <script>
    $.ajax({
      url: "data/data.html",
      cache: false
    })
      .done(function(data, textStatus, jqXHR) {
        $("#content").html(data);
      })
      .fail(function(jqXHR, textStatus, errorThrown){
        console.log("fail: ", jqXHR);
      })
      .always(function(data, textStatus, jqXHR){
        console.log("always: ", data);
      });
    </script>
  </body>
</html>
```