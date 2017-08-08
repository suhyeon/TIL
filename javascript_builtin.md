# JAVASCRIPT - BUILT-IN OBJECT
BUILT-IN OBJECT(내장 객체) : 웹페이지 등을 표현하기 위한 공통의 기능을 제공한다.

- STANDARD BUILT-IN OBJECTS(GLOBAL OBJECTS)
- BOM (BROWSER OBJECT MODEL)
- DOM (DOCUMENT OBJECT MODEL)

STANDARD BUILT-IN OBJECTS : 표준 빌트인 객체  
NATIVE OBJECT : BOM,DOM  
HOST OBJECT(사용자 정의객체) : 사용자가 생성한 객체

## 1. STANDARD BUILT-IN OBJECTS(GLOBAL OBJECTS)
일반적으로 String, Array와 같이 대문자로 시작한다.  
global object와 다른의미로 사용되므로 혼동에 주의!!

## 2. BOM(BROWSER OBJECT MODEL)
브라우저 객체 모델 : 브라우저 탭 또는 브라우저 창의 모델을 생성  
최상위 객체 : WIDNOW 객체  
> 현재 브라우저 창 또는 탭을 표현하는 객체  

`이 객체들은 STANDARD BUILT-N OBJECTS가 구성된 후에 구성된다.`
- WINDOW : 현재 브라우저 창 또는 탭
- document : 현재 로드된 웹페이지
- history : 브라우저 히스토리에 기록된 웹페이지
- location : 현재 페이지 url
- navigator : 브라우저 관련 정보
- screen : 장치의 디스플레이 정보

## 3. DOM (DOCUMENT OBJECT MODEL)
브라우저가 자동 생성. 문서 객체 모델 : 현재 웹페이지의 모델을 생성한다.  
최상위 객체 : DOCUMENT 객체 : 전체 문서를 표현한다.  

> 이 객체의 자식 객체들은 문서의 다른 요소들을 표현한다.