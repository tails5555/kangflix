---
layout: post
title: "Web 개발 및 보안 면접 대비"
date: 2019-07-04 17:00:00 +09:00
image: "/kangflix/assets/img/category/ct_interview.png"
category: 'interview'
tags:
- Web
- Interview
description: Web 개발 및 보안 면접 및 지식 포스트입니다.
introduction: Web 개발 및 보안 면접 및 지식 포스트입니다.
---

![Web_Image]({{ site.baseurl }}/assets/img/post/interview/web/web_image.jpg){: width="100%"}

Web 개발을 하면서 꼭 알아둬야 하는 개념들을 정리한 문서입니다.

수정이 필요한 사항은 아래 댓글 서비스를 사용해서 요청하시면 바로 정정 하겠습니다.

Mozilla 개발 문서나 위키백과, 나무위키를 기반으로 공부할 수 있도록 간략하게 정리하겠습니다.

# Contents

* Contents
{:toc}

---

# Web Storage

웹 브라우저가 돌아가는 HTML 환경에서 사용되는 저장소를 웹 저장소(Web Storage) 라고 합니다.

이 저장소는 서버 측에 저장하지 않고, Web 서비스를 사용하는 동안 필요한 정보를 일시적으로 축적하는 공간입니다.

Web Storage 의 종류는 크게 Local Storage, Session Storage 2가지로 나뉩니다.

이는 모든 언어를 기반으로 한 Web Framework 에서 접근할 수 있습니다.

이 개념을 JavaScript 문장으로 살펴 보겠습니다. 이들은 `window` 프로퍼티에 속합니다.

```javascript
localStorage.setItem('token', '1234567890');
sessionStorage.setItem('token', '1234567890');
```

이들의 값은 JavaScript Object 처럼 Key 와 Value 의 모음으로 구성되어 있습니다.

여기에 나오는 Value 들은 숫자, 문자열, `null`, `undefined` 등으로 저장할 수 있는데 전부 문자열로 반환됩니다.

데스크탑에는 5 ~ 10 MB 정도 저장 가능하고, 모바일은 2.5 MB 정도 저장 가능합니다. (참고로 Cookie 는 4 KB 정도 저장할 수 있습니다.)

Local Storage 는 웹 사이트를 재접속 하여도, 아니면 새로운 탭으로 실행하여도 저장된 정보를 이용할 수 있습니다. 심지어 직접 없애지 않는 이상 만료 기간이 없습니다.

Session Storage 는 세션이 종료될 때 데이터가 소멸됩니다. 또한 브라우저(IE, Chrome, Safari 등) 별로 다르게 구분합니다. 세션 종료는 브라우저의 탭을 닫는 경우, `window.close()` 함수를 실행 하는 경우 등으로 볼 수 있습니다.

자동 로그인 등 사용자에게 지속적으로 필요한 정보는 Local Storage 를 사용하는 것이 좋습니다.

그리고 일회성 로그인 정보, 접속 시각 등 한 번만 쓰고 소멸하는 데이터는 Session Storage 를 사용해야 합니다.

물론 JWT Token 을 Session Storage 에서 사용하는 방법이 있습니다. 그러나 XSS 로 뚫릴 수 있으니 토큰으로 회원 정보 관리할 때 주의해야 합니다.

