# URI와 웹브라우저 요청 흐름https://www.inflearn.com/course/http-웹-네트워크

Date: October 7, 2021

## URI(Uniform Resource Identifier)

- 크게 URL(URLocater)와 URN(URName)으로 분류 가능
    - **U**niform : 리소스를 식별하는 통일된 방식
    - **R**esource : 자원, URI로 식별할 수 있는 모든 것
    - **I**dentifier : 다른 항목과 구분하는데 필요
    - URL : 리소스가 있는 위치를 지정 / URN : 리소스에 이름을 부여

### URL 문법

- Scheme://[userinfo@]host[:port][/path][?query][#fragment]
- http://www.google.com:443/search?q=hello&hl=ko
    - 프로토콜 - http
    - 호스트명 - www.google.com
    - 포트번호 - 443
    - Path - /search
    - 쿼리 파라미터 - q=hello&hl=ko
- Scheme
    - 주로 프로토콜(어떤 방식으로 자원에 접근할 것인지에 대한 규칙) 사용
    - http : 80포트, https : 443포트를 주로 사용, 포트는 생략이 가능하다.
- UserInfo : URL에 사용자 정보를 포함해서 인증하나 거의 상용하지 않는다.
- Host : 도메인 명이나 IP 주소를 직접적으로 사용 가능
- Port : 접속 포트
- Path : 리소스의 절대 경로
- Query : K - V 형태, ?로 시작하고 &로 추가한다.
- Fragment : 내부 북마크 등에 사용하고 서버에 전송하지는 않는다.

출처 : 

[모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)