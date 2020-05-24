test
=====
* 공부하며 간략한 기능 구현을 연습해보기 위한 저장소(~2020.05.24)
* 관련 내용들을 기록
- - -
## 목차
1. [화면에서 서버로 데이터 넘기기](#화면에서-서버로-데이터-넘기기)
	1. [개발환경](#개발환경)
	2. [화면 그리기](#화면-그리기)
	3. [데이터 처리하기](#데이터-처리하기)
	4. [기타](#기타)
2. .

## 화면에서 서버로 데이터 넘기기
### 개발환경
> * 언어: JAVA8
> * 프레임워크: SPRINGBOOT
> * 데이터베이스: H2
> * 빌드: MAVEN
> * 기타: JSP(JSTL), SL4J

- - -

1. DB: H2
	* 인메모리 데이터베이스로 주로 메모리에 데이터 저장 용도(∴ 휘발성)
	* 유의할 점
		1. 데이터베이스를 사용하기 위해서는 의존성의 scope를 `runtime`으로 설정(pom.xml)
		2. 브라우저 콘솔(데이터베이스 클라이언트)을 사용하기 위해서는 의존성의 scope를 `compile`로 설정
	* 레퍼런스
		* [H2 설치, 서버 실행, 접속 방법](https://atoz-develop.tistory.com/entry/H2-Database-%EC%84%A4%EC%B9%98-%EC%84%9C%EB%B2%84-%EC%8B%A4%ED%96%89-%EC%A0%91%EC%86%8D-%EB%B0%A9%EB%B2%95)
		* [스프링 부트와 스프링 시큐리티 환경에서 H2 사용하기](https://lahuman.jabsiri.co.kr/128)
		* [Spring Boot With H2 Databse](https://www.baeldung.com/spring-boot-h2-database)
		* [스프링 부트 H2 클라이언트로 인텔리제이 사용하기](https://jojoldu.tistory.com/234)
		* [스프링 부트와 H2를 이용한 CRUD 구현](https://augustines.tistory.com/177)
2. .

##### [목차로 이동](#목차)

### 화면 그리기
1. 이미지 잘라서 사용하기
	* 이미지 태그 자체를 자르는 방법 못 찾아서 div 태그 `background` 속성 사용
	* style 태그에 빼긴 하였으나 중복 많음
2. 이미지에 링크걸기
	* 링크를 걸어야 하는 태그 고민(div/a/img)
	* 레퍼런스
		1. [a 태그 안에 블럭 넣어도 돼?](https://asource.tistory.com/19)
		2. [div 칸 전체에 링크 걸기?](https://xe1.xpressengine.com/qna/22777673)
3. HTML input 태그
	1. radio
		* [w3shcools](https://www.w3schools.com/tags/att_input_type_radio.asp)
		* [label 태그](https://www.codingfactory.net/11008)
	2. .
4. 부트스트랩 적용하기

##### [목차로 이동](#목차)

### 화면 그리기
처리란 요청 및 응답을 말한다.

1. 요청 시
	1. `HttpRequest` vs `HttpServletRequest`
		* .
		* 레퍼런스
			* [What is the difference between `org.apache.http.HttpRequest` and `javax.servlet.http.HttpServletRequest`?](https://stackoverflow.com/questions/26190641/what-is-the-difference-between-org-apache-http-httprequest-and-javax-servlet-htt)
			* [Difference between ServletRequest & HttpServletRequest](https://coderanch.com/t/621449/java/Difference-ServletRequest-HttpServletRequest)
	2. JSP와 Controller 간 매핑 매커니즘
		* JSP의 `form` 태그 내부 `input`가 Controller 메서드의 파라미터인 VO로 자동 매핑되는 원리 
2. 응답 시


##### [목차로 이동](#목차)

### 기타
1. 브라우저 캐시 지우기
	* 단축키: Ctrl-Shift-Delete
	* 레퍼런스
		* [Clear your web browser's cache, cookies, and history](https://kb.iu.edu/d/ahic)
2. 로거 설정하기
	* .
3. TDD 적용하기
4. 깃허브 연동하기

##### [목차로 이동](#목차)

##


##### [목차로 이동](#목차)