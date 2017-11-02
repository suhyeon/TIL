# CSS - WEBDESIGN

## 1. Resposive Web Deseign 개요
하나의 웹사이트를 구축해 다양한 디바이스의 화면 해상도에 최적화된 웹사이트를 제공하는 것

> layout은 방문자의 화면 해상도를 고려해야 한다.

- 각 디바이스별 size
    - desktop : 1024 +
    - tablet : 1023 ~ 768
    - phone device : 767 ~ 320

`최근 트렌드인 web app framework`  
[ionic](http://ionicframework.com/)  
[Electron](https://electron.atom.io/)  
[phoneGap](https://phonegap.com/)  
[sench touch](https://www.sencha.com/)

---
### 1. Viewport Meta Tag
viewport를 이용해 디바이스의 특성과 디바이스의 화면크기등을 고려해 각종 디바이스 사용자에게 최적화된 웹페이지를 제공할 수 있다.  

viewport : 웹페이지의 가시 영역  
>디바이스에 따라 차이가 있다.

`meta tag는 브라우저 혹은 SEO를 위해 검색엔진에게 메타데이터를 전달하기 위해 사용된다.`

>일반적으로 viewport meta tag는 모바일 디바이스에서만 적용된다.

```
//가장 일반적인 viewport 설정
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 2. @media
서로다른 미디어 타입에 따라 각각의 styles 를 지정하는 것을 가능하게 한다.

> 반응형 웹디자인에 사용되는 핵심기술이다.

`@media 를 사용해 미디어 별로 style을 지정한는 것 : Media Query

- Media Query 디바이스별 분류
```
/*==========  Mobile First Method  ==========*/
/* All Device */

/* Custom, iPhone Retina : 320px ~ */
@media only screen and (min-width : 320px) {

}
/* Extra Small Devices, Phones : 480px ~ */
@media only screen and (min-width : 480px) {

}  
/* Small Devices, Tablets : 768px ~ */
@media only screen and (min-width : 768px) {

}
/* Medium Devices, Desktops : 992px ~ */
@media only screen and (min-width : 992px) {

}
/* Large Devices, Wide Screens : 1200px ~ */
@media only screen and (min-width : 1200px) {

}

/*==========  Non-Mobile First Method  ==========*/
/* All Device */

/* Large Devices, Wide Screens : ~ 1200px */
@media only screen and (max-width : 1200px) {

}
/* Medium Devices, Desktops : ~ 992px */
@media only screen and (max-width : 992px) {

}
/* Small Devices, Tablets : ~ 768px */
@media only screen and (max-width : 768px) {

}
/* Extra Small Devices, Phones : ~ 480px */
@media only screen and (max-width : 480px) {

}
/* Custom, iPhone Retina : ~ 320px */
@media only screen and (max-width : 320px) {

}
```
## 2. Responsive Navigation Bar
디바이스 해상도에 따라 반응할 수 있도록 viewport meta tag 와 media query를 추가한다.
