# CSS - SYNTAX  
## 1. 셀렉터 ( 선택자)

스타일을 적용하고자 하는 HTML 요소를 선택하는 것

```
h1 { color: red; font-size: 12px;}
```
- h1 : 셀렉터
- color, font-size : 프로퍼티
- red, 12px : 프로퍼티 값

> 스타일 시트 : rule set의 집합

## 2. 프로퍼티 (Property / 속성)
다양한 style을 적용할 수 있다.
>표준 스펙으로 이미 지정되어 있는 것을 사용해야 한다. 
```
p {
  color: ...;
  font-size: ...;
}
```

## 3. 값 (Value / 속성값)
키워드, 크기단위, 색상표현단위 등의 특정단위를 지정해야 한다.
```
p {
  color: orange;
  font-size: 16px;
}
```
## 4. HTML과 CSS 연동
---
### 1. Link Style
html에서 외부에 있는 css파일을 로드하는 방식
> 가장 일반적인 사용법

```
  <head>
    <link rel="stylesheet" href="css/style.css">
  </head>
```
### 2. Embedding Style
html 내부에 css를 포함시키는 방식.
> html과 css는 서로 역할이 다르기에 다른 파일로 구분해 작성하고 관리되는 것이 바람직하다.

```
  <head>
    <style>
      h1 { color: red; }
      p  { background: aqua; }
    </style>
  </head>
```
### 3. Inline Style
html요소의 style 프로퍼티에 css를 기술하는 방식
>Javascript가 동적으로 css를 생성할 때 사용하는 경우가 있다.  
`Link style을 사용하는 편이 좋다.`

## 5. Reset CSS 사용하기
기본적인 html요소의 css를 초기화하는 용도로 사용한다.
> 크로스브라우징을 위해 주의해야한다.

`Eric Meyer's reset css`
```
/* http://meyerweb.com/eric/tools/css/reset/
  v2.0 | 20110126
  License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
```
<!--2017.07.22 SuhyeonJo --!>