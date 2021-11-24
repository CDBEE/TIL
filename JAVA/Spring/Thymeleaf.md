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

## 속성 값 설정

---

타임리프 태그 속성(Attribute) : 타임리프는 주로 HTML 태그에 `th.*` 속성을 지정하는 방식으로 동작한다. `th.*`로 속성을 적용하면 기존 속성을 대체하고 없다면 새로 추가한다.

- `<input type="text" name="abc" th:name="efg" />`

  → `<input type="text" name="efg" />`


### 속성 추가

- `th:attrappend` : 속성 값의 뒤에 값을 추가한다.

  `<input type="text" class="text" th:attrappend="class=' large'"/>`

  → `<input type="text" class="text large"/>`

- `th:attrprepend` : 속성 값의 앞에 값을 추가한다.

  `<input type="text" class="text" th:attrprepend="class='large ' />`

  → `<input type="text" class="large text">`

- `th:classappend` : class 속성에 자연스럽게 값을 추가한다.

  `<input type="text" class="text" th:classappend="large" />`

  → `<input type="text" class="text large" />`


### checked 설정

HTML은 checked 속성이 false인 경우에도 checked 속성이 있는 것으로 판단하기 때문에 체크박스가 체크처리 되어버린다. 타임리프의 `th:checked`는 값이 false인 경우 checked 속성 자체를 제거한다.

## 반복

---

타임리프에서 반복은 `th:each`를 사용한다. 추가로 반복에서 사용할 수 있는 여러 상태값을 지원한다.

### 반복기능

`<tr th:each="user : ${users}">` : users 변수에서 하나씩 꺼내 user변수에 담아 태그를 반복한다.

- `th:each`는 List 뿐만이 아니라 `java.util.Iterable`, `java.util.Enumeration`을 구현한 모든 객체에 사용 가능.

### 반복 상태 유지

`<tr th:each="user, userStat : ${users}">` : 반복의 두 번째 파라미터를 설정해 반복의 상태를 확인할 수 있다.  두 번째 파라미터는 생략이 가능하고, 생략 시 첫 번째 파라미터 + Stat이 된다.

### 반복 상태 유지 기능

- index  : 0부터 시작하는 값
- count : 1부터 시작하는 값
- size : 전체 사이즈
- even, odd : 홀수, 짝수 여부(boolean)
- first, last : 첫 번째, 마지막 여부(boolean)
- current : 현재 객체

## 조건부 평가

---

타임리프의 조건식은 if, unless를 사용한다. 타임리프는 해당 조건이 맞지 않으면 태그 자체를 랜더링 하지 않는다. 만약 다음 조건이 false인 경우 `<span> ... </span>`이 랜더링 되지 않는다.

- `<span th:text="'성인'" th:if="${user.age lt 20}"></span>`

### switch

`<td th:switch="${user.age}">`

- `<span th:case="10"> ... </span>`
- `<span th:case="*"> ... </span>`

  → `*` 은 만족하는 조건이 없을 때 사용하는 디폴트이다.


## 주석

---

1. 표준 HTML 주석 `<!-- -->`

   자바스크립트 표준 HTML 주석은 타임리프가 렌더링하지 않고 남겨둔다.

2. 타임리프 파서 주석 `<!--/* [[${data}]] */-->`

   타임리프 파서 주석은 타임리프의 진짜 주석이다. 렌더링에서 주석 부분을 제거한다.

3. 타임리프 프로토타입 주석 `<!--/*/ ... /*/-->`

   타임리프 프로토타입 주석은 HTML파일을 열었을 때 주석처리가 되어있고, 타임리프 렌더링을 거칠 경우에는 그냥 정상 구문이 된다.


## 블록

---

`<th:block>`은 HTML 태그가 아닌 타임리프의 자체 태그이다. `<th:block>`은 렌더링 시 제거된다.

## 자바스크립트 인라인

---

자바스크립트 인라인은 자바스크립트에서 타임리프를 편리하게 사용할 수 있는 기능이다.

`<script th:inline="javascript">`로 적용한다. 왜 자바스크립트 인라인을 사용해야 하는가?

### 텍스트 렌더링

`var username = [[${user.username}]];`

→ 인라인 사용 전 : `var username = userA;`

→ 인라인 사용 후 : `var username = "userA";`

- 인라인 사용 전을 보면 userA라는 변수이름이 그대로 남아있어 변수명으로 사용되게 되어 오류를 발생시킨다.  인라인 사용 시 문자 타입인 경우 `"`를 포함해준다. 추가로 자바스크립트에서 문제가 발생할 만한 문자가 있다면 이스케이프 처리도 해준다.

### 자바스크립트 내추럴 템플릿

HTML을 직접 열어도 동작하는 내추럴 템플릿을 자바스크립트 인라인 기능을 사용하면 주석을 활용해 기능을 사용할 수 있다. 인라인 사용 후 결과를 보면 주석 부분이 제거되고 기대한 "userA"가 적용된다.

