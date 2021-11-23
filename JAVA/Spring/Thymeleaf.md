# Thymeleaf

Date: 2021년 11월 22일

# 타임리프

---

## 타임리프란?

- 서버 사이드 HTML 렌더링(SSR)

  타임리프는 백엔드 서버에서 HTML을 동적으로 렌더링 하는 용도로 사용된다.

- 네츄럴 탬플릿

  타임리프는 **순수 HTML**을 최대한 유지하는 특징이 있다. 타임리프로 작성된 파일은 HTML을 유지하기 때문에 웹 브라우저나 직접 열어도 내용을 확인할  수 있고, 서버에서는 동적으로 렌더링 된 결과물을 확인할 수 있다. 순수 HTML을 유지하면서 뷰 템플릿도 사용할 수 있는 타임리프의 특징을 **네츄럴 탬플릿이라고 한다.**

- 스프링 통합 지원

  타임리프는 스프링과 자연스럽게 통합되고 다양한 기능을 사용할 수 있도록 지원한다.


### 타임리프의 선언

`<html xmlns:th="http://www.thymeleaf.org">`

## 타임리프의 기본 표현식

- 간단한 표현
  - 변수 표현식 : `${ ... }`
  - 선택 변수 표현식 : `*{ ...}`
  - 메시지 표현식 : `#{ ... }`
  - [링크 URL 표현식]() : `@{ ... }`
  - 조각 표현식 : `~{ ... }`
- [리터럴]()
  - [텍스트]() : `'one text', 'Another text', ...`
  - 숫자 :  `0, 34, 3.0, 12.3, ...`
  - 불린 : `true, false`
  - 널 : `null`
  - 리터럴 토큰 : `one, some text, main, ...`
- [연산자]()
  - 문자 연산 :
    - 문자 합치기 : `+`
    - 리터럴 대체 : `|The name is ${name}|`
  - 산술 연산 :
    - Binary Operators : `+, -, *, /, %`
    - Unary Opertor : `-`
  - 불린 연산 :
    - Binary Operators : `and, or`
    - Unary Operator : `!, not`
  - 비교와 동등 :
    - 비교 : `>, <, >=, <= (gt, lt, ge, le)`
    - 동등 연산 : `==, != (eq, ne)`
  - 조건 연산 :
    - If-then : `(if) ? (then)`
    - If-then-else : `(if) ? (then) : (else)`
    - Default : `(value) ?: (defaultValue)`
  - 특별한 토큰 :
    - No-operation : `_`

## 텍스트

---

기본 기능인 텍스트를 출력하는 기능. HTML의 콘텐츠에 데이터를 출력 시 `th:text`를 사용한다.

- `<span th:text="${data}">`

HTML 태그의 속성이 아닌 HTML 콘텐츠 영역 안에서 직접 테이터를 출력 시 `[[ ... ]]`를 사용한다.

- `<li> 직접 출력 = [[${data}]]</li>`

### Escape

웹브라우저는 <를 HTML 태그의 시작으로 인식한다. 그래서 <를 태그의 시작이 아닌 문자로 표현할 방법이 필요한데, 이를 **HTML 엔티티**라고 한다. 그리고 특수 문자를 HTML 엔티티로 바꾸어주는 것을 **Escape**라고 한다. `th:text`, `[[ ... ]]` 는 기본적으로  Escape를 지원한다.

### UnEscape

이스케이프 기능을 사용하지 않고 싶을 때도 있다. 그때는 `th:utext`, `[( ... )]` 를 사용하면 된다.

## Spring EL

---

변수 표현식에서는 스프링 EL이라는 스프링이 제공하는 표현식을 사용 가능하다.

### Object

- `user.username` : user의 username을 프로퍼티 접근

  → `user.getUsername()`

- `user['username']` : 위와 같음
- `user.getUsername()` : user의 `getUsername()`을 직접 호출

### List

- `user[0].username` : List에서 첫 번째 회원을 찾고 username 프로퍼티 접근

  →`list.get(0).getUsername()`

- `user[0]['username']`: 위와 같음
- `user[0].getUsername()` : List에서 첫 번째 회원을 찾고 메서드 직접 호출

### Map

- `userMap['userA'].username` : Map에서 userA를 찾고, username 프로퍼티 접근

  → `map.get("userA").getUsername()`

- `userMap['userA']['username']` : 위와 같음
- `userMap['userA'].getUsername()` : Map에서 userA를 찾고 메서드 직접 호출

### 지역 변수 선언

th:with를 사용하면 지역 변수를 선언해서 사용 가능하다. 지역 변수는 선언한 태그 안에서만 사용할 수 있다.

```html
<div th:with="user=${users[0]}">
	<p>처음 사람의 이름은 <span th:text="${user.username}"></span></p>
</div>
```

## 기본 객체들

---

타임리프는 기본 객체들을 제공한다.

- ${#request}
- ${#response}
- ${#session}
- ${#servletContext}
- ${#locale}
- HTTP 요청 파라미터 접근 : param

  → `${param.paramData}`

- HTTP 세션 접근 : session

  → `${session.sessionData}`

- 스프링 빈 접근 : @

  → `${@helloBean.hello('Spring!')}`


## 유틸리티 객체와 날짜

---

타임리프는 문자, 숫자, 날짜, URI 등을 편리하게 다루는 다양한 유틸리티 객체들을 제공

- `#message` : 메시지, 국제화 처리
- `#uris` : URI 이스케이프 지원
- `#dates` : [java.util.Date](http://java.util.Date) 서식 지원
- `#calendars` : java.util.Calendar 서식 지원
- `#temporals` : 자바 8 날짜 서식 지원
- `#numbers` : 숫자 서식 지원
- `#strings` : 문자 관련 편의 기능
- `#objects` : 객체 관련 기능 제공
- `#bools`  : boolean 관련 기능 제공
- `#arrays` : 배열 관련 기능 제공
- `#list, #sets, #maps` : 컬렉션 관련 기능 제공
- `#ids` : 아이디 처리 관련 기능 제공

## URL 링크

타임리프에서 URL 생성 시 `@{ ...`  를 사용한다.

- 단순 URL : `@{/hello}`

  `-> /hello`

- 쿼리 파라미터

  `@{/hello(param1=${param1}, param2=$param2})}`

  → `/hello?param1=data1&param2=data2`

- 경로 변수

  `@{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})}`

  → `/hello/data1/data2`

- 경로 변수 + 쿼리 파라미터

  `@{/hello/{param1}(param1=${param1}, param2=${param2})}`

  → `/hello/param1?param2=data2`


## 리터럴

---

소스 코드 상에서 고정된 값을 말하는 용어

- 문자 리터럴 : 타임 리프에서 문자 리터럴은 항상 '로 감싸야 한다.
- 리터럴 대체 : 리터럴 대체 문법을 사용하면 편리하다.

  → `<span th:text="|hello ${data}|">`


## 연산자

---

타임리프 연산은 HTML 엔티티를 사용하는 부분만 조심하고 나머지는 자바와 다르지 않다.

- 비교연산 : `>(gt), <(lt), >=(ge), <=(le), !(not), ==(eq), !+(neq,ne)`
- 조건식 : 자바의 조건식과 유사
- Elvis 연산자 : 조건식의 편의 버전
  - `<li>${data} >: 데이터가 없습니다.' </li>`

    → data가 null이면 데이터가 없습니다.를 출력, 그 외에는 data 출력

- No-Operation : _ 인 경우 타임리프가 실행되지 않은 것 처럼 동작한다.