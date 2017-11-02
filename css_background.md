# CSS-BACKGROUND

  ## 1. background-image 프로퍼티

  요소에 배경이미지를 지정한다.

  ```
  body {
      background-image: url("http://poiemaweb.com/img/bg/dot.png");
    }
  ```

  ## 2. background-repeat 프로퍼티
  배경 이미지의 반복을 지정한다.   수직, 수평, 수직과수평 반복을 지정할 수 있다.

```
body {
      background-image: url("http://poiemaweb.com/img/bg/dot.png");
      background-repeat: repeat-x;
    }
```
> 반복 출력을 멈추고 싶은 경우,  
> background-repeat 프로퍼티값에 no-repeat를 설정한다.

` 복수개의 이미지를 설정할 경우,  `  
` 먼저 설정된 이미지가 전면에 출력된다.`

## 3. background-size 프로퍼티
배경이미지의 사이즈를 지정한다.

> 프로퍼티값 : px, %, cover, contain 등

`하나의 값만을 지정한 경우,  `  
`지정한 값은 width를 의미.
height는 auto로 지정`
 - px 값 지정 : width, height 순으로 설정된 값 그대로 지정
 - % 값 지정 : 퍼센트 값에 비례해 설정
 - cover 지정 : 크기 비율을 유지한 상태에서 부모 요소의 w,h 중 큰값에 배경이미지를 맞춘다. 
 - contain 지정 : 크기 비율을 유지한 상태에서 부모 요소의 영역에 전체가 들어갈 수 있도록 스케일을 조정한다.

 ## 4. background-attachment 프로퍼티

 화면을 스크롤해도 배경이미지는 스크롤되지 않고 고정되게 한다.
 > background-attachment: fixed;

 ## 5. background-position 프로퍼티
 이미지의 출력좌표를 지정할 수 있다.   
 (xpos, ypos)

 > 기본값은 background-position: 0% 0%; 배경이미지는 우측 상단에 위치하게 된다.

 #### 마진 상쇄
 개념 : 이 무엇인지 익혀보아라.

[마진 상쇄문제 해결을 위한 코드]( https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
```
  #page-wrap {
      width: 400px;
      /* 마진 상쇄 발생 */
      margin: 50px auto;
      padding: 30px;
      background: white;
      box-shadow: 0 0 20px black;
      /* size/line-height | family */
      font: 15px/2 Georgia, Serif;
    }
```

## 6. background-color 프로퍼티
  요소의 배경색상을 지정한다.

## 7. background Shorthand
  한번에 정의하기 위한 Shorthand Syntax이다.
```
// order 순서
background: color || image || repeat || attachment || position
```
<!--2017.07.22 SuhyeonJo --!>