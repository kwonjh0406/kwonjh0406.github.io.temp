---
title: "[JAVA] Optional 클래스"
categories: [언어, JAVA]
tags: JAVA
---

Spring JPA 공부를 하다가 처음 만난 Optional.<br>

JPA Repository를 이용하여 데이터를 꺼내면 해당 객체가 아닌 Optional로 한번 감싼 Optional 객체가 반환 되도록 구현이 되어있다.
Optional 객체란 무엇일까?

## 자바의 Optinal 클래스란?

---

Optional 클래스의 목적은 <span style="color:red">**객체를 반환할 때 Null Pointer Exception을 방지**</span>하기 위함이다.

간단하게 예를 들어보자.<br>
findById(id)라는 id의 값으로 해당 id의 객체를 반환하는 함수가 존재한다.<br>
id의 값으로 5를 넘겨줘서 객체를 반환받고 싶은데 id가 5인 객체가 없다.<br>
그러면 NULL 객체가 반환될 것이고 Null Pointer Exception이 발생한다.<br>
이를 방지하기 위해서는 직접 NULL 객체 반환 상황에 대한 로직을 작성해 줘야 될 것인데
Optional을 사용하면 NULL을 직접적으로 다루지 않기에 NPE가 생기는 일이 방지되고 다양한 Optinal의 기능으로 NULL 객체에 대한 유연한 대처가 가능하다.

## Optional 객체 생성 방법

---

### Optional.empty()
비어있는 Optional 객체(Optional EMPTY 객체)를 반환해 줍니다.

### Optional.of(T)

>객체가 NULL이 아닌 경우에만 사용하자.

객체를 Optional로 감싸 반환합니다.
근데 Optional.of(T)의 경우는 객체가 NULL인 경우 Null Pointer Exception이 발생합니다. 이를 해결하기 위해 Optional.ofNullable(T)이 있습니다.

### Optional.ofNullable(T)

객체를 Optional로 감싸는데 Optional.of(T)와 다르게 객체가 NULL이면 비어있는 Optional 객체를 반환해 줍니다.

## Optional 객체 사용법

---

### optional.get()

Optional 객체가 감싸고 있는 객체를 그대로 꺼내온다.<br>
이 경우 근데 감싸고 있는 객체가 NULL인 경우 NULL을 그대로 꺼내와 NPE가 터질 수 있다.<br>
따라서 객체가 존재하는지 확인하는 로직(isPresent 같은)이 선행되어야 안전한 방법이다.

### optional.isPresent()

Optional에 객체가 존재하면 true를 비어있다면 false를 반환한다.

### optional.orElse(T)

optional 객체가 존재한다면 그 객체를, 존재하지 않는다면 지정된 객체를 반환한다.
특징으로는 객체가 존재하든 안 하든 일단 orElse() 코드는 항상 동작한다.

### optional.orElseGet(()->{})

Optional 객체가 존재한다면 그 객체를, 존재하지 않는다면 인수로 지정된 람다식의 리턴 값을 반환한다.
orElse와의 차이점은 객체가 존재하지 않는 경우에만 동작한다.

### optional.orElseThrow(()->{})

Optional 객체가 존재한다면 그 객체를, 존재하지 않는다면 지정된 예외를 발생시킨다.

## Optional 결론

---

null이 반환될 수도 있는 로직이라면 null 대신에 반환 타입을 Optional로 하고 Optional.empty()로 null 역할을 하게 하자!<br>
Optinal 클래스는 반환 타입을 위해 설계된 클래스이다.<br>
따라서 그 외의 경우 (필드 타입)로 Optional을 사용하는 것은 권장되지 않는다.<br>
그리고 Optional 남발은 코드 품질 및 성능의 저하로 이어지므로 꼭 필요한 상황에만 사용하자!