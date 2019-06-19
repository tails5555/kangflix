---
layout: post
title: "JavaScript 면접 대비"
date: 2019-06-19 18:00:00
image: "/kangflix/assets/img/category/ct_interview.png"
category: 'interview'
tags:
- JavaScript
- Interview
description: JavaScript 면접 및 지식 포스트입니다.
introduction: JavaScript 면접 및 지식 포스트입니다.
---

![JavaScript]({{ site.baseurl }}/assets/img/post/interview/javascript.png){: width="100%"}

아래의 포스트 링크를 주로 참고하였습니다.

너무 기초적인 지식보다 조금 까다로운 개념들과 단골 질문들을 주로 다루겠습니다.

수정이 필요한 사항은 아래 댓글 서비스를 사용해서 요청하시면 바로 정정 하겠습니다.

참고로 AJAX 나 JSON 등 JavaScript 와 관련은 있지만, 문법과 거리가 먼 자료는 **Web 개념 및 보안** 자료에 정리하겠습니다.

https://www.edureka.co/blog/interview-questions/javascript-interview-questions/

https://www.guru99.com/javascript-interview-questions-answers.html

https://h5bp.org/Front-end-Developer-Interview-Questions/translations/korean/

# Contents

* Contents
{:toc}

---

# JavaScript 정의

JavaScript 는 웹 브라우저 안에서 사용하는 스크립트 언어입니다.

이는 웹 페이지에 있는 DOM 을 효율적으로 구성하기 위해 제작되었습니다.

객체 지향 프로그래밍 언어이지만, 프로토타입(Prototype) 기반으로 이뤄집니다.

HTML, CSS 와 함께 웹 페이지를 구성합니다.

또한 Python 처럼 소스 코드를 바로 실행할 수 있는 인터프리터(Interpreter) 언어 입니다.

JavaScript 의 표준 문법은 ECMAScript 를 따릅니다.

