# HTTP 메서드의 활용

Date: October 8, 2021

## 클라이언트 ↔ 서버 간 데이터의 전송

→ 두 가지 전달 방식이 존재

1. Query Parameter를 통한 데이터의 전송(GET)
    1. 주로 정렬 필터로 사용
2. 메시지 바디를 통한 데이터 전송(POST, PUT, PATCH)

→ 4가지 정도의 상황이 존재

- 정적 데이터 조회
    - 쿼리 파라미터를 미사용하며 이미지나 정적 텍스트 문서를 조회(GET)
- 동적 데이터 조회
    - 쿼리 파라미터 사용, 검색 대상을 정렬하는 정렬 필터나 줄여주는 필터에 주로 사용
    - GET 사용
- HTTP Form을 통한 데이터 전송
    - GET, POST 사용 가능. GET은 조회, POST는 저장
    - Content-Type : application/x-www-form-urlencoded
    - →전송 값은 보통 K-V 형태로 메시지 바디를 통해 전송
    - Content-Type : multipart/form-data
    - → 파일 전송
- HTTP API를 통한 데이터 전송
    - 서버 to 서버, 앱 클라이언트, 웹 클라이언트 등에서 사용
    - Content-Type : application/json이 거의 표준
    

## API 설계 - POST 기반 등록(회원 관리)

- resource 목록 : /resources → GET
- resource 등록 : /resources → POST
- resource 조회 : /resources/{id} → GET
- resource 수정 : /resources/{id} → PATCH, PUT, POST
- resource 삭제 :  /resources/{id} → DELETE

→ 클라이언트는 등록될 리소스의 URI를 모름

→ 서버가 새로 등록된 리소스의 URI 생성

→ 컬렉션 존재

## API 설계 - PUT 기반 등록(파일 관리)

- 파일 목록 : /files → GET
- 파일 조회 : /files/{name} → GET
- 파일 등록 : /files/{name} → PUT
- 파일 삭제 : /files/{name} → DELETE
- 파일 대량 등록 : /files → POST

→ 클라이언트가 리소스의 URI를 알고 있어야 함

→ 클라이언트가 직접 리소스의 URI를 지정

→ 스토어 존재

## HTML FORM

→ 컨트롤 URI

- GET, POST만 지원하기 때문에 제약이 존재
- → 동사로 된 리소스 경로를 사용(컨트롤 URI)
- HTTP 메서드로 해결하기 애매한 경우 사용

### 참고하면 좋은 URI 설계 개념

- 문서(Document)
    - 단일 개념(파일 하나, 객체 인스턴스, DB row)
- 컬렉션(Collection)
    - 서버가 관리하는 리소스 디렉토리
    - 서버가 리소스의 URI를 생성하고 관리
- 스토어(Store)
    - 클라이언트가 관리하는 자원 저장소
    - 클라이언트가 리소스의 URI를 생성하고 관리
- 컨트롤러(Controller), Controll URI
    - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
    - 동사를 직접 사용

출처 :
[모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)
