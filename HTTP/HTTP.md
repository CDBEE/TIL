# HTTP

Date: October 7, 2021

# HTTP(HyperText Transfer Protocol)

## 모든 것이 HTTP이다 - HTTP 메시지에 모든 것을 전송

- 거의 모든 형태의 데이터가 전송이 가능하다.
- 서버간 데이터 전송 시에도 대부분 HTTP를 사용
- HTTP/1.1, HTTP/2, HTTP/3 등 여러 버전이 있으나 1.1이 제일 많이 쓰임
- TCP는 HTTP/1.1, HTTP/2를 기반, UDP는 HTTP/3에서 많이 쓰임

## 특징

- 클라이언트 - 서버 구조로 되어있다.
    - Req - Res 구조, 클라이언트가 서버에 요청을 보내고 응답을 대기한다.
- Stateless Protocol
    - 서버가 클라이언트의 상태를 보존하지 않는다.
    - 이로인해 확장성은 높아지나 데이터의 양이 많아짐
    - 응답서버를 쉽게 바꿀 수 있다 → 서버 증설이 쉬워진다.
    - 모든 것을 Stateless로 설계할 수는 없으나 Stateful은 최소한만 사용
- 비연결성
    - 요청이 오면 응답 후 TCP/IP 연결이 끊어진다.
    - → 이로 인해 서버의 자원이 프리해짐
    - 단점 : 연결시마다 새로 TCP 3 way handshake 필요 → 추가 시간 소요 및 자원 소모
    - → 해당 단점은 HTTP 지속연결(Persistent Connection)으로 해결된다.
- HTTP 메시지
    - HTTP에 모든 것을 담아 전송한다.
- 단순하고 확장이 가능하다.

## HTTP 응답 메시지

### 시작 라인(요청 메시지)

- 요청 메시지(Request Line) : method SP(공백) request-target SP HTTP-version SP CRLF(엔터)
    - Method : GET, POST, PUT, PATCH, ...
    - Request-target : 절대경로로 시작하는 경로 + ?query
    - HTTP-version

### 시작라인(응답 메시지)

- 응답 메시지(Status Line) : HTTP-version SP status-code SP reason-phrase CRLF
    - HTTP-version
    - Status-code : 200, 400, 404, ...
    - Reason-phrase : 짧은 설명 상태 코드(OK)

### HTTP 헤더

- Header-field = field-name":" OWS(띄어쓰기 허용) field-value OWS
    - e.g) Content-type: text/html
- HTTP 전송에 필요한 모든 부가정보를 담는다.

### HTTP 메시지 바디

- 실제로 전송할 데이터를 담는다.
- byte형태로 표현이 가능한 모든 데이터가 전송 가능 범주

출처 :
[모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)