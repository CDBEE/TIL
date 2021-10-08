# HTTP 헤더

Date: October 8, 2021

## HTTP 헤더

- HTTP 전송에 필요한 모든 부가 정보를 담고있음
- RFC 2616(과거) → RFC 7230 ~ 7235
- 엔티티(과거) → 표현(Representation)으로 바뀜

## HTTP BODY

- 메시지 본문(Message body / payload)을 통해 표현 데이터를 전달
- 표현 헤더를 표현 데이터를 해석할 수 있는 정보를 제공한다.
    
    → 표현 : 요청이나 응답에서 전달할 실제 데이터
    

## 표현 헤더

- Content-Type : 표현 데이터 형식
    - 미디어 타입, 문자 인코딩
    - e.g) Content-Type : application/json
- Content-Encoding : 표현 데이터의 압축 방식
    - 표현 데이터의를 압축하기 위해 사용, 전달하는 곳에서 압축 후 인코딩 헤더 추가
    - 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- Content-Language : 표현 데이터의 자연 언어
    - e.g) ko-KR, en
- Content-Length : 표현 데이터의 길이
    - 바이트 단위

## 협상(Content Negotiation)

→ 클라이언트가 선호하는 표현 요청, 요청 시에만 사용

- Accept : 선호하는 미디어 타입 전달
- Accept-charset : 선호하는 문자 인코딩
- Accept-Encoding : 선호하는 압축 인코딩
- Accept-Language : 선호하는 자연 언어

### 협상 우선 순위

- Quality Value(q) 사용
- 0~1, 클수록 높은 우선 순위. 생략 시 1
- e.g) Accept-Language: ko-KR;ko;q=0.9
- 구체적인 것이 우선
- e.g) Accept: text/*, text/plain, text/plain;format=flowed
    
    → text/plain;format=flowed → text/plain → text/*
    

## 전송 방식

- 단순 전송 : Content-Length
- 압축 전송 : Content-Encoding
- 분할 전송 : Transfer-Encoding (사용 시 Content-Length 사용 불가)
- 범위 전송

### 일반 정보

- From : 유저 에이전트의 이메일 정보
    - 검색 엔진에서 주로 사용(요청)
- Referer : 이전 웹 페이지 정보
    - 요청 페이지의 이전 주소, 유입 경로 분석 가능
- User-Agent : 유저 에이전트 애플리케이션 정보
    - 웹 브라우저 정보, 등등
- Server : 요청을 처리하는 오리진 서버의 소프트웨어 정보
    - 응답에서 사용
- Date : 메시지가 생성된 날짜
    - 응답에서 사용

### 특별한 정보

- Host : 요청한 호스트 정보(도메인)
    - 필수 정보
    - 하나의 서버가 여러 도메인을 처리해야할 때 사용
- Location : 페이지 리다이렉션
    - Location 헤더가 있고 3xx 응답 결과라면 Location 위치로 자동 이동
- Allow : 허용 가능한 HTTP 메서드
    - 405 Method not allowed 응답에 포함
- Retry-After : 다음 요청까지 기다려야 하는 시간

출처 :
[모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)