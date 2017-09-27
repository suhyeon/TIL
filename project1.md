# 요구사항
- 긴 url은 한명의 관리자만 만들 수 있다.
- 긴 url을 짧게 줄인 짧은 url은 누구나 사용할 수 있다.

# 시나리오 설계
- 관리자
  - 로그인
  - url 변환
    - 긴 url을 form에 입력 후 전송
    - 서버에서 url을 변환
    - 결과 확인
    - url이 0일때
      - 현재 생성된 url이 없습니다.
      - 긴 url 입력 인풋 필드(플레이스홀더)
      - 생성 버튼
  - 변환된 url을 리스트 열람
    - 루트 경로(도메인/)에서 열람
  - 짧은 url 접속 가능
- 방문자
  - 변환된 url을 볼 수 없다.
  - 짧은 url 이용가능
    - 방문자 혹은 관리자가 짧은 url을 접속
    - 서버는 301코드를 응답
    - 방문자 혹은 관리자는 url로 리다이렉트
# 화면 설계
- 로그인 화면
  - 팝업창으로 구현할 예정
  - 브라우저내에 내장된 기능
- url목록 화면
  - 테이블 태그를 사용
  - url 목록 현재 생성된 개수 표시
  - 긴url, 짧은 url
# 데이터 설계
- 긴url, 짧은 url 객체
- 객체 1세트를 모아 배열로 구성
- uuid 식별자 사용

## Express 앱세팅
- npm install --save express
- 템플릿 엔진설정
- npm script추가
- static 라우트 설정
- 템플릿, css파일 추가

## 로깅과 인증
- morgan 설정
- express-basic-auth 설정

## 초기 데이터 작업
- randomstring

[작업소스](https://url-xjobpgwfph.now.sh)