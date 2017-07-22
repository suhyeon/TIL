# CSS - UNITS(단위)
## CSS 선언 구조
```
  h1{color:red; font-size: 12px;}
  // h1 : selector
  // color, font-size : property
  // red, 12px : property-value
```

## 1. 키워드
각 프로퍼티에 따라 사용할 수 있는 키워드가 존재.   
>ex ) display의 값 키워드 : block, inline, inline-block    

## 2. 크기 단위
css 상대적 크기단위 : em, %  
css 절대적 크기단위 : px

- px : 픽셀(화소)단위  
  디바이스 해상도에 따라 상대적인 크기를 갖는다.  

    > px은 요소의 크기나 이미지의 크기 지정에 주로 사용된다.

       div {
          font-size: 14px;
          }

- % : 백분률 단위의 상대단위  
    > 요소에 지정된 사이즈(상속된 사이즈나 디폴트 사이즈)에 상대적인 사이즈를 설정한다.

         div {
      font-size: 120%;                 // 14px * 1.2 = 16.8px 
         }

- em : 배수 단위인 상대 단위  
  요소에 지정된 사이즈에 상대적인 사이즈를 설정한다.

  > 주의 : 모든 자식 요소의 사이즈에 영향을 미친다.

  ```
  <div class='box1'>
    Font size: 1.2em ⇒ 14px * 1.2 = 16.8px
    <div class='box2'>
      Font size: 1.2em ⇒ 16.8px * 1.2 = 20.16px
      <div class='box3'>
        Font size: 1.2em ⇒ 20.16px * 1.2 = 24.192px
      </div>
    </div>
  </div>
  ```

- rem : 최상위 요소(html)의 사이즈를 기준  
```
 html {
      font-size: 14px;
      /* font-size 미지정 시에는 16px */
    }
    div {
      font-size: 1.2rem; /* html font-size: 14px * 1.2 = 16.8px */
    }
```
### 2.1 Viewport 단위
  viewport를 기준으로 한 상대적 사이즈 상대 단위

- 1vw : viewport 너비 1000px의 1%인 10px
- 1vh : viewport 높이 600px의 1%인 6px
- vmin : viewport 높이 600px의 1%인 6px
- vmax : viewport 너비 1000px의 1%인 10px
```
.item {
      width: 50vw;
      height: 100vh;
      text-align: center;
      line-height: 100vh;
    }
```
## 3. 색상 표현 단위
  - 키워드 방식
  - HEX 코드단위
  - 나머지 방식   
       [HTML color codes 참조](http://htmlcolorcodes.com/)

> 키워드 방식이 편리하지만 색상표현에 한계가 있다.
```
  keyword {
    color: red; //키워드 방식
  }
  HEX {
    background-color: #ff0000;
  }
```
<!--2017.07.22 SuhyeonJo --!>