[맨 위로](#contents)

---

# JavaScript 특징

**동적 형변환과 타입의 제한이 없습니다.**

```javascript
var a = 10;
var b = '20';
console.log(b - a); // 10
```

JavaScript 는 타입의 제한이 없고, 심지어 값에 따라 자동 형변환을 시킨 값으로 작동합니다.

JavaScript 는 인터프리터 언어라서 결과 값 추출을 우선으로 두고 있습니다.

**프로토타입(Prototype) 기반 객체 지향을 제공합니다.**

```javascript
var person = {
    name: '강사람',
    age: 26
};

person['address'] = '용인시 기흥구';

console.log(person); // { name: '강사람', age: 26, address: '용인시 기흥구' }
```

JavaScript 에서 객체를 생성하면 클래스를 사용하지 않습니다.

대신에 그 특성을 복제하여 새로운 객체를 생성합니다.

프로토타입 기반에서 사용하는 객체는 Property 와 Value 를 자유롭게 추가 및 삭제할 수 있습니다.

**함수형 프로그래밍을 같이 사용할 수 있습니다.**

```javascript
let arr = [10, 20, 30];
let twice = arr.map(x => x * 2); // [20, 40, 60]
```

JavaScript 는 객체 지향 프로그래밍 뿐만 아니라 함수형 프로그래밍을 같이 병용할 수 있습니다.

참고로 JavaScript 에서 함수는 일급 객체(1st Class Object) 이기도 합니다.

이를 활용하기 위해 고차 함수 개념을 사용해야 합니다.

**다양한 Application 환경에서 사용할 수 있습니다.**

JavaScript 는 웹 브라우저에서 `script` 태그의 소스 코드를 컴파일 하기 위해 브라우저 만의 엔진이 상주하고 있습니다.

대표적으로 Chrome 의 V8 Engine, Safari 의 Webkit 등이 있습니다.

또한 JavaScript 를 기반으로 서버 어플리케이션을 구성하는 경우도 있습니다. (Node.js, Express, Koa 등)

최근에는 모바일 Application 을 제작할 때 많이 사용되지만, 버전 업데이트가 자주 있어 입문하기 어려운 단점이 있습니다. (React Native, Flutter 등)

각 Application 환경에서 사용하는 JavaScript 의 초기 변수의 구성 요소가 달라집니다.

**대부분 Single Thread 기반으로 작동합니다.**

JavaScript 는 웹 브라우저에선 단일 Thread 만 사용할 수 있습니다.

물론 Multi Thread 를 사용하는 방법이 있긴 합니다. (Web Workers 사용)

Single Thread 환경에서는 하나의 작업이 길어져도, 이를 마친 이후에 다음 작업을 진행할 수 밖에 없습니다.

그러나 Task Queue 와 Event Loop 를 통하여 Non Blocking 처리를 하여 여러 작업들이 병행(Concurrency) 할 순 있습니다.

이러한 이유로 JavaScript 도 Multi Thread 를 제공하는 것처럼 보이지만, 사실은 그렇지 않습니다.

이에 대한 상세한 내용은 아래 포스트를 읽어보시면 더욱 도움됩니다.

https://meetup.toast.com/posts/89

[맨 위로](#contents)

---

# JavaScript 장단점

**장점**

- 인터프리터로 소스 코드의 추론 속도가 빨라집니다.
- JIT 컴파일을 제공하여 즉석 컴파일로 결과물을 쉽게 얻을 수 있습니다.
- 웹 브라우저의 개발자 도구를 사용하여 디버깅을 쉽게 확인할 수 있습니다.
- 이를 이용한 프레임워크와 라이브러리가 많습니다.
- 객체 지향 프로그래밍 중에서 입문하기 쉬운 편에 속합니다.
- 객체는 JSON 으로 작성할 수 있어 다양한 플랫폼 언어에서 적용하기 쉽습니다.

**단점**

- 개선 사항이 많아서 적응하기 힘듭니다.
- 타입의 정형성이 떨어져서 유지보수가 힘듭니다.
- 웹, 서버, 모바일 등 다른 개발 환경에서 확장성이 용이합니다.
- 브라우저에 따라 제공하지 않는 API 를 확인해야 합니다.
- 개발자 도구에서 소스 코드가 보여져서 XSS 방어에 취약합니다. 

[맨 위로](#contents)

---

# Scope

Scope 를 변수나 함수가 사용되는 범위라고 설명하면 틀린 답은 아니지만 좋은 설명은 아닙니다.

쉽게 설명하면 팝송을 예로 듭니다. 노래의 제목을 모르는데 계속 들어보면 언뜻 들은 적이 있을 것입니다.

그러면 다음에 이 노래를 검색하면 제목과 발매 년도를 보면 깜짝 놀라게 됩니다.

프로그래밍에서 사용하는 변수의 값과 함수의 로직은 메모리 주소를 통하여 가리킵니다.

변수가 가리키는 메모리 주소를 사용하는 로직 범위를 찾은 후, 변수의 이름과 사용 범위를 찾는 원리를 Scope 라고 합니다.

Scope 의 종류는 크게 Global 스코프, Local 스코프 로 나뉩니다.

```javascript
var _c = 20; // (1)
function add(_a, _b) {
    var _c = _a + _b; // (2)
    return _c;
}

console.log(add(20, 30)); // 50 (R1)
console.log(_c); // 20 (R2)

var _c = 30;
console.log(_c); // 30 (R3)
```

**Global & Local Scope**

위 문장에서 (1) 과 (2) 의 Scope 는 다릅니다.

(1) 은 전역 문장에서 사용되어 Global Scope 에 속합니다.

그러나 `add` 함수를 실행하면, (2) 에서 사용되는 `_c` 의 변수는 지역 문장에서 사용되어 Local Scope 에 속합니다.

`_c` 의 값을 (R1) 문장에서 반환하면 함수가 종료되면서 Local Scope 가 사라집니다.

(R2) 문장에서는 가장 가까이 있는 Global Scope 의 `_c` 변수를 참고하게 되어 처음에 초기화 한 20 을 출력합니다.

**변수 중복 선언**

참고로 `var` 타입을 사용하면 변수 이름을 중복으로 사용할 수 있어 (R3) 문장 처럼 중복 선언할 수 있습니다.

그러나 Scope 를 찾는데 혼란을 줄 수 있어 Global Scope 에서 객체로 데이터를 묶는 것이 좋습니다. 

**Lexical Scope**

```javascript
var _x = 10;

function foo() {
    var _x = 100;
    var baz = function () {
        console.log(_x);
    }
    baz(); // 100 (R6)
    bar();
}

function bar() {
    console.log(_x);
}

bar(); // 10 (R4)
foo(); // 10 (R5)
```

Scope 는 위에서 언급했지만, 사용하는 변수의 사용 범위를 찾는 과정입니다.

(R4) 문장에서 `_x` 가 사용되는 가까운 Scope 가 Global Scope 이기 때문에 출력 값은 10 이 나옵니다.

그러나 (R5) 문장을 살펴보면, `foo` 함수에서 `_x` 변수의 값을 100 으로 바꿔도 `bar` 함수의 결과는 10 이 나옵니다.

하지만 (R6) 문장에선 `foo` 함수에 있는 `_x` 의 변수를 참조하여 실행 결과는 100 이 나옵니다.

이처럼 함수 안에 없는 변수를 탐색하기 위해 문서적인 측면에서 Scope 를 판단하는 것을 Lexical Scope 라 합니다.

[맨 위로](#contents)

---

# var, const, let

JavaScript 에서 변수를 선언하는 방법입니다.

이 셋의 차이는 ES6 문법에 새로 추가된 부분이 있으니 JavaScript 개발자로 가게 되면 읽어두세요.

**`var`**

`var` 는 ES6 이전 문법입니다.

이는 Function-Scoped 로, 함수 안에서 변수를 선언하면, 그 변수는 선언한 함수 안에서만 접근 할 수 있습니다.

예를 들어 `for` 문을 살펴 보겠습니다.

```javascript
// Case 01. for 문 With Hoisting
for(var k = 0; k < 10; k++){
    console.log(k); // 0 ~ 9
}
console.log(k); // 10

// Case 02. for 문 With Function
function foo() {
    for(var l = 0; l < 10; l++){
        console.log(k, 'k'); // 10 k (2 - (1))
        console.log(l); // 0 ~ 9
    }
}

foo();
console.log(l); // 오류 걸립니다. (2 - (2))
```

Case 1 에서는 `for` 문 안에서 0부터 9까지 돌리고, 10까지 돌리면 멈춥니다.

그러나 마지막 출력 문장에서는 다행이 10이 나옵니다.

이는 `k` 변수가 `var` 로 인해 Hoisting 되었기 때문입니다.

Case 2 - (1) 에서는 `k` 변수도 `foo()` 함수에서 사용할 수 있습니다.

`var` 는 외부에서 함수를 호출하면, 외부에 있는 변수를 사용할 수 있기 때문입니다.

그러나 Case 2 - (2) 에서는 `foo()` 함수가 끝나면, `l` 의 변수 사용이 불가능합니다.

`l` 변수는 함수 `foo()` 에서 선언 되어, Function-Scoped 때문에 외부에서 사용 불가능하기 때문입니다.

**let, const**

```javascript
var a = '123';
var a = '234'; // var 로 중복 선언이 가능하다!

b = '345'; // Hoisting 때문에 참조 에러가 안 납니다.
var b;
```

`var` 의 단점은 Function-Scoped Hoisting 이 일어나서, 변수를 중복 선언해도, 아무 키워드 없이 값을 지정할 수 있습니다.

이를 막을 수 있는 방법은 맨 위에 `'use strict'` 문장을 작성하는 방법이 있습니다.

그리고 ES6 에서는 이러한 문제를 해결하기 위해 `let`, `const` 타입을 만들었습니다.

`let` 와 `const` 의 공통점은 변수 재선언이 불가능한 Block-Scoped 입니다.

차이점은 값을 변경할 수 있는가 입니다.

`let` 는 새로운 값으로 변경할 수 있지만, `const` 는 `=` 로 변경할 수 없습니다.

(물론 `const` 로 선언한 객체의 Property, 배열의 Index 를 접근하여 이들 안의 값을 수정할 수 있습니다.)

```javascript
let a = 10;
let a = 12; // Uncaught SyntaxError: Identifier 'a' has already been declared
a = 12; // OK!

const b = 'asd';
b = 'sdf'; // Uncaught TypeError : Assignment to constant variable.
```

참고로 Block-Scoped 단위도 Hoisting 이 일어납니다.

```javascript
e = 30;
let e; // Uncaught ReferenceError: e is not defined
```

이는 TDZ(Temporal Dead Zone) 때문에 에러가 발생합니다.

```javascript
const a; // const 는 선언과 동시에 값을 할당해야 합니다.
```

물론 `const` 도 마찬가지로 TDZ 때문에 에러가 발생합니다.

게다가 `let` 보다 엄격합니다.

JavaScript 에 TDZ 가 필요한 이유는 `script` 태그에서 바로 실행되는 동적 언어이기 때문입니다.

이를 위해 Runtime Type Check 가 필요합니다. 

**참조 링크**

https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d

[맨 위로](#contents)

---

# Hoisting

```javascript
var _x = foo(10, 20);
function foo(_a, _b){
    return _a + _b;
}

/*
 * var _x = undefined;
 * function foo(_a, _b){
 *   return _a + _b;
 * }
 * _x = foo(10, 20);
 */

// 정상 작동
```

```javascript
var _x = foo(10, 20);
var foo = function(_a, _b){
    return _a + _b;
}

/*
 * var _x = undefined;
 * var foo = ???;
 * _x = foo(10, 20); // ??? 가 _a + _b 를 반환하는 함수는 아닙니다. 
 */

// 오작동
```

함수 로직을 Literal Function 으로 선언하기 이전에 호출을 해도 오류 없이 돌아갑니다.

JavaScript 엔진에서 변수를 선언하기 전에 모든 변수의 값을 `undefined` 로 할당합니다.

선언 된 변수의 값이나 함수 로직을 발견하면 값을 대입 시킨 것처럼 느낄 수 있을 것입니다.

이처럼 변수나 함수의 정의가 범위에 따라 선언과 할당으로 분리 시켜주는 개념을 **호이스팅** 이라 합니다.

호이스팅은 Literal Function 으로 작동하는데, 변수를 이용한 Function 에선 작동하지 않습니다.

이는 JS 엔진에서 객체나 콜백 함수들은 Heap Segment 에서 동적으로 할당하는데, 호이스팅을 하는 시점에선 진행하지 않기 때문입니다. (저자 생각)

[맨 위로](#contents)

---

# Prototype

솔직히 프로토타입(Prototype) 은 면접에서 잘 안 물어보고, 실무에서도 사용 빈도가 적습니다.

그래서 햇깔리는 개념만 간략하게 설명하고, 링크를 남기는 것으로 대체합니다.

**Prototype 정의**

JavaScript 의 모든 객체는 자신의 부모 역할을 하는 객체와 연결 되어 있습니다. 

부모 객체의 프로퍼티, 메소드, 생성자 등을 조회할 수 있습니다. 이를 도와주는 주체를 Prototype 이라고 합니다.

Prototype 을 참조하는 객체 내의 프로퍼티는 크게 `__proto__` 와 `prototype` 으로 나뉩니다.

```javascript
const person = {
    name: '강사람',
    age: 26
};

console.log(person); // __proto__ 는 Object 의 prototype 입니다.

function Person(_name, _age){
    this._name = _name;
    this._age = _age;
}

console.log(new Person('강사람', 26)); // __proto__ 는 Person 의 prototype 입니다.
```

**`__proto__` 프로퍼티**

Chrome V8 엔진을 기준으로 `__proto__` 프로퍼티는 부모 객체의 Prototype 을 가리킵니다.

생성된 각 객체에 공유 프로퍼티를 제공하고 조회할 수 있지만, 확장 혹은 수정해서 사용할 수 없습니다.

물론 객체 로직 밖에서 접근이 불가능합니다.

**`prototype` 프로퍼티**

반대로 `prototype` 프로퍼티는 함수 객체(객체 생성자, Primitive 객체) 만 가지고 있습니다.

이는 생성자로 사용될 때 그 객체의 부모 역할을 하는 객체 정보를 가리킵니다. 

이는 로직 밖에서 접근 가능하고 필요한 메소드를 확장 또는 수정해서 사용할 수 있습니다.

**More...**

프로토타입(Prototype) 에 대한 자세한 사항은 아래 블로그를 참고하시면 더욱 좋습니다.

https://poiemaweb.com/js-prototype

[맨 위로](#contents)

---

# Immutable Object

Immutable Object 는 Java 처럼 객체 생성 이후 값을 변경 불가능한 패턴입니다.

예를 들어 문자열을 합치는 문장을 살펴 보면, `str1` 와 `str2` 의 값은 이미 Heap Segment 에 저장되어 있습니다.

그러나 `str1` 를 `str1` 와 `str2` 를 합쳐서 저장되면 `str1` 의 값이 변경되는 것으로 착각할 수 있습니다.

하지만 `str1` 가 가리킨 값은 그대로 방치하고, `str1` 와 `str2` 를 합친 문자열의 값을 할당하고 가리키는 것입니다.

Primivite 타입 (Number, String, Boolean 등) 은 Immutable 이 보장되어 있습니다.

```javascript
let str1 = 'asdfghjkl';
let str2 = 'qwertyuiop';

str1 = str1 + str2; // 'asdfghjklqwertyuiop' (*)
```

그러나 JavaScript Object 은 Mutable 로 되어 있어 Property 에 해당된 값이 언제든지 변경될 수 있습니다.

`person2` 변수가 `person1` 를 가리키고 난 후, 데이터를 일부 변경하면 아이러니 한 일이 일어납니다. 

`person2` 의 이름을 '배사람' 으로 변경하려다가 `person1` 의 이름도 '배사람' 으로 변해 버립니다.

```javascript
var person1 = {
    name: '김사람',
    age: 26
};

var person2 = person1;
person2.name = '배사람';

console.log(person1.name); // '배사람'
console.log(person2.name); // '배사람'
```

**`Object.assign()`**

참조로 인한 아이러니 현상을 막기 위해 객체의 프로퍼티와 값을 복사하는 Object.assign() 함수를 사용하는 것입니다.

이는 JavaScript ES6 문법에 추가된 메소드입니다. 또한 여러 객체들을 병합하여 복제할 수 있습니다.

Shallow Copy 를 지원하여, 참조 변수의 객체 복제(Deep Copy)는 별도로 처리해야 합니다.

```javascript
var person3 = Object.assign(person1); // { name: '배사람', age: 26 }
var person4 = Object.assign(person1, { address: '서울' }); // { name: '배사람', age: 26, address: '서울' }
```

**`Object.freeze()`**

변수가 참조하는 객체의 값을 냉동 인간처럼 만들어서 값을 아예 변경하지 못 하게 막습니다.

값 변경 시도할 때 따로 오류나진 않습니다. 객체 안의 객체 데이터는 변경할 수 있어 Deep Reference 까지 보장하진 못 합니다.

```javascript
var person5 = {
    person1, address: '수원'
};

Object.freeze(person5);
person5.address = '성남'; // 수원으로 유지된다.
person5.person1.name = '강사람'; // 못 믿겠지만, 강사람으로 변경 됩니다.
```

[맨 위로](#contents)

---

# Object Binding

[맨 위로](#contents)

---

# Closure

계속 작성 하겠습니다!

[맨 위로](#contents)

---

# Callback Function VS Arrow Function

계속 작성 하겠습니다!

[맨 위로](#contents)

---

# Functional Programming

```javascript
let arr = [10, 20, 30];
let twice = arr.map(x => x * 2); // [20, 40, 60]
```

`map`, `reduce`, `filter` 만 사용한 것은 함수형 프로그래밍의 원리를 적용한 도구일 뿐입니다.

함수형 프로그래밍은 순수 함수를 기반으로 로직을 디자인하는 개념입니다.

순수함수는 아래와 같은 원칙을 지켜야 합니다.

- 매개 변수는 1개 이상의 인자를 받아야 합니다.
- 받은 인자를 처리한 결과를 돌려줘야 합니다.
- 쓸데 없는 변수와 로직을 없애야 합니다.
- 함수와 데이터를 중점으로 디자인해야 합니다.

함수형 프로그래밍은 말 그대로 순수함수를 재사용하여 가공된 값을 반환하는 것을 지향합니다.

이의 반대 개념은 명령어 프로그래밍인데 변수의 상태와 참조를 바꾸는 것을 지향합니다.

JavaScript 에서는 `this` 가 동적으로 변해서 순수함수 구성에 무리가 있습니다.

이전에 사용했던 익명 함수의 `this` 는 바인딩을 해야 됩니다.

그렇지만 Arrow Function 에서 `this` 는 상위 스코프의 `this` 를 자동으로 바인딩 해 줍니다.

그래서 함수형 프로그래밍을 구성할 땐 Arrow Function 을 자주 사용하는 것이 좋습니다.

[맨 위로](#contents)

---

# V8 Engine

계속 작성 하겠습니다!

[맨 위로](#contents)

---

# JS Garbage Collection

계속 작성 하겠습니다!

[맨 위로](#contents)

---