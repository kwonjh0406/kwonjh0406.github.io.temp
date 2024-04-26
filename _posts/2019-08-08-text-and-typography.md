---
title: (JAVA) String, StringBuffer, StringBuilder 정리
description: Examples of text, typography, math equations, diagrams, flowcharts, pictures, videos, and more.
date: 2022-08-08 11:33:00 +0800
categories: [언어, Java]
tags: [java]
pin: true
math: true
mermaid: true
---

> #### String

String으로 생성된 문자열은 불변이다.
기본적으로 String으로 문자열을 생성하면 Java Literal Pool이라는 공간의 문자열을 참조한다. String 문자열의 수정이 발생하면 그 수정된 문자열이 새로 Java Literal Pool에 등록이 되고(이미 JLP에 존재하면 등록 X) 해당 문자열을 새로 참조하는 방식으로 문자열 수정이 이루어진다.

*String을 리터럴 방식이 아닌 new로 생성하면 얘기가 다른데 이는 권장되지 않는 방식이다.

> #### StringBuffer

String과 달리 가변 문자열이다.
참조하는 문자열 공간에서 수정이 이루어지며 기본적으로 동기화 기능을 지원하는 클래스(메서드에는 synchronized 키워드가 붙어있음)이기에 스레드로부터 안전하다. <- 즉 여러 스레드가 StringBuffer의 메서드를 동시에 접근 못함

> #### StringBuilder

StringBuffer와 마찬가지로 가변 문자열이다.
StringBuilder와의 차이점으로는 동기화가 되어있지 않아 스레드로부터 안전하지 않다. 하지만 String이나 StringBuffer에 비하여 속도가 훨씬 빠르다.

#### 결론

현재 상황에 맞는 것을 사용해야 한다.

문자열을 못 박아두고 거의 수정할 일이 없다? String
다중 스레드 환경이다? StringBuffer
단일 스레드 환경이다? StringBuilder