[맨 위로](#contents)

---

# Cookie

쿠키는 서버 Application 에서 Web 브라우저로 전송하는 작은 데이터 조각입니다. 크기는 4 KB 입니다.

이는 이름, 값, 만료 일자, 경로 정보 등이 들어 있습니다.

쿠키는 Web 브라우저가 깔린 로컬 디스크에 저장됩니다.

즉, 클라이언트 측에 남게 되어 사용자 정보가 유출될 수 있습니다. 물론 쿠키도 만료 기간은 있지만, 길게 잡아두면 영구적으로 저장됩니다.

쿠키는 로그인 보안 기능이 필요하면 Request Header 에 자동으로 쿠키 정보를 넣어 보내줍니다.

**Cookie 의 활용**

로그인 상태를 언제든지 유지시키는 자동 로그인, 장바구니, N 일간 보지 않음 등에서 많이 쓰입니다.

참고로 JavaScript 에서는 `document.cookie` 로 접속한 사이트의 쿠키 정보를 볼 수 있지만, 대부분 Base64, SHA-256 등으로 암호화 되어 있습니다. 

그리고 부족한 쿠키 정보는 Web Storage 나 IndexedDB 를 사용하여 저장합니다. 

**Cookie를 더 쓰는 이유**

Session 은 서버의 자원을 추가로 사용해야 합니다.

클라이언트 측에서 서버로 요청하는 횟수가 많아지면, 서버의 메모리가 감당할 수 없는 경우가 발생합니다.

그러면 서버 측의 속도가 현저히 떨어지게 되어 Web 서비스의 효율성이 떨어집니다.

반대로 Cookie 는 보안이 떨어지지만, Session 처럼 여러 다른 요청들이 쌓이지 않고 단일 정보만 저장되기 때문에 속도 면에서 빠릅니다.

[맨 위로](#contents)

---

# Session

세션은 일정 시간동안 같은 브라우저로 들어오는 요청들을 하나의 상태로 유지시키는 기술입니다.

세션은 서버 측에서 접속한 클라이언트의 고유 ID 를 저장합니다. 이 아이디는 서버에서 부여합니다.

이는 네트워크에서 반영구적이고, 둘 이상의 컴퓨터를 만나야 공간이 생깁니다. 즉, 브라우저가 종료 되면 자동으로 만료 됩니다.

세션은 쿠키와 반대로, 서버 측에 고유 ID 만 저장하기 때문에 보안성은 좋습니다.

하지만 세션은 서버 측으로 연결하여 처리해야 하기 때문에 속도 면에서 떨어집니다.

로그인 정보 유지 등에서 많이 사용되고, Session 정보는 Key-Value No-SQL 인 Redis 를 사용하여 축적합니다.

**Cookie 와 Session 의 내용을 잘 정리한 블로그**

https://jeong-pro.tistory.com/80

[맨 위로](#contents)

---

# JSON (JavaScript Object Notation)

```json
{
    "name" : "강사람",
    "age" : 26,
    "hobby" : ["축구", "배구"]
}
```

```javascript
const person = {
    name: '강사람',
    age: 26,
    hobby: ['축구', '배구']
};

JSON.stringify(person); // JavaScript 객체를 JSON 으로 변환합니다.
JSON.parse('{ "name" : "강사람" }'); // JSON 문장을 JavaScript 객체로 변환합니다.
```

서버에서 클라이언트로 데이터를 보낼 때 사용되는 양식입니다. 클라이언트의 언어 종류에 상관 없이 데이터를 안전하게 사용할 수 있습니다.

JSON 은 JavaScript 객체 문법처럼 Key 와 Value 로 구성되어 있습니다.

XML 언어는 가독성이 떨어지고, 용량을 많아서 JSON 을 많이 쓰는 추세입니다.

JSON 의 공식 인터넷 미디어 타입은 `application/json` 입니다. 어느 프로그래밍 언어이든 활용할 수 있습니다.

MongoDB 와 같은 Document NoSQL 는 표준 표기법으로 취급하고 있어 Node.js 는 이를 더욱 연동합니다.

하지만 JavaScript 객체 문법관 달리 문법 오류에 민감합니다. 또한 주석을 따로 추가가 불가능하고, Property 는 무조건 더블 쿼터("") 로 감싸줘야 합니다.

[맨 위로](#contents)

---

# Serialization (직렬화)

직렬화(Serialization) 는 프로그램 시스템 내부에서 사용되는 객체를 외부의 시스템에서도 사용할 수 있도록 Byte 형태로 변환하는 것입니다.

역직렬화(Deserialization) 는 Byte 데이터를 다시 프로그래밍에서 사용하는 객체로 변환하는 것입니다.

Java 에서 객체를 자동으로 직렬화할 수 있는 방법은 아래와 같습니다.

```java
import java.io.Serializable;

public class Person implements Serializable {
    final static long serialVersionID = 1L; // *

    private int id;
    private String name;
    private int age;

    public Person(int id, String name, int age){
        this.id = id;
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString(){
        return String.format("Person {id:%d, name:%s, age:%d}", this.id, this.name, this.age);
    }
}
```

```java
import java.io.ByteArrayOutputStream;
import java.io.ObjectOutputStream;
import java.io.ByteArrayInputStream;
import java.io.ObjectInputStream;

public class Example {
    public static void main(String[] args) {
        Person person = new Person(1, "강사람", 26);

        // Serialization 예제
        byte[] serializedMember;
        try (ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
            try (ObjectOutputStream oos = new ObjectOutputStream(baos)) {
                oos.writeObject(person);
                serializedMember = baos.toByteArray();
            }
        }
        System.out.println(Base64.getEncoder().encodeToString(serializedMember));

        // Deserialization 예제
        String base64Member = "~~~~~~~~~~~";
        byte[] serializedMember = Base64.getDecoder().decode(base64Member);
        try (ByteArrayInputStream bais = new ByteArrayInputStream(serializedMember)) {
            try (ObjectInputStream ois = new ObjectInputStream(bais)) {
                Object objectMember = ois.readObject();
                Person person = (Person) objectMember;
                System.out.println(person);
            }
        }
    }
}
```

Java 직렬화는 `ObjectOutputStream` 을 사용하여 객체 데이터를 `byte` 배열로 변환합니다.

Spring Framework 에서 Controller 단위 요청 URL 에 따라 객체를 JSON 으로 자동 반환하는 것을 볼 수 있습니다.

이는 Java 의 객체를 Jackson 혹은 GSON 라이브러리 내부에서 JSON 으로 자동 반환 시켜주기 때문입니다.

`byte` 배열 뿐만 아니라 JSON, CSV 등의 문자열 포맷으로 변경시켜주는 과정도 직렬화에 속합니다.

그러나 역직렬화를 하기 위해선 (*) 문장처럼 `serialVersionID` 의 값을 Java Application 끼리 같은 값으로 설정되어 있어야 합니다.

이의 값은 또한 MyBatis 에서 캐시 기능을 사용할 때 필요한 변수이기도 합니다. 

MyBatis 캐시 안에서 Java 객체 데이터로 저장하기 위해 역직렬화 과정이 필요할 것으로 추측됩니다.

**참고 링크**

http://woowabros.github.io/experience/2017/10/17/java-serialize.html

https://nesoy.github.io/articles/2018-04/Java-Serialize

[맨 위로](#contents)

---

# OAuth

인터넷 서비스는 SaaS(Software as a Service) 형태로 제공하는 추세로, 사용자가 일부 필요한 것만 사용할 수 있어야 합니다.

그 중 사용자 인증 기능을 Web 서비스의 요구 뿐만 아니라 다른 수단으로 처리할 필요가 생깁니다.

OAuth 는 인터넷 서비스를 사용하는 사용자들이 자신의 계정 정보를 제공하지 않고 다른 Web 서비스의 회원 권한을 가질 수 있는 수단입니다.

이를 제공하는 서비스는 네이버, 카카오, 구글, 페이스북, 트위터 등이 있습니다.

**OAuth 1.0 to 2.0**

OAuth 1.0 은 2007년부터 발표되었으나 초반에는 아이디와 패스워드를 API 에 전달하여 사용해서 보안에 취약했습니다.

그리고 이 때는 OAuth 를 사용하는 범위가 적었으며 프로토콜을 비공식적으로 사용해 안전성이 떨어졌습니다.

그래서 OAuth 2.0 에서는 다양한 Application 에서도 사용하게 지원하였고, 토큰에 Life-Time 을 추가하였습니다.

그리고 2010년부터 OAuth 의 토큰들이 공식적인 프로토콜로 인정되어 사용하는 빈도가 더욱 늘어납니다.

**일반 로그인 vs OAuth 로그인**

이를 군대에 있는 위병소로 설명하겠습니다. 군대 간부들의 출입이 일반 로그인, 면회자의 출입이 OAuth 로그인과 유사합니다.

위병 근무자들은 군대 간부들의 차 넘버와 차종을 이미 숙지하여 바로 건널목 스틱을 올려줍니다.

회원 아이디와 비밀번호의 데이터가 군대 간부들의 차와 연락처 정보 데이터와 같은 맥락입니다.

그러나 면회 온 병사 부모님들은 위병 근무자가 아들 정보로 신원 확인을 거치고 나서야 출입증을 받고 들어갈 수 있습니다.

웹 서비스를 사용하기 위한 인증 서비스 주체가 면회용 출입증과 똑같은 맥락입니다.

**OAuth 인증 과정**

OAuth 의 인증 과정은 아래와 같습니다.

1. 타 서비스에게 Request Token 요청과 발급
2. 인증 서비스 사용자 인증 페이지 호출
3. 인증 서비스 사용자 로그인 완료
4. 인증 서비스 사용자 권한 요청 및 수락
5. 타 서비스 Access Token 발급
6. 타 서비스 Access Token 을 사용해 서비스 정보 요청

Request Token 은 인증 서비스의 회원이 타 서비스 Service Provider 에게 인증 서비스 정보로 신원 확인을 요청하기 위한 데이터입니다.

Access Token 은 인증 서비스의 허가 확인 이후, 타 서비스에서 자신의 신분임을 인증하는 토큰입니다. 이를 사용하여 타 서비스의 회원임을 인증, 인가할 수 있습니다.

이 토큰들은 대부분 JWT(JSON Web Token) 를 사용하여 암호화 시켜 사용합니다.

**참조 링크**

이외의 정보는 아래 포스트를 참고하시면 더욱 도움 됩니다.

https://d2.naver.com/helloworld/24942

[맨 위로](#contents)

---

# AJAX(Asynchronous JavaScript & XML)

AJAX 는 비동기 Web Application 을 제작하기 위해 사용됩니다.

XML 뿐만 아니라 JSON 이나 일반 텍스트도 사용할 수 있습니다.

**AJAX 이용 목적**

Web 브라우저에서 어떤 정보를 요청하게 되면 서버에선 페이지 전체를 전달할 수 밖에 없습니다.

서버로부터 받은 HTML 문장을 일일히 렌더링하는 것은 클라이언트, 서버 둘 다 불편했습니다.

그래서 일부 페이지에 `iframe`, `template` 태그 안에 필요한 정보를 REST API 서버에게 요청하여 가공할 필요가 있었습니다.

요청하는 함수가 AJAX 이지, 데이터를 가져와 표출하는 것을 서버 사이드 렌더링이라고 합니다.

**AJAX 사용 방법**

**`XMLHttpRequest`**

순수 자바스크립트 (Vanilla JS) 를 사용하여 요청할 수 있습니다.

입력, 출력, 상태를 모두 하나의 객체로 관리해야 하는 단점이 있어 Promise 기반 비동기 프로그래밍 방식에는 적합하지 않습니다.

```js
var request = new XMLHttpRequest();

request.open("GET", 'http://127.0.0.1:8080/api/person');
request.onreadystatechange = function() {
    if(request.status === 200){
        document.getElementById('app').innerHTML = request.responseText;
    }
}
```

**jQuery AJAX**

XHL 의 어려운 문법을 보완 시키는 것이 jQuery AJAX 입니다.

또한 Promise 기반 비동기 프로그래밍 방법도 제공합니다.

하지만 이를 사용하기 위해 굳이 jQuery 를 불러오면 용량 낭비로 요청 효율성을 떨어트립니다.

**`fetch()`**

XHL 로 객체 관리하는 단점을 버리고, Promise 기반 비동기 프로그래밍으로 관심 분야를 격리 시켜주는 AJAX 가 Fetch API 입니다.

이는 JavaScript ES6 부터 제공합니다. 또한 CORS, HTTP Origin Header 까지 검사하여 보안성을 더욱 강화했습니다.

그러나 IE 나 Edge 에서 호환하지 않는 단점이 있습니다.

또한 서버에서 받아온 데이터를 일일히 가공해서 결과를 얻어야 하는 단점도 있습니다.

**Axios**

`fetch()` 함수에서 받아온 데이터를 일일히 가공하는 것과 IE 에서 못 사용하는 단점을 보완한 라이브러리 입니다.

AJAX 요청에 필요한 Method(GET, POST, PUT, DELETE) 별 간략 메소드 뿐만 아니라 여러 요청들을 한 번에 불러오는 병렬 호출 기능도 추가되었습니다.

모두 받은 결과를 JSON 객체로 자동 변환 시켜줘서 입문하기 쉬운 라이브러리입니다.

또한 TypeScript 에서도 사용할 수 있습니다.

https://github.com/axios/axios

[맨 위로](#contents)

---

# SQL Injection

말 그대로 입출력이 이뤄지는 응용 프로그램에서 보안 상 허점을 의도적으로 사용해 SQL 문을 실행하게 하여 DB 를 비정상적으로 조작하는 공격 방법입니다.

이는 Web Application 을 사례로 들어보겠습니다. 

예를 들어 ORDER BY 쿼리를 선택해야 하면, XSS 방법으로 SELECT 폼에 SQL 문장을 입력합니다.

```sql
SELECT * FROM PEOPLE ORDER BY ""
``` 

```html
<select value="id" name="ob">
    <option value="name">이름</option>
    <option value="age">나이</option>
    <option value="address">주소</option>
    <option value="id desc; DELETE FROM PEOPLE">메롱</option>
</select>
```

`option` 태그 중에 내용이 메롱인 걸 선택해서 Submit 하면 PEOPLE 테이블에 있는 모든 데이터가 전부 삭제 됩니다.

`ORDER BY` 문장만 안전한 것이 아닙니다. 

예를 들어 사용자 ID 와 비밀번호를 입력하는 경우를 살펴보면 비밀번호를 모르더라도 `true` 값을 넘겨 SUBMIT 할 수 있습니다.

참고로 비밀번호 데이터를 데이터베이스에 그대로 저장하면 견찬서 행입니다. 최소한 SHA-256 으로 암호화를 해야 합니다.

```sql
SELECT * FROM PEOPLE WHERE id="" AND password=""
``` 

```html
<form>
    <input type="text" name="id" value="admin_id" />
    <input type="password" name="password" value=" ' OR '1' = '1' " />
    <button type="submit">로그인</button>
</form>
```

이를 예방하기 위해 SQL 쿼리 문장에서는 Prepared Statement (? 에 데이터 넣는 거) 로 처리해야 합니다.

또한 MyBatis 를 사용하면 ORDER BY 문장 같은 경우는 Dynamic SQL 를 사용하는 것이 좋습니다.

[맨 위로](#contents)

---

# XSS(Cross-Site Scripting)

XSS 는 사이트 간 스크립팅 입니다. Web 에서 기초적인 취약점을 공격하는 방법입니다.

간단하게 설명하면, 사용자가 악의적으로 공격하기 위한 사이트에 스크립트를 넣는 기법입니다.

공격에 성공하면 이 사이트에 접속한 다른 사용자가 이를 실행하게 되어 Cookie 나 Session 토큰 등의 민감한 정보를 뺏어갑니다.

이는 주로 자바스크립트를 사용해서 공격합니다. 하지만 많은 사이트들이 XSS 의 방어 조치를 해 두지 않았습니다.

XSS 를 방어하는 방법은 특정 라이브러리를 사용하는 방법과 Validation 으로 데이터 입출력을 확인하는 방법이 있습니다.

[맨 위로](#contents)

---

# CSRF(Cross-Site Request Forgery)

이는 사이트 간 요청 위조로 어떤 사용자든 상관 없이 공격자가 CRUD 행위를 특정 사이트에 요청하는 행위입니다.

XSS 는 특정 사이트를 신용하는 점을 노렸지만, CSRF 는 신용을 한 상태에서 뒷통수를 치는 것입니다.

`src` 프로퍼티가 있는 `img` 태그에 요청 URL 를 입력하여 공격합니다. 

`img` 태그는 GET 요청을 통해 이미지 데이터를 가져오지만, 특정 웹 페이지에서 form 태그에 요구하는 값을 위조하여 CRUD 를 요청할 수 있습니다.

예를 들어 사용자 A 가 로그인을 하고, 한 이미지 태그를 일단 조회합니다.

이 사람이 `http://abc.com/post_update?id=1&title=타이틀&context=내용` 이란 URL 를 `src` 에 넣습니다.

다른 접속자가 이 이미지를 조회하는 것만으로도 1번 게시글의 제목이 '타이틀', 내용이 '내용' 으로 바뀝니다.

이를 방지하기 위해 Servlet 기반 페이지라도, GET/POST 방식을 잘 구분해야 합니다.

그리고 Session ID 를 통해 CSRF Token 을 발급 받아야 합니다. 이는 Spring Framework 나 django Framework 에선 자동으로 구현되어 있습니다.

다만 SPA (Angular, React, Vue) 로 Web App 을 제작하면 Server 측에서 막아야 합니다.

Spring Framework 에서는 Spring Security 의 `csrf().disable()` 로 막을 수 있습니다.

[맨 위로](#contents)

---

# CORS(Cross-Origin Resource Sharing)

접속한 클라이언트에서 서버에게 데이터 전송을 활성화하는 Cross-Domain 접근 제어권을 부여하는 것입니다.

**Cross-Domain**

Cross-Domain 은 JavaScript 의 보안 정책 중 하나인 Same-Origin Policy 를 만족해야 합니다.

이는 스크립트 실행되는 페이지와 비동기 호출시 주소의 프로토콜, 호스트, 포트가 같아야 하는 전제 조건입니다.

**배경**

서버에 접근한 URL 이 다른데, 다른 도메인으로 자원(Resource) 를 가져오기 위해 Cross-Site HTTP Request 가 필요합니다.

멀티미디어 자료나 스크립트 태그, 링크 등을 다른 도메인에서 가져오면 일단 작동은 합니다.

하지만 Script 태그 안에서 생성된 Cross-Site Http Request 는 Same-Origin Policy 를 적용 받기 때문에 다른 도메인의 자원을 가져오는 것이 불가능하게 됩니다.

사실 보안상의 이유로 초반의 XMLHttpRequest 는 Same-Origin 정책을 따라 다른 도메인에선 자원을 접근하지 못 하게 막았습니다.

그렇지만 클라이언트 사이드 기반 Web 에서 AJAX 요청 등을 다루기 위해 다른 도메인에서 접근 가능하도록 CORS 개념이 생긴 것입니다.

**종류**

CORS 요청의 종류는 크게 4 가지로 나뉩니다.

- Simple Request : 서버에 1번 요청하고, 1번 응답 받는 방식. GET, POST, HEAD 방식 중에서만 적용 가능. Header 는 그대로 사용.
- Preflight Request : 다른 메소드 요청 가능. Header 의 내용 변경 가능. 예비 요청과 본 요청으로 나뉘어 전송.
- Credential Request : HTTP Cookie, Authentication 정보를 인식하는 요청. Access-Control-Allow-Origin 헤더 값은 구체적인 도메인이 와야 함.
- Non-Credential Request : `xhr.withCredentials` 값이 `false` 이면 Non-Credential 요청임. 이 값이 `true` 이면 Credential Request 에 해당.

**과정**

- CORS 요청 시, OPTIONS 주소로 서버가 CORS 를 허가하는지 물어봅니다.
- Access-Control-Request-Method 로 보내는 메소드 방식을 확인합니다.
- Access-Control-Request-Headers 로 보내는 헤더를 알립니다.
- Allow 항목들은 Request 에 대응하여 서버가 허용하는 메소드와 Header 를 응답하는데 사용합니다.
- Request 랑 Allow 랑 일치하면 CORS 요청이 이뤄집니다.

[맨 위로](#contents)

---

# REST API

REST 는 REpresentational State Transfer 의 약자입니다.

이는 Web 의 장점을 최대한 활용 가능한 아키텍쳐입니다. 모든 디바이스에서 통신할 수 있어야 하는 전제 조건이 붙습니다.

REST 는 HTML 의 Hyper Media API 의 기본을 충실히 지킵니다.

이는 웹 기술과 HTTP 프로토콜을 그대로 활용하고, Client 와 Server 사이의 통신 방식을 규정할 수 있습니다.

**구성 요소**

REST API 은 크게 Resource URI, Method, Message 3 요소로 구성 되어 있습니다.

또한 리소스 지향 아키텍쳐 스타일이기 때문에 모든 것을 리소스, 명사로 표현하는 것이 원칙입니다.

**특징**

- 무상태성(Stateless) : 상태 정보를 저장하지 않고, 들어오는 요청만 메시지로 처리함.
- 캐싱(Cacheable) : HTTP 웹 표준에서 제공하는 Cache 기능 사용 가능.
- 계층화 : 클라이언트가 서버나 미들 서버 등 통신 주체를 정확히 알 수 없음.
- 자체 표현 구조 : REST API 메시지만 보고도 이해하기 쉬운 구조로 되어 있음.
- 클라이언트-서버 구조 : 클라이언트는 사용자 인증 등을 직접 관리하고, 서버는 비즈니스 로직만 처리하여 이들의 의존성을 최소화합니다.

**장점**

- 여러 서비스 디자인에서 생기는 문제를 최소화합니다.
- HTTP 프로토콜의 표준을 최대한 활용하여 추가적인 장점을 함께 가져갈 수 있게 해 줍니다.

**단점**

- 테스트 할 일이 많아지면 URL 보다 Header 를 건들어야 하는 일이 많아집니다.
- 구형 브라우저(IE) 에서 지원해주지 못 하는 부분이 존재합니다. (ex) PUT, DELETE 메소드 처리.

**RESTful**

RESTful 는 REST 라는 아키텍쳐를 구현한 웹 서비르를 나타나는 용어입니다.

RESTful 는 REST 답게 사용하는 뇌피셜일 뿐입니다.

RESTful API 는 이해하기 쉬윈 REST API 를 만들고, 일관적인 컨벤션을 통한 API 이해도 및 호환성을 높여주는 것이 원칙입니다.

RESTful API 는 퍼포먼스(성능) 와는 전혀 무관합니다. 

쉽게 생각하면 돈가스 라는 음식이 있는데, 음식 호칭을 정하기 위해 고급스런 이름으로 포크 커틀릿으로 부르거나, 속칭으로 스윙스로 부르는 차이일 뿐입니다.

다만, RESTful API 를 지키기 위해 최소한 아래와 같은 2가지 원칙은 지켜야 합니다.

- CRUD 기능을 모두 POST 로 처리하면 안 됨.
- Route 에 Resource, PK 이외의 정보가 들어가면 안 됨. (`/person/updateAge` => `/person/:id [PUT]` )

[맨 위로](#contents)

---

# SEO(Search Engine Optimization)

SEO 는 검색 엔진 최적화 란 의미입니다.

웹 페이지 검색 엔진이 (예를 들어 구X, 네X버, 다X 등) 자료를 수집하고 순위를 매겨 페이지를 구성해 상위에 나오는 작업입니다.

웹 페이지와 관련된 검색한 결과가 상위에 나오면 방문 트래픽이 늘어납니다. 이 방법이 곧 인터넷 마케팅 방법 중 하나라 볼 수 있습니다.

최근에는 사용자의 신뢰를 잃어 컨텐츠의 신뢰도를 확인할 수 있는 지표(ex. 인용 횟수 등) 를 추가하여 정렬하고 있습니다.

**Server / Client Side Rendering 의 영향**

Server Side Rendering 은 초기 로딩 속도가 빠르기 때문에 SEO 가 필요한 정보를 빠르게 크롤링할 수 있습니다.

그렇지만 View 를 변경하는 부분에선 서버 요청 비용이 증가하여 SEO 와는 상관이 없습니다.

하지만 Client Side Rendering 은 동적으로 변하는 UI 때문에 SEO 측은 오히려 안 좋은 영향이 있습니다.

최근에 구X 엔진은 SPA (ReactJS, VueJS 등으로 구현한 Web) 를 분석하기 위한 엔진이 준비되어 있지만, 네X버나 다X 은 분석을 진행하지 않아 Server Side Rendering 기반으로 따로 준비해야 합니다.

그래서 최근에는 Client Side Rendering 뿐만 아니라, Server Side Rendering 을 같이 사용할 수 있는 라이브러리를 겸용하는 편입니다. (React - Next.js, Vue - Nuxt.js 등)

[맨 위로](#contents)

---

# Server Side Rendering

![Server_Side_Rendering]({{ site.baseurl }}/assets/img/post/interview/web/server_side_rendering.png)

렌더링(Rendering) 은 Web 페이지에 접속할 때, 페이지를 화면에 그리는 과정입니다.

사용자가 브라우저에서 요청을 하면, 서버에 새로운 페이지를 요청하는 방식입니다.

그러니까, 웹 페이지에 접근하면 UI(View), 데이터 등 서버에서 일일이 처리하는 것입니다.

서버 측에선 Model Session 에 따라 HTML, View 를 응답합니다.

물론 서버에게 View 까지 요청하기 때문에 첫 로딩은 짧은 편입니다. 

(나머지 필요한 파일들은 렌더링을 하면서 동적으로 불러오면 되기 때문에 Case By Case 입니다.)

이러한 방식은 모바일 웹에서 데이터를 많이 잡아 먹는 단점이 생깁니다.

[맨 위로](#contents)

---

# Client Side Rendering

![Client_Side_Rendering]({{ site.baseurl }}/assets/img/post/interview/web/client_side_rendering.png)

SPA(Single Page Application) 기반으로 렌더링하는 기법입니다.

이는 페이지 전체를 요청하지 않고, 렌더링에 필요한 컴포넌트 UI 등 데이터만 변경하여 사용하는 단일 페이지 Application 입니다.

이러한 패러다임은 View 는 오로지 클라이언트에서만 담당하고, 서버는 JSON 등 데이터만 주고 받습니다.

Client Side Rendering 은 서버에서 View 를 렌더링하지 않고, 정적 페이지 URL 로 요청하여 JS, CSS, HTML 등 필요한 파일을 다운 받아 브라우저에게 보여줍니다.

그래서 첫 로딩은 파일을 불러오기 때문에 Server Side Rendering 보다 오래 걸리는 편입니다.

[맨 위로](#contents)

---