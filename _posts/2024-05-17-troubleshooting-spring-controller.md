---
title: "Spring MVC Cotroller 트러블슈팅"
categories: [Troubleshooting]
tags: [Spring MVC, Troubleshooting]
---

## 발생 개요

![alt text](/image/image2.png)

제목과 내용을 작성하여 저장 버튼을 누르면 ajax 요청으로 서버의 saveMemo 컨트롤러가 호출되는 방식이었다.

![alt text](/image/MemoController.png)

## 발생 오류

### 오류 코드

![alt text](/image/image.png)

네트워크를 살펴보니 /saveMemo 요청에서 http 500 에러가 발생하고 있었다.

500 에러는 서버 측 오류일 때 발생하는 에러로 클라이언트에서는 구체적으로 무슨 에러인지 확인할 수 없다.

서버 콘솔로 가서 오류를 확인해 보자.

### 오류 메시지

> 2024-05-18T11:30:01.151+09:00 ERROR 3152 --- [memo] [io-8080-exec-10] org.thymeleaf.TemplateEngine             : [<span style="color:blue">THYMELEAF</span>][<span style="color:red">http-nio-8080-exec-10</span>] Exception processing template "saveMemo": Error resolving template [saveMemo], template might not exist or might not be accessible by any of the configured Template Resolvers

콘솔에 찍혀있는 오류 메시지이다. Template Resolver가 saveMemo를 못 찾고 있는 거 같다.

saveMemo는 뷰를 반환하지 않는 로직으로 만들었는데 왜 saveMemo라는 뷰를 찾고 있을까..?

## 원인

기본적으로 @Controller는 View Resolver가 이 애노테이션을 보고 뷰를 반환하는 방식이다.

나는 @Controller의 리턴 값을 void로 해두면 뷰를 리턴하지 않는 줄 알았는데 알아보니까 <span style="color:red">@Controller는 리턴 타입 void일 시 요청한 주소 그대로 뷰를 리턴해주는 방식</span>으로 설정이 되는 것이었다. 

saveMemo 로직은 분명 뷰 리턴을 안 했는데 왜 자꾸 saveMemo 뷰를 찾지 못했다고 하는지 알 수 있었다.

## 해결책

saveMemo는 뷰를 리턴할 필요가 없는 로직이다.
게다가 ajax의 saveMemo 호출에 대한 요청 결과도 ajax로 보내줘야 하기 때문에 Data를 리턴해주는 것이 바람직한 거 같다..

@RestController를 따로 만들거나 아니면 @RestController가 @ResponseBody + @Controller이기에 해당 매핑에 @ResponseBody를 추가하여 해결할 수 있다.

일단 나는 규모가 작고 그냥 심심해서 하는 프로젝트였기에 @ResponseBody를 따로 붙이고 ajax에게 요청에 대한 응답도 추가해 주었다..

![alt text](/image/MemoController2.png)

## 결론

그냥 간단한 프로젝트라서 RestController를 작성하기 귀찮아서 컨트롤러에 다 욱여넣다가 발생한 상황이었다.

@Controller의 동작 방식에 대해 아직 미흡한 점이 많아서 붙잡아두고 시간을 좀 버린 거 같은데 앞으로는 이런 실수 안 해야지..