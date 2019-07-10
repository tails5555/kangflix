---
layout: post
title: "Java 면접 대비"
date: 2019-07-10 17:00:00 +09:00
image: "/assets/img/category/ct_interview.png"
category: 'interview'
tags:
- Interview
- Java
description: Java 면접 및 지식 포스트입니다.
introduction: Java 면접 및 지식 포스트입니다.
---

Java 에서 알아둬야 하는 약간의 핵심 내용을 정리했습니다.

# Contents

* Contents
{:toc}

---

# Java 8

Java 8 에서는 다음과 같은 개념들이 추가 되었습니다.

- `interface` 에 `default` 메소드 사용.
- Stream API - `Optional`, `Stream`
- Lambda Expression - Functional Programming

[맨 위로](#contents)

---

# Abstract Class

추상 클래스(Abstract Class) 는 **미완성 된 클래스** 로 이를 상속하여 완성시켜주는 개념입니다.

**공통된 부분을 추상화 시켜 자식 클래스에서 확장** 시키는 목적으로 만들었습니다.

추상 클래스는 인터페이스와 달리 `extends` 로 상속 받아 사용합니다.

Interface 처럼 IS-A 관계이지만, 차이점을 설명할 땐 목적이 다른 것을 강조하는 것이 좋습니다.

[맨 위로](#contents)

---

# Interface

인터페이스(Interface) 는 클래스의 사용 목적이 다르지만, 행위는 같을 때 사용합니다.

이는 공동으로 사용하는 메소드들을 묶어 상속 받아 사용하는(`implements`) 개념입니다.

클래스(Class) 와 달리 다중 상속이 가능합니다.

**객체의 구조는 몰라도, 메소드만 알고 있으면 어떠한 객체를 접근할 수 있게 도와줍니다.**

Java 8 에서는 디폴트 메소드가 추가되어 클래스에 구현된 메소드를 변경하지 않고, 새롭게 로직을 작성할 수 있습니다.

다만 디폴트 메소드는 인터페이스 당 1개만 작성할 수 있습니다.

또한 인터페이스 안에는 상수 필드와 추상 메소드들을 가질 수 있습니다.

[맨 위로](#contents)

---

# 다형성

다형성은 한 클래스나 메소드의 상황에 따라 다양한 방법으로 동작하는 것을 뜻합니다.

오버라이딩이 이를 잘 활용했습니다.

아래의 조건을 만족해야 다형성을 이룹니다.

**공통 부모**

공통 부모를 래퍼라고 치면 라이브를 뛰고, 음반을 내고, 방송 출연을 할 수 있습니다.

**공통 메소드 재정의**

래퍼가 라이브를 뛰는 것을 가정합니다.

더 콰이엇은 주기적으로 축제에서 후배 래퍼들을 밀어줍니다.

또 다른 예로 식케이는 라이브를 엉망으로 하여 웃음 거리를 만듭니다.

다들 라이브는 뛰지만, 리스너들의 성과에 따라 달라집니다.

**부모 타입의 변수로 호출**

처음에 랩을 잘 모르는 친구한테 '너 더 콰이엇 알아?' 라고 질문을 합니다.

그 친구는 모르겠다고 이야기를 하면, '아 그 얼굴 잘 생긴 래퍼라고...' 이러면 알아챕니다.

[맨 위로](#contents)

---

# Overloading, Overliding

오버로딩(Overloading) 은 **같은 이름의 메소드들 중 다른 매개 변수들** 을 두는 개념입니다.

오버라이딩(Overliding) 은 부모로서 **상속** 받은 메소드를 자식이 **재정의하여 사용하는 개념** 입니다.

[맨 위로](#contents)

---

# String, StringBuffer, StringBuilder

String 은 불변 데이터(Immutable) 입니다. 또한 다양한 타입의 데이터로 만들 수 있습니다.

또한 아래와 같은 문장도 연산 되어 저장됩니다. 

이는 사실 Builder 엔진을 사용하여 새로운 String 객체를 만들어 Heap 저장소에 올리기 때문에 사용 메모리 양만 많아집니다.

```java
String a = "돈가스" + " " + "냉모밀";
```

StringBuilder 는 버퍼의 크기를 늘려 유연하게 동작합니다.

그리고 긴 String 문장을 다룰 때 이를 사용하는 것이 좋습니다.

하지만 Thread-Safe 를 제공하진 않습니다. Thread 를 다루지 않아도 되면 이를 사용하면 무방합니다.

StringBuffer 는 StringBuilder 와 메소드는 똑같지만, `synchronized` 키워드 때문에 Thread-Safe 를 보장합니다.

[맨 위로](#contents)

---

# Collection

수 많은 데이터들을 저장하기 위해 자료구조를 구현한 API 입니다.

Collection 은 모든 자료구조 클래스의 최상위 객체입니다.

**List**

리스트는 순서가 있는 데이터의 모음입니다.

ArrayList 는 배열을 만들어 사용하기 때문에 조회 작업이 많으면 자주 사용합니다.

LinkedList 는 양방향 포인터를 사용하여, 삽입 및 삭제가 빈번하면 자주 사용합니다.

**Vector**

벡터는 List 와 역할이 비슷하지만, Thread-Safe 를 보장합니다.

Java 의 Stack 은 이를 상속 받아 구현되어 있어, 다중 쓰레드 환경에서 사용해도 무방합니다.

**Set**
 
순서도 없고, 중복을 허용하지 않는 데이터 모음입니다.

HashSet 는 Hash 값으로 순서를 결정하여, 이의 값을 알아채기 힘들어 순서를 알 수 없습니다. 그렇지만 시간 복잡도는 O(1) 로 매우 빠릅니다.

TreeSet 는 Tree 구조로 인덱스를 매겨 순서를 알 수 있지만 시간 복잡도는 O(log n) 입니다.

**Map**

Key 와 Value 로 이루어진 데이터 집합입니다.

Python 의 Dictionary 와 같은 맥락입니다.

또한 JSON 의 구조와 언뜻 비슷합니다.

Set 처럼 순서도 엉키지만, Key 값은 중복을 둘 수 없습니다.

HashMap 은 Hash 값으로 Key 를 설정하여, Hash Table 를 이룹니다. 이의 시간 복잡도는 O(1) 입니다.

TreeMap 은 Tree 구조의 인덱스를 매겨 정렬 순서로 조회하는 속도가 빠릅니다. 시간 복잡도는 O(log n) 입니다.

HashTable (네, 있습니다...) 는 HashMap 보다 느리지만, 동기화가 지원됩니다.

[맨 위로](#contents)

---

# Reflection

Java 에서 Reflection(리플렉션) 은 로딩이 완료된 클래스에서 다른 클래스를 동적으로 로딩(Dynamic Loading) 하여 생성자, 멤버 변수, 메소드 등을 사용할 수 있는 기법입니다.

Reflection 은 이 뿐만 아니라, 패키지 정보, 접근 지정자, 슈퍼 클래스, 어노테이션 등의 정보도 얻을 수 있습니다.

```java
@Getter
@Setter
public class Person {
    private String name;
    private int age;
    
    public Person(){

    }

    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }
}

public class Main {
    public static void main(String[] args){
        Class person = Class.forName("Person");
        Method[] methods = person.getDeclaredMethods();
        for(Method method : methods){
            System.out.println(method.toString());
        }

        Field field = person.getField("age");
        Person p = (Person) person.newInstance();
        field.set(p, 25);
        System.out.println(field.get(p)); // 25
    }
}
```

Reflection 은 다른 클래스 안에 있는 멤버 변수, 메소드 등을 얻기 위해 사용됩니다.

Reflection 를 사용하면 완성도 높은 코드를 구현할 수 있습니다.

또한 `private` 변수 및 메소드도 접근할 수 있습니다. 

다만 이는 `Field.setAccessible()` 메소드를 True 로 지정해야 합니다.

[맨 위로](#contents)

---

# Spring Framework

스프링은 Java 와 JSP 기반 Web 프레임워크 입니다. 2003년 6월에 최초 공개. 2019년 버전으로 5.1.X 까지 공개 되었습니다.

JVM (Java Virtual Machine) 위에서 작동합니다. 또한 전자정부 표준 프레임워크 기반 기술이기도 합니다.

**특징**

- POJO(Plain Old Java Object) 방식 : Java EE 플랫폼에 종속된 객체를 최대한 가볍게 제작하는 원칙.
- AOP(Aspect Oriented Programming) : 로깅, 트랜젝션, 보안 등 여러 모듈에서 공동으로 사용하는 기능을 분리할 수 있습니다.
- DI(Dependency Injection) : 프로그래밍의 의존 관계를 소스 코드 내부가 아닌 외부에서 설정하는 방식. 코드 재사용성을 높여 모듈간 결합도를 낮출 수 있음.
- IoC(Inversion of Control, 제어의 반전) : 개발자가 외부 라이브러리를 호출하는 것과 반대로, 거기서 개발자가 작성한 코드를 호출하는 것입니다.
- 생명주기 존재 : Java 객체의 생성과 소멸 등을 직접 관리함.
- 다양한 서비스 : MyBatis, JPA, Hibernate 등 ORM 라이브러리나 Apache Tiles 같은 인터페이스 등을 제공합니다.

**구조**

![Spring_Structure]({{ site.baseurl }}/assets/img/post/interview/java/spring_structure.png){: width="100%"}

Spring Framework 에서 주로 사용하는 모듈은 6가지로 이뤄집니다.

- Core : IoC, DI 등을 사용하기 위한 모듈.
- DAO : JDBC 를 사용하기 위한 모듈.
- ORM : JPA, MyBatis, Hibernate 등 ORM 들이 통합할 수 있는 기능 제공.
- AOP : Spring Framework 에서 기본으로 제공하는 AOP 패키지.
- Web : Spring Web MVC 등 Web Application 구현에 도움되는 기능 제공.

**Spring Boot**

Node.js (Express.js) 로 서버를 구축하기 위해 필요한 기능들을 라이브러리 의존성을 추가하여 작업했습니다.

그렇지만 Spring Boot 는 Spring Framework 에서 제작한 프로젝트들을 보일러 플레이트로 간단하게 배포할 수 있도록 도와줍니다.

예를 들어 데이터베이스 연동, Web App 생성, 의존성 및 AOP 관리, 테스팅 기능 등을 역할 별로 구분하여 개발자가 원하는 로직을 구현할 수 있습니다.

서버 배포를 진행하기 위해 `jar` 파일을 만들 수 있도록 제공합니다.

또한 의존성은 Maven, Gradle 를 사용하여 라이브러리의 필요성을 관리할 수 있습니다.

그렇지만 Spring Boot 가 설정을 자동화 하지만, 보안(Security) 등 일부 커스터마이징이 필요한 경우에는 따로 설정해야 하는 귀찮은 단점이 있습니다.

[맨 위로](#contents)