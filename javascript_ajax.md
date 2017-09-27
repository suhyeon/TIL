# JAVASCRIPT - AJAX
## 4. JSON
Ajax 요청에 대한 서버의 응답은 주로 HTML, XML, JSON이 사용된다. 이 중 가장 일반적인 데이터 형식은 JSON(JavaScript Object Notation)이다.

```javascript
// JSON 형식의 문자열 => 객체
var obj = JSON.parse(strObject);
console.log(typeof obj, obj); // object { name: 'Lee', gender: 'male' }

// 객체 => JSON 형식의 문자열
var strObject = JSON.stringify(o);
console.log(typeof strObject, strObject); // string '{"name":"Lee","gender":"male"}'
```

## 6. JSON LOAD
### 3. LOAD JSONP
요청에 의해 웹페이지가 전달된 서버와 동일한 도메인의 서버로부터 전달된 데이터는 문제없이 처리할 수 있다.
> 다른 도메인은 브라우저가 크로스 도메인 요청은 제한된다. : 동일출처원칙

`우회하는 방법`
- 1. 웹서버의 프록시 파일
  - 서버에 원격 서버로부터 데이터를 수집하는 별도의 기능을 추가하는 것 : 프록시
- 2. JSONP
  - script 태그의 원본 주소에 대한 제약이 존재하지 않는데 이것을 이용해 다른 도메인의 서버에서 데이터를 수집하는 방법
  - 자신의 서버에 함수를 정의하고 다른 도메인의 서버에 얻고자 하는 데이터를 인수로 하는 함수 호출문을 로드하는 것이다.
  `API 제공방식`
  ```javascript
  <!-- 루트 폴더(htdocs)/loadjsonp.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="http://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id='content'></div>

    <script>
    function showTours(data) {
      console.log(data); // data: object

      // JSON → HTML String
      var newContent = '';
      newContent += '<div id="tours">';
      newContent += '<h1>Guided Tours</h1>';
      newContent += '<ul>';
      for (var i = 0; i < data.tours.length; i++) {
        newContent += '<li class="' + data.tours[i].region + ' tour">';
        newContent += '<h2>' + data.tours[i].location + '</h2>';
        newContent += '<span class="details">' + data.tours[i].details + '</span>';
        newContent += '<button class="book">Book Now</button>';
        newContent += '</li>';
      }
      newContent += '</ul></div>';

      document.getElementById('content').innerHTML = newContent;
    }
    </script>
    <script src='http://poiemaweb.com/assets/data/data-jsonp.js'></script>
    <!-- <script>
      showTours({
        "tours": [
          {
            "region": "usa",
            "location": "New York, USA",
            "details": "$1,899 for 7 nights"
          },
          {
            "region": "europe",
            "location": "Paris, France",
            "details": "$2,299 for 7 nights"
          },
          {
            "region": "asia",
            "location": "Tokyo, Japan",
            "details": "$3,799 for 7 nights"
          }
        ]
      });
    </script> -->
  </body>
</html>
// http://poiemaweb.com/assets/data/data-jsonp.js
showTours({
  "tours": [
    {
      "region": "usa",
      "location": "New York, USA",
      "details": "$1,899 for 7 nights"
    },
    {
      "region": "europe",
      "location": "Paris, France",
      "details": "$2,299 for 7 nights"
    },
    {
      "region": "asia",
      "location": "Tokyo, Japan",
      "details": "$3,799 for 7 nights"
    }
  ]
});
  ```
- 3. Cross-Origin resource Sharing
  - HTTP 헤더에 추가적으로 정보를 추가해 브러우저와 서버가 서로 통신해야 한다는 사실을 알게하는 방법