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
> * 데이터베이스: H2, Oracle(추후)
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
		* [H2: Data Types](http://www.h2database.com/html/datatypes.html)
		* [스프링 부트 실행 시, DB 데이터 삽입](https://pasudo123.tistory.com/394)
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

### 데이터 처리하기
처리란 요청 및 응답을 말한다.

1. 요청 시
	1. `HttpRequest` vs `HttpServletRequest`
		* .
		* 중복 제출 방지
			1. 뒤로 가기 방지
			2. 동일 IP 체크
		* 레퍼런스
			* [What is the difference between `org.apache.http.HttpRequest` and `javax.servlet.http.HttpServletRequest`?](https://stackoverflow.com/questions/26190641/what-is-the-difference-between-org-apache-http-httprequest-and-javax-servlet-htt)
			* [Difference between ServletRequest & HttpServletRequest](https://coderanch.com/t/621449/java/Difference-ServletRequest-HttpServletRequest)
	2. JSP와 Controller 간 매핑 매커니즘
		* 값 전달 방식
			1. `HttpServletRequest`
			2. VO[1]
				* `@ModelAttribute`는 스프링에서 Setter 자동 호출
				* JSP의 `form` 태그 내부 `input`이 Controller 메서드의 파라미터인 VO로 자동 매핑되는 원리
				* ~~JSP의 데이터를 2개 이상의 VO로 받아올 수 있는가~~ → 상속 이용 하나의 VO로?
			3. `@RequestParam`
				*Primitive type만 허용
	3. DTO와 VO
		* JSP에서 전달되는 데이터 자료형(`String`)과 DB의 컬럼형(`Number`)이 다를 경우?
2. 응답 시


- - -
1. Value Object(VO)
	* 단지 DB 테이블에 데이터를 전달(매핑)하는 클래스(객체)라고 생각하기엔 짚고 넘어가야 할 부분 존재
		* 이를 테면 ORM 프레임워크에서 테이블 매핑 객체는 엔티티라 부르지만, 자바에서는 값 객체라 부름
	* 개념
		1. 엔티티 vs 값 객체
			* 엔티티는 가변(Mutable) 객체인 반면, 값 객체는 불변(Immutable) 객체
				* 엔티티(객체)는 속성이 바뀌어도 여전히 같은 것으로 인식  
				(사람 엔티티의 정체성은 `id`로 표현되며 외에 이름, 이메일, 비밀번호는 수정 가능)
				* 반면 값 객체는 속성이 같아야 같은 것으로 인식  
				(위치 객체의 정체성은 위도와 경도로 결정되며, 같은 위도와 경도를 가진다면 두 객체는 동일)
					1. ∴ VO는 세터(Setter) 없음  
					(DTO와의 가장 큰 차이점)
					2. ∴ VO의 핵심 역할은 `equals()`와 `hashcode()`를 오버라이딩하는 것  
						```java
						@Override
						public boolean equals(Object o) {
							if (this == o) return true;
							if (o == null || getClass() != o.getClass()) return false;
							Article article = (Article) o;
							return Objects.equals(id, article.id);
						}

						@Override
						public int hashCode() {
							return Objects.hash(id);
						}
						```
		2. `Value Context` vs `Identifier Context`
			* 코드스피츠에서 [관련 부분 언급](https://github.com/nara1030/TIL/blob/master/docs/lecture_list/code_spitz/s86_oop_javascript/week_1.md)
				* 함수형 프로그래밍: 값(Value)
				* 객체지향 프로그래밍: 식별자(Identifier)
		3. 어떻게 값 객체를 식별할까?
			* 어떤 객체가 엔티티인지 값 객체인지는 애플리케이션의 상황에 따라 달라짐
			* 단, 일반적인 경우 아래와 같은 분류
				1. 값 객체: 위치, 날짜, 숫자, 금액
				2. 엔티티: 사람, 제품, 파일, 판매
		4. 기타
			* 흔히 DB와 1:1로 구현하는데, 보안상 문제가 발생할 수 있음  
			(참고: [MVC 모델에서의 DTO 객체 설계](https://www.slideshare.net/sunnykwak90/mvc-vo))
	* 레퍼런스
		* [값 객체](https://zetawiki.com/wiki/%EA%B0%92_%EA%B0%9D%EC%B2%B4)
		* [Entity, VO, DTO](https://medium.com/webeveloper/entity-vo-dto-666bc72614bb)
		* [엔티티와 값 객체의 차이](https://jaeyeolshin.github.io/2016-02-06/difference-between-entity-and-value-object/): [-](https://github.com/nara1030/test_for_sunday_study/blob/master/docs/vo_vs_entity.pdf)
		* [`java.lang.Object.hashCode` 메소드](https://johngrib.github.io/wiki/Object-hashCode/)
2. .

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
	* .
	* 레퍼런스
		* [GitHub Training & Guides](https://www.youtube.com/user/GitHubGuides/videos)
		* GitHub로 프로젝트 관리하기
			* [이슈 발급부터 코드리뷰까지](https://www.popit.kr/github%EB%A1%9C-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-part1-%EC%9D%B4%EC%8A%88-%EB%B0%9C%EA%B8%89-%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EB%A6%AC%EB%B7%B0%EA%B9%8C/)
			* [CI & Test Coverage & Wiki](https://www.popit.kr/github%EB%A1%9C-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-part2-ci-test-coverage-wiki/)
5. [인텔리제이 단축키](https://gmlwjd9405.github.io/2019/05/21/intellij-shortkey.html)

##### [목차로 이동](#목차)

##


##### [목차로 이동](#목차)