# CSS-DISPLAY 프로퍼티

LAYOUT정의에 자주 사용되는 중요한 프로퍼티

- block : block특성을 가지는 요소
- inline : inline 특성을 가지는 요소
- inline-block : inline-block 특성을 가지는 요소
- none : 해당 요소를 화면에 표시하지 않는다.
>display 프로퍼티는 상속되지 않는다.

## 1.1 block 레벨 요소
- ` 항상 새로운 라인 `에서 시작한다.
- `화면 크기 전체의 가로폭`을 차지. (width: 100%)
- width, height, margin, padding 프로퍼티 지정이 가능
- block레벨 요소내에 inline 레벨요소를 포함가능
  - ex) div,h1~h6,p,ol,...

## 1.2 inline 레벨 요소
- 줄을 바꾸지 않고 다른 요소와 함께 `한 행에 위치`한다.
- 컨텐츠의 너비만큼 가로폭을 차지
- `width, height, margin-top, margin-bottom 프로퍼티를 지정할 수 없다.`
- inline레벨 요소뒤에 공백이 있으면, 정의하지 않은 `space 4px이 자동지정`된다.
- inline 레벨 요소내에 block 레벨 요소를 포함할 수 없다.
    - ex) span, a, strong, img, br, input,..

## 1.3 inline-block 레벨 요소
`inline 레벨 요소와 같이 한 줄에 표현 되면서 width, height, margin 프로퍼티를 모두 지정할 수 있다.`

```
inline-block {
  display: inline-block;
}
```
- inline레벨 요소뒤에 공백이 있는 경우, 정의하지 않은 `space 4px`이 자동지정.  
[회피방법 참조 사이트](https://css-tricks.com/fighting-the-space-between-inline-block-elements/)

## 2. visibility 프로퍼티
  요소의 렌더링 여부를 결정한다.
  - visible : 해당 요소를 보이게 한다.
  - hidden : `display: none;은 해당요소의 공간까지 사라지게 하지만, hidden은 해당요소의 공간은 사라지지 않고 컨텐츠만 안보인다.`

## 3. opacity 프로퍼티
요소의 투명도를 정의한다.
>0.0 ~ 1.0의 값을 입력  
>0.0 : 투명  
>1.0 : 불투명  

`effect = transition: opacity 1s; : 약간의 부드러운 액트를 표현한다.`
<!--2017.07.22 SuhyeonJo --!>