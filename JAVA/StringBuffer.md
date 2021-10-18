# StringBuffer

Date: October 18, 2021

# StringBuffer 클래스

## String 클래스란?

- 문자열 객체다.
- + 연산자를 통해 문자열을 이을 수 있다.
- 수정이 불가능하다는 특징이 있다.

## String 형 객체가 더해지는 방식

- String형 + String형을 한다고 기존의 것에 더해지는 것이 아니라 아예 새로운 String형 객체를 탄생시킨다.

  → 메모리 낭비와 속도 낭비가 심하다.

- JDK 1.5이후 String의 + 연산자가 StringBuilder의 append로 자동 변환되긴 하지만 그래도 오래 걸린다.

## 이를 해결하기 위한 StringBuffer/StringBuilder 클래스

- StringBuffer/StringBuilder 클래스의 경우 생성자로 생성 이후 append() 메서드를 통해 문자열을 더할 수 있다.
- delete/setCharAt/insert 등 다양하고 유용한 메서드들을 제공한다.
- 연산자의 사용 횟수가 많아지면 많아질수록 StringBuffer/Builder 클래스가 압도적으로 빠른 속도를 보인다.

![http://pds24.egloos.com/pds/201201/23/45/d0139645_4f1d1b70db761.png](http://pds24.egloos.com/pds/201201/23/45/d0139645_4f1d1b70db761.png)

출처 :

[String, StringBuffer, StringBuilder 속도 실험 (시간 측정)](http://egloos.zum.com/deblan2/v/419830)

## StringBuffer와 StringBuilder의 차이점

- StringBuffer의 경우 동기화를 지원하며 멀티쓰레드 환경에서 안전하다.
- StringBuilder는 동기화를 지원하진 않지만 단일쓰레드 환경에서는 StringBuffer보다 빠르다.