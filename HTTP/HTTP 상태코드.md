# HTTP 상태코드

Date: October 8, 2021

## 상태코드

→ 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1xx(Informational) → 요청 수신 후 처리 중
- 2xx(Successful) → 성공적으로 처리
    - 200 OK : 요청 성공
    - 201 Created : 요청 성공되어 새로운 리소스 생성됨
    - 202 Accepted : 접수 후 미처리 상태(배치 처리 시 사용)
    - 204 No Content : 요청 성공이지만 같은 화면 유지
- 3xx(Redirection) → Location 헤더의 위치로 자동 이동
    
    → 영구 리다이렉션 : 요청된 URI가 아예 바뀐 경우
    
    - 301 Moved Permanently : Redirect 시 요청 메서드가 GET으로 변하고 본문이 제거될 수 있음
    - 308 Permanent Redirect : 요청 메서드와 본문 유지
    
    → 일시 리다이렉션 : 일시적인 변경(e.g 주문 완료 후 주문 내역화면 이동)
    
    - 302 Found : Redirect 시 요청 메서드가 GET으로 변하고 본문이 제거될 수 있음
    - 303 See Other : 요청 메서드가 GET으로 변경
    - 307 Temporary Redirect : 요청 메서드와 본문 유지
    - PRG(Post/Redirection/Get) : 주문 시 POST로 주문 후 주문 결과 화면을 GET으로 리다이렉트
        
        → 중복 주문을 방지해줌
        
    
    → 특수 리다이렉션
    
    - 300 Redirection : 미사용
    - 304 Not Modified : 리소스가 수정되지 않았음을 알림, 주로 캐시 사용
- 4xx(Client Error) : 오류의 원인이 클라이언트에 존재, 똑같은 재시도가 실패함
    - 400 Bad Request : 잘못된 요청으로 서버가 처리할 수 없음
        
        → 요청 내용을 클라이언트가 다시 검토하고 보내야 함.
        
    - 401 Unauthorized : 인증되지 않았음( 로그인 같은)
    - 403 Forbidden : 승인 거부(접근 권한 불충분)
    - 404 Not Fuond : 해당 리소스가 서버에 없음
- 5xx(Server Error) : 서버 오류
    - 500 Internal Server Error : 서버 내부 문제
    - 503 Service Unavailable : 서비스 이용 불가

출처 :
[모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)