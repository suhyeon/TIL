# CSS - BOX MODEL 
  모든 html 요소는 box 형태의 영역을 가지고 있다.
> inline요소,  box요소를 가지고 있다.
  - Margin(마진)
  - Border(테두리)
  - Padding(패딩)
  - Contents(컨텐츠)
      - 컨텐츠 안에 다른 요소가 들어간 경우를 중첩되었다고 한다.

> background-color는 패딩까지만 영향이 있다.  

## 1. width / height 프로퍼티
  컨텐츠 영역을 대상으로 너비와 높이가 지정된다.
  > width : 부모의 100%  
  > height : 컨텐츠가 들어갈 영역

## 2. margin/ padding 프로퍼티
  content의 4개 방향(top, right, left, bottom)에 대하여 지정이 가능하다.  

  - 4개의 값을 지정할 때  (t,r,b,l)  
margin: 25px 50px 75px 100px;
  - 3개의 값을 지정할 때 (t,(r,l),b)  
margin: 25px 50px 75px;
  - 2개의 값을 지정할 때 ((t,b),(r,l))  
margin: 25px 50px;
  - 1개의 값을 지정할 때 (t,r,b,l)  
margin: 25px;

> margin: auto 키워드를 설정하면 해당요소를 브라우저 중앙에 위치시킬 수 있다.

> 요소너비 > 브라우저 너비:
가로 스크롤바가 만들어진다.  
해결방법 : max-width를 사용한다.

## 3. border 프로퍼티
>프로퍼티 값의 갯수에 따라 4개 방향에 대해 지정이 가능하다.
---
### 3.1 border-style
테두리 선의 스타일을 지정

### 3.2 border-width
테두리의 두께를 지정
>border-style과 함께 사용하지 않으면 적용되지 않는다.

### 3.3 border-color
테두리의 색상을 지정
>border-style과 함께 사용하지 않으면 적용되지 않는다.

### 3.4 border-radius
테두리 모서리를 둥굴게 표현하도록 지정
- 원의 반지름 값을 이용한 경우
```
/* 4 꼭지점에 대해 Radius 지정 */
border-radius: 5px;
```
- 타원의 가로, 길이를 이용한 경우
```
/* top-left & bottom-right | top-right & bottom-left */
border-radius: 15px 75px;
```
- 모든 모서리에 동일한 둥근 모서리 설정 
```
  border-top-left-radius:     20px;
  border-top-right-radius:    20px;
  border-bottom-right-radius: 20px;
  border-bottom-left-radius:  20px;
```
- 두 개의 반지름을 지정해 타원형 둥근모서리 설정
```
.border-rounded {
  border-top-left-radius: 50px 25px;
}
```
- 각각 모서리에 타원형 둥근 모서리 축약 설정
```
.border-rounded {
  border-radius: 50px 50px 0 0 / 25px 25px 0 0;
}
```

### 3.5 border
width 와 style, color를 한번에 설정하기 위한 shorthand이다.

## 4. box-sizing 프로퍼티
width, height 프로퍼티의 대상 영역을 변경할 수 있다.
> box-sizing 프로퍼티는 상속되지 않는다.
 
width와 height 의 대상:
컨텐츠 -> border
>box-sizingㅍ로퍼티를 사용하기 위해 초기화하는 css
```
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
```
<!--2017.07.22 SuhyeonJo --!>