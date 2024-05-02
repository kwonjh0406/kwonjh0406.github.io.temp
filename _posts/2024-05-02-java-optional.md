---
title: "[JAVA] Optional이란 무엇인가?"
categories: [언어, JAVA]
tags: JAVA
---

Spring JPA 공부를 하다가 처음 만난 Optional.<br>
JpaRepository를 이용하여 데이터를 꺼내면 해당 객체가 아닌 Optional로 한번 감싼 Optional 객체가 반환된다.
Optional 객체란 무엇일까?

---

## 자바의 Optinal 클래스란?

Optional 클래스의 목적은 <span style="color:red">**객체의 Null Pointer Exception을 방지**</span>하기 위함이다.

간단하게 예를 들어보자.<br>
findById(id)라는 id의 값으로 해당 id의 객체를 반환하는 함수가 존재한다.<br>
id의 값으로 5를 넘겨줘서 객체를 반환받고싶은데 id가 5인 객체가 없다.<br>
그러면 NULL 객체가 반환될 것이고 Null Pointer Exception이 발생한다.<br>
이를 방지 하기 위해서는 직접 NULL 객체 반환 상황에 대한 로직을 작성해줘야될 것인데
Optional을 사용하면 NULL이 아닌 디폴트 값이 존재하여 NPE가 생길 일이 1차적으로 방지되고 
다양한 Optinal의 기능으로 NULL객체에 대한 유연한 대처가 가능하다.

---

## Optional 객체 생성 방법

## Optional 객체 사용법

### Optional.get()

Optional 객체가 감싸고 있는 객체를 그대로 꺼내온다.<br>
이 경우 근데 감싸고 있는 객체가 NULL 인 경우 NULL을 그대로 꺼내와 NPE가 터질 수 있다.<br>
따라서 객체가 존재하는지 확인하는 로직이 선행되어야 안전한 방법이다.

### Optional.orElse() 종류

#### orElse()

#### orElseGet()

#### orElseThrow()

### 

## Optional의 주의사항

Optinal 클래스는 반환 타입을 위해 설계된 클래스이다.

따라서 그 외의 경우 (필드 타입)로 Optional을 사용하는 것은 권장되지 않는다.

그리고 Optional 남발은 코드 품질 및 성능의 저하로 이어지므로 꼭 필요한 상황에만 사용하자!