`var username = /*[[${user.username}]]*/ "test username"`

- 인라인 사용 전 :  `var username = /*userA*/ "test username"`
- 인라인 사용 후 :  `var username = "userA";`

### 객체

타임리프의 자바스크립트 인라인 기능 사용 시 객체를 JSON으로 자동 변환해준다. 인라인 사용 전은 객체의 toString()이 호출된 값이다.

`var user = [[${user}]];`

- 인라인 사용 전 : `var user = BasicController.User(username=userA, age=10);`
- 인라인 사용 후 :  `var user = {"username" : "userA", "age" : 10};`

### 자바스크립트 인라인 each

```html
[# th:each="user : ${users}"]
...
[/]
```

## 템플릿 조각

---

웹 페이지 개발 시 여러 페이지에서 함꼐 사용하는 상단영역, 하단영역, 좌측 영역과 같은 공통 영역은 많다. 이 부분들을 하나하나 다 손을 댈 경우 굉장히 비효율적이기 때문에 타임리프는 템플릿 조각과 레이아웃 기능을 지원한다.

### 부분 포함 insert

`<div th:insert="~{template/fragment/footer :: copy}"></div>`

- `template/fragment/footer :: copy` : `template/fragment/footer.html`템플릿에 있는 `th:fragment="copy"`라는 부분을 템플릿 조각으로 가져와 사용한다는 의미이다. insert의 경우 `<div>` 태그 밑에 `<footer>`가 삽입된다.

### 부분 포함 replace

`<div th:replace="~{template/fragment/footer :: copy}"></div>`

- insert와 같은 기능을 하지만 replace 사용 시 `<div>`태그가 `<footer>`태그로 대체된다.

`<div th:replace="template/fragment/footer :: copy"></div>`와 같이 단순 표현식으로 사용도 가능하지만 템플릿 조각을 사용하는 코드가 단순할때만 가능하다.

### 파라미터 사용

파라미터 전달을 통해 동적으로 조각을 렌더링할 수도 있다.

`<div th:replace="~{template/fragment/footer :: copyParam ('데이터1', '데이터2')}></div>`

```html
<footer th:fragment="copyParam (param1, param2)">
	<p th:text="${param1}"></p>
	<p th:text="${param2}"></p>
</footer>
```

이 경우 param1에는 데이터1이, param2에는 데이터2 가 들어간다.

## 템플릿 레이아웃1

---

### 템플릿 레이아웃

템플릿 조각이 일부 코드 조각을 가져와 사용한다면, 코드 조각을 레이아웃에 넘겨서 이용하는 방법도 있다. 예를 들어 `<head>`에 공통으로 사용하는 `css`, `javascript`같은 정보들이 있는데, 이러한 공통 정보들을 한 곳에 모아두고 공통으로 사용하지만 각 페이지마다 필요한 정보를 더 추가해서 사용하고 싶다면 다음과 같이 사용하면 된다.

```html
<head th:fragment="common_header(title, links)">
	<title th:replace="${title}">레이아웃 타이틀</title>
	<!-- 공통 -->
	<link rel="stylesheet" type="text/css" media="all" th:href="@{/css/
	awesomeapp.css}">
	<link rel="shortcut icon" th:href="@{/images/favicon.ico}">
	<script type="text/javascript" th:src="@{/sh/scripts/codebase.js}"></
	script>
	<!-- 추가 -->
	<th:block th:replace="${links}" />
</head>
```

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
	<head th:replace="template/layout/base :: common_header(~{::title},~{::link})">
		<title>메인 타이틀</title>
		<link rel="stylesheet" th:href="@{/css/bootstrap.min.css}">
		<link rel="stylesheet" th:href="@{/themes/smoothness/jquery-ui.css}">
	</head>
	<body>
		메인 컨텐츠
	</body>
</html>
```

```html
<!DOCTYPE html>
<html>
	<head>
		<title>메인 타이틀</title>
		<!-- 공통 -->
		<link rel="stylesheet" type="text/css" media="all" href="/css/awesomeapp.css">
		<link rel="shortcut icon" href="/images/favicon.ico">
		<script type="text/javascript" src="/sh/scripts/codebase.js"></script>
		<!-- 추가 -->
		<link rel="stylesheet" href="/css/bootstrap.min.css">
		<link rel="stylesheet" href="/themes/smoothness/jquery-ui.css">
	</head>
	<body>
		메인 컨텐츠
	</body>
</html>
```

- `common_header(~{::title},~{link})` 부분이 핵심이다.
  - `::title`은 현재 페이지의 title 태그를 전달
  - `::link`는 현재 페이지의 link 태그를 전달

결과를 보면 메인 타이틀은 전달한 부분으로 대체되고, link 로 전달한 부분이 추가되었다.

## 템플릿 레이아웃 2

---

### 템플릿 레이아웃 확장

앞서 나온 개념을 `<head>` 뿐만이 아니라 `<html>` 전체에도 적용 가능하다.