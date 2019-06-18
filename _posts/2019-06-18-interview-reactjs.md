---
layout: post
title: "React.js 면접 대비"
date: 2019-06-18 22:00:00
image: "/kangflix/assets/img/category/ct_interview.png"
category: 'interview'
tags:
- React
- Interview
description: React.js 면접 및 지식 포스트입니다.
introduction: React.js 면접 및 지식 포스트입니다.
---

![ReactJS]({{ site.baseurl }}/assets/img/post/interview/reactjs.jpg)

아래의 포스트 링크를 주로 참고하였습니다.

https://www.edureka.co/blog/interview-questions/react-interview-questions/

https://github.com/appear/reactjs-interview-questions-ko

참고하면 좋은 포스트 링크도 주제 별로 같이 남겼습니다.

수정이 필요한 사항은 아래 댓글 서비스를 사용해서 요청하시면 바로 정정 하겠습니다.

추가로 ReactJS 에 대한 상세한 Tutorial 은 여기서 다루지 않으니 이는 주제 별로 나오는 링크를 참고하시면 더욱 도움 될 것입니다!

---

# Contents

* Contents
{:toc}

---

# ReactJS 정의

ReactJS 는 자바스크립트 라이브러리의 하나로 사용자 인터페이스(User Interface) 를 만들기 위해 사용됩니다.

싱글 페이지(Single Page) 나 모바일(Mobile) 어플리케이션을 개발할 때 주로 사용됩니다.

ReactJS 어플리케이션이 복잡해지면 상태 관리(Redux, MobX), 라우팅(React Router), API 통신(Axios) 을 위한 라이브러리를 추가해야 합니다.

JavaScript ES6 문법을 보편적으로 사용합니다. 이를 브라우저 환경에서 컴파일 할 수 있도록 Babel Transpiler 로 번역해야 합니다.

[맨 위로](#contents)

---

# ReactJS 주요 특성

**Virtual DOM 을 사용하여 브라우저에 DOM 을 렌더링 합니다.**

변경되는 데이터가 많은 경우에 React 의 효력을 느낄 수 있습니다.

**Server-Side Rendering 을 제공합니다.**

Node.js 안에서 가능하고, Next.js 라이브러리를 사용하는 경우가 있습니다.

**React 컴포넌트는 단방향 데이터 플로우, 단방향 데이터 바인딩을 따릅니다.**

Vue 컴포넌트도 React 의 컴포넌트 사상을 따르게 되면서 단방향 데이터 플로우를 제공합니다.<br/>
반대로 `v-model` 를 사용할 때 양방향 데이터 바인딩을 따르는 차이가 있습니다.

[맨 위로](#contents)

---

# ReactJS 장단점

**장점**
- JSX 문법을 사용하여 컴포넌트의 가독성이 좋습니다.
- 모바일, 웹, VR 등 디바이스에 따른 확장이 쉬워집니다.
- User Interface 에만 집중할 수 있어 관심사의 분리가 용이합니다.
- Angular, Meteor 등의 프레임워크와 통합하여 사용할 수 있습니다.
- Spring, django, Ruby On Rails 등 서버 프레임워크의 Web Application 에서 구성하여 사용할 수 있습니다.
- TypeScript 로 타입을 지정하여 컴포넌트를 정형화 시킬 수 있습니다.
- Jest Framework 로 React 의 컴포넌트를 단위로 테스팅할 수 있습니다.

**단점**
- JSX 문장과 ES6 문장을 웹 브라우저에서 분석하기 위해 Transpiler 가 필요합니다.
- ReactJS 는 라이브러리 이지만, 규모가 생각보다 크기 때문에 초급자들이 공부하기 힘듭니다.
- 데이터 변동이 적은 정적 페이지를 구현하면, 라이브러리의 메모리 낭비를 고려해야 합니다.

[맨 위로](#contents)

---

# Virtual DOM 정의와 비교

렌더링(Rendering) 은 브라우저 엔진에서 실행하는 페이지의 HTML, CSS 문서를 해석하고 각 태그들의 트리를 DOM 노드로 변환하여 사용자에게 보여지는 과정입니다.

하지만 ReactJS 에서는 변경사항만 적용된 Virtual DOM 을 만듭니다.

ReactJS 에서 문장 작성을 완료하고, Real DOM 과 Virtual DOM 의 차이점을 비교하고 변경된 부분만 Real DOM 에 적용합니다.

DOM 객체 안의 데이터가 자주 변경되는 작업을 하면 렌더링 퍼포먼스를 올리는데 도움됩니다.

**브라우저 DOM 렌더링 과정 참고하기**

https://d2.naver.com/helloworld/59361

| Real DOM | 비교 사항 | Virtual DOM |
|:--------:|:--------:|:--------:|
| 느리다. | 렌더링 속도 | 빠르다. |
| 곧바로 적용 된다. | 접근 직관성 | Transpiler 의 도움이 필요하다. |
| 새로운 DOM 을 만든다. | 단일 데이터의 값의 변경 | JSX 문장에만 영향이 있다. |
| 많이 잡아 먹는다. | 메모리 용량 차지 | 용량 낭비가 줄어든다. |
| 매우 복잡하다. | DOM 조작 | 쉬워진다. |

> **렌더링 속도**
>
> 브라우저 엔진에서 실행된 페이지의 HTML, CSS 문서의 DOM 트리를 구성해야 하기 때문에 Real DOM 의 렌더링 속도는 느립니다.
>
> 그러나 Virtual DOM 은 변경된 부분만 Real DOM 에 적용하기 때문에 렌더링 속도는 빠릅니다.

> **접근 직관성**
> 
> HTML 와 CSS 문장을 직접 수정하면 곧바로 페이지에 있는 문서들을 다시 읽어들여 렌더링을 진행합니다.
>
> 허나 Virtual DOM 의 내용을 수정하면, JSX 문장을 브라우저에서 해석할 수 없어 Babel, Webpack 등의 Transpiler 로 번역하고 렌더링을 진행합니다.

> **단일 데이터 변경 및 메모리**
> 
> 데이터의 값이 일부 변경되거나 추가 되면 Real DOM 은 DOM 노드를 무작정 새로 만들어 렌더링해야 합니다. 
> 
> 이로서, 페이지에 있는 HTML, CSS 의 노드를 렌더링하는 메모리에만 집중되어 용량 낭비가 나옵니다.
>
> 하지만 Virtual DOM 은 JSX 문장에만 영향을 받습니다. 렌더링의 메모리는 수정하는 DOM 노드에만 영향을 줘서 용량 낭비가 줄어듭니다.

> **DOM 조작**
> 
> Real DOM 에서 DOM 노드를 조작하기 위해 탐색해야 합니다. 전체 문장 안에서 찾아야 하는 DOM 의 양이 많아져서 조작의 어려움이 있습니다.
> 
> 하지만 Virtual DOM 에서는 Real DOM 안에서 깔리고 난 후, 탐색이 필요한 근방 DOM 노드를 탐색하고 조작할 수 있습니다. 탐색할 DOM 의 양이 크게 줄어들어 조작이 쉬워집니다.

[맨 위로](#contents)

---

# JSX

```jsx
// ES6
const tag = <p>Hello! JSX!</p>

// ES5 이전
var tag = React.createElement('p', {}, 'Hello! JSX!');
```

JSX 는 **J**ava**S**cript e**X**tension 의 줄임말입니다.

HTML 와 매우 유사한데, Application 을 빌드하면 Babel 를 통해 트랜스파일이 되어야 브라우저에서 보여질 수 있습니다.

JSX 와 HTML 의 프로퍼티 차이점이 몇 개 있습니다.

- HTML 의 `class` 를 JSX 에선 `className` 으로 사용해야 합니다.
- HTML 의 `style` 는 JSX 에선 CSS 객체(프로퍼티가 CSS 속성이지만, 카멜체로 기재해야 함.) 를 넣어야 합니다.
- 그리고 JSX 의 프로퍼티는 카멜체로 구성된 것이 관례입니다. (`onclick` → `onClick`)
- HTML 는 `<my-component>` 와 같은 문법으로 사용했지만, JSX 는 `<MyComponent>` 처럼 파스칼체를 사용해야 합니다.

ReactJS 는 JSX 를 사용해서 렌더링 하지만, VueJS 는 Vue Template 문법을 사용하여 렌더링을 합니다.

[맨 위로](#contents)

---

# Fragment

ReactJS 에서 반환하는 JSX 문장은 DOM 트리의 Root 가 1개여야 합니다.

`dom2` 처럼 작성하면 문법 오류가 나옵니다. 그래서 여러 컴포넌트가 나오기 위해 새로운 DOM 을 만들어야 합니다.

그래서 HTML 와 CSS 에 따른 렌더링에 영향이 없이 여러 DOM 객체를 하나로 묶어주는 태그가 Fragment 입니다.

이는 복수의 데이터를 렌더링할 때 `key` 값으로 설정할 수 있습니다.

또한 이전의 `div` 태그로 묶음으로 `style` 등의 렌더링 결과가 달라지는 사고를 방지할 수 있습니다.

`render()` 함수나 Functional 컴포넌트에서 DOM 객체를 반환할 때 사용하는 것이 좋습니다.

```jsx
const dom1 = <h1>Hello, World</h1> // OK

const dom2 = (
    <h1>Hello, World</h1>
    <h2>Hello, React</h2>
); // Oh, No.

const dom2_fragment = (
    <Fragment>
        <h1>Hello, World</h1>
        <h2>Hello, React</h2>
    </Fragment>
); // OK
```

[맨 위로](#contents)

---

# Component 정의와 비교

컴포넌트는 React Application 을 구성하는 User Interface 를 이루는 조각입니다.

컴포넌트 안에 또 다른 컴포넌트들이 구성될 수 있고, `props` 를 사용하여 데이터를 전달할 수 있습니다.

또한 컴포넌트는 이전에 사용했던 DOM 객체를 다른 데이터로 재활용할 수 있습니다.

**Element 와 Component 의 비교**

```jsx
const tagElement = <h1>Hello, Element!</h1>

const tagComponent = ({ title }) => <h1>{ title }</h1>
```

HTML 단일 태그로 정의만 한 DOM 은 Element 입니다. 이를 차지하는 메모리 공간은 Data Segment 입니다.

그러나 Component 는 함수나 클래스를 호출하여 DOM 을 생성합니다. 이를 차지하는 메모리 공간은 Stack Segment 입니다.

[맨 위로](#contents)

---

# Component 종류

컴포넌트를 생성하는 방법에 따라 달라집니다. 이는 3가지로 나뉩니다.

**Functional Component**

```jsx
const MyComponent = ({ title }) => (
    <p>{ title }</p>
);

function MyComponent(props) {
    return (
        <p>{ props.title }</p>
    );
}

export default MyComponent;
```

- Stateless Component 라고도 합니다.
- 자식 컴포넌트에 렌더링 할 데이터를 `props` 로 전달할 때 주로 사용합니다.
- Life Cycle API 함수, `ref` 콜백을 따로 사용할 수 없습니다.
- 컴포넌트 단위 테스트가 용이해집니다.
- Life Cycle 를 사용하지 않아 성능 향상은 보장합니다. 하지만 클래스 컴포넌트보다 7~11% 정도 빠르다고 합니다.
- Redux 에서 Container 단위 컴포넌트, Router 의 Page 단위 컴포넌트에서 주로 사용합니다.

**Component**

```jsx
class MyComponent extends Component {
    constructor(props){
        super(props);
        this.state = { subtitle : '' };
    }

    render() {
        const { title } = this.props;
        const { subtitle } = this.state;

        return (
            <div>
                <h1>{ title }</h1>
                <h2>{ subtitle }</h2>
            </div>
        );
    }
}

export default MyComponent;
```

- `props`, `state`, Life Cycle API 를 함께 사용할 수 있는 기본 컴포넌트입니다.
- Life Cycle 중 `shouldComponentUpdate()` 의 반환 값에 따라 컴포넌트의 리-렌더링 과정을 거칩니다.
- `shouldComponentUpdate()` 를 선언하지 않으면 무조건 `true` 를 반환하여 무조건 리-렌더링을 합니다.
- `shouldComponentUpdate()` 함수에서는 `JSON.stringify()` 나 Shallow Comparison 검사를 수행하지 않아야 합니다.
- HOC(Higher Order Component) 패턴에서 주로 사용합니다.
- `render()` 함수에서는 Root 가 1개인 DOM 을 반환해야 합니다.
 
**PureComponent**

```jsx
class MyComponent extends PureComponent {
    constructor(props){
        super(props);
        this.state = { subtitle : '' };
    }

    render() {
        const { title } = this.props;
        const { subtitle } = this.state;

        return (
            <div>
                <h1>{ title }</h1>
                <h2>{ subtitle }</h2>
            </div>
        );
    }
}

export default MyComponent;
```

- Class Component 처럼 `props`, `state`, Life Cycle API 를 사용할 수 있습니다.
- 다만, `shouldComponentUpdate()` 함수는 Shallow Comparison 방식으로 이미 구현되어 있습니다.
- 중첩된 Object 에서는 이를 사용하는 것이 무의미할 것입니다.
- 복잡하지 않은 데이터 구조에서 `state` 를 사용해야 하면 이를 선택하는 것이 좋습니다.

**TOAST Meetup Component 종류에 따른 렌더링 성능**

아래 링크는 Component 종류 별 DOM 렌더링 성능을 참고하기 좋은 포스트입니다.

https://meetup.toast.com/posts/110

[맨 위로](#contents)

---

# Props

`props` 는 HTML 태그의 Property 처럼 React Component 에 전달되는 값을 포함한 값들의 객체입니다.

`props` 데이터는 부모 Component 에서 자식 Component 로 전달 됩니다.

Class Component, Pure Component 에서 `props` 를 사용하기 위해 `constructor(props)` 함수에서 `super(props)` 를 해야 합니다.

이는 ReactJS 에서 단방향 데이터 흐름을 사용하는 증거이기도 합니다.

이에 해당되는 값은 오로지 Read-Only 입니다. 또한 컴포넌트에서 구현한 이벤트 핸들링 함수도 전달할 수 있습니다.

[맨 위로](#contents)

---

# State

`state` 는 React Component 안에서 사용할 수 있고, 언제든지 수정할 수 있는 데이터입니다. 

이는 `constructor(props)` 함수에서 `this.state` 에 값을 대입하여 초기화 합니다.

`state` 는 가능하면 단순하게 구성하는 것이 컴포넌트의 무게가 줄어듭니다.

`state` 는 직접 업데이트할 수 없고, `this.setState({})` 함수를 사용해서 업데이트 해야 합니다. 

다만, `this.setState({})` 함수를 실행할 때 일부 Life Cycle API 에서 무한 루프가 나올 수 있으니 주의해야 합니다.

이 메소드를 실행하면 무조건 Re-Rendering 을 합니다.

`props` 에서 받아온 데이터를 컴포넌트 안에서 동기화 할 때 `state` 에 저장하여 사용합니다.

[맨 위로](#contents)

---

# Life Cycle API 정의

Class Component 나 Pure Component 를 사용하면 Life Cycle API 를 사용할 수 있습니다.

Component 의 생명 주기 단계는 크게 컴포넌트 생성, 컴포넌트 데이터 업데이트, 컴포넌트 소멸 3가지로 나뉩니다.

**컴포넌트 생성**

React 컴포넌트가 브라우저 화면에 보이는 순간을 뜻합니다.

컴포넌트의 DOM 이 브라우저에 안 나타나지만, 부모 컴포넌트나 Element 렌더 주체에서 호출되면 컴포넌트의 JSX 문단에 따라 DOM 트리를 구성합니다.

여기에선 React 컴포넌트에서 사용할 데이터를 호출하거나 이벤트 등록 등 전처리 작업을 실행하는 것이 좋습니다.

**컴포넌트 데이터 업데이트**

컴포넌트가 브라우저 화면에 보여지고 난 후, `props` 나 `state` 의 데이터가 변경되는 순간을 뜻합니다.

React 는 단방향 데이터 흐름 기반 Application 으로 `props` 와 `state` 의 데이터가 변경되면 무조건 리-렌더링을 거치게 됩니다.

그래서 `shouldComponentUpdate()` 메소드를 사용해서 리-렌더링 빈도를 줄이면 렌더링 성능을 어느 정도 개선할 수 있습니다.

```
새 Props 받아오기 → 리-렌더링 여부 검사 → 리-렌더링 시작 이전 → 리-렌더링 → 리-렌더링 완료 이후 
```

React 16.3 이전까지만 해도 `props` 데이터를 새로 받는 것만 집중하여 위와 같은 과정으로 Life Cycle 함수가 구현되어 있었습니다.

```
새 Props 받아서 State 에 동기화하기 → 리-렌더링 여부 검사 → 리-렌더링 → 스냅샷 저장 → 리-렌더링 완료 이후
```

그러나 컴포넌트 내의 변수인 `state` 의 동기화를 중점으로 두어 위의 과정으로 개편되어 있습니다. 

**컴포넌트 소멸**

이는 간단하게 컴포넌트가 브라우저에서 안 보이고 소멸되는 순간을 뜻합니다.

여기선 컴포넌트의 DOM 이 브라우저에서 아예 소멸되어 안 보이게 됩니다. 

이는 CSS Style 에 `display` 속성의 `none` 으로 안 보이는 것과 전혀 다릅니다.

[맨 위로](#contents)

---

# Life Cycle Method

![React Life Cycle]({{ site.baseurl }}/assets/img/post/interview/component_life_cycle.png)

<h3>컴포넌트 생성</h3>

**constructor(props)**

React 컴포넌트의 생성자 함수입니다.

여기서 `props` 를 사용하기 위해 `super(props)` 문단을 꼭 써야 하고, `state` 를 초기화 할 수 있습니다.

```javascript
// ...
constructor(props){
    // ...
    this.handleChange = this.handleChange.bind(this);
}
// ...
```

또한 위 문장처럼 이벤트를 바인딩한 멤버 변수를 정의할 때 사용됩니다.

**componentDidMount()**

렌더링 된 컴포넌트가 브라우저 창에 보이면 이 함수가 실행 됩니다. 

이 함수에서는 컴포넌트에서 필요한 전처리 과정들을 기재합니다.

- 타이머 등록
- AJAX 요청 (`axios`, `fetch` 등을 사용)
- DOM 을 사용하는 외부 라이브러리 연동(D3, Google Charts 등)

<h3>컴포넌트 데이터 업데이트</h3>

**static getDerivedStateFromProps(nextProps, prevState)**

새로운 `props` 의 값을 받아와 컴포넌트 변수인 `state` 에 대해 동기화 할 때 사용합니다.

`static` 함수이기 때문에 이 안에서는 `this` 를 못 사용합니다. 

대신에 새로운 `props` 변수의 값으로 새로운 `state` 값을 반환 시켜 저장 시켜줍니다.

또한 이 함수에서는 `props` 의 변경 사항이 없더라도 `null` 를 반환 해야 합니다.

**shouldComponentUpdate(nextProps, nextState)**

리-렌더링으로 인한 성능 최적화를 위해 사용 됩니다. 

단일 컴포넌트는 변경된 데이터가 그 때마다 바로 변경 해 주면 끝입니다.

상관 관계가 있는 컴포넌트에서 부모 측의 컴포넌트가 `props` 와 `state` 의 변경이 많아지면, 자식 컴포넌트에서도 쓸데 없는 리-렌더링 과정이 일어나서 렌더링 성능이 떨어지게 됩니다.

참고로 `Component` 를 상속 시키면 이를 디테일하게 구현할 수 있습니다.
 
반면에 `PureComponent` 를 상속 시키면 얕은 비교를 통하여 자동으로 구현되어 있습니다.

이 함수에서 `true` 값을 반환 시켜야 리-렌더링 과정이 일어납니다. 이를 구현하지 않으면 무조건 `true` 를 반환합니다.

반대로 `false` 를 반환하면 리-렌더링 과정이 아예 안 일어나고, 컴포넌트 생성 시점의 DOM 만 보여집니다.

**getSnapshotBeforeUpdate(prevProps, prevState)**

DOM 에 대한 변화가 일어나기 직전의 시점의 DOM 상태를 가져올 수 있습니다.

`componentDidUpdate` 에서 세 번째 파라미터로 사용할 수 있습니다.

주로 애니메이션 효과 초기화, 이벤트 리스너를 없애는 작업을 합니다. 

**componentDidUpdate(prevProps, prevState, snapshot)**

컴포넌트가 리렌더링을 마칠 때 실행 되는 함수입니다. 

여기서 `this.state`, `this.props` 는 이미 업데이트 된 값이 저장 되어 있습니다. 

그리고 `snapshot` 변수를 이용하여 변경된 값을 바로 비교하여 렌더링할 수 있습니다.

또한 `this.setState({})` 함수를 실행할 때 무한 루프가 발생할 수 있으니 주의해야 합니다.

참고로 여기서는 컴포넌트 생성과 업데이트 이후 라우터에 대한 액션들을 처리할 때 많이 사용합니다.

<h3>컴포넌트 소멸</h3>

**componentWillUnmount()**

컴포넌트가 더 이상 표기될 필요가 없을 때 실행 되는 함수입니다. 

`setTimeout()`, `setInterval()` 등 타이머 함수의 속성을 없애는 `clearTimeout()` 함수를 이용할 때 사용됩니다.

[맨 위로](#contents)

---

# Key Props 

```javascript
const people = [
    { id: 1, name: '강사람', age: 26 },
    { id: 2, name: '조사람', age: 28 },
    { id: 3, name: '배사람', age: 27 },
    { id: 4, name: '박사람', age: 26 },
    { id: 5, name: '이사람', age: 26 },
    { id: 6, name: '저사람', age: 25 }
];

const people_render = people.map(p => <PersonInfo key={p.id} person={p} />);
```

`key` 는 복수 데이터를 컴포넌트에 렌더링할 때 사용해야 합니다.

물론 사용하지 않아도 문제는 발생하지 않지만, 경고 창으로 사용 하도록 유도합니다.

이는 렌더링할 자식 컴포넌트에서 조회할 수 없지만, 부모 컴포넌트에서 데이터 목록의 변경 및 추가, 제거 항목을 쉽게 분별할 수 있습니다.

`map` 함수에선 `data` 와 `index` 를 가져올 수 있는데 항목 순서의 변동이 심해지면 `map` 의 `index` 를 사용하지 않는 것이 좋습니다.

`state` 값에 이상이 발생할 수 있기 때문에 단일 객체에서 고유 데이터를 사용하는 것이 좋습니다.

참고로 Vue.js 에서도 복수 데이터를 렌더링할 때 `key` 값 바인딩을 요구합니다.

[맨 위로](#contents)

---

# Children Props

```jsx
const ListView = ({ children }) => (
    <ul>
        { children }
    </ul>
);

const ElementView = ({ title }) => (
    <li>{ title }</li>
);

const TigerComponent = () => (
    <ListView>
        <ElementView title="너희가 힙합을 아느냐" />
        <ElementView title="난 널 원해" />
        <ElementView title="소외된 모두 왼발을 한 보 앞으로" />
    </ListView>
);

export default TigerComponent;
```

React 컴포넌트는 `props` 로 데이터 뿐만 아니라 또 다른 컴포넌트를 전달할 수 있습니다.

부모 컴포넌트 안에 자식에게 보내고 싶은 컴포넌트를 작성하면 이것이 Children Props 가 됩니다.

자식 컴포넌트에서 전달 받은 컴포넌트를 렌더링하고 싶으면, `this.props.children` 으로 가져옵니다.

참고로 `children` 프로퍼티는 **컴포넌트** 의 배열입니다. 이의 요소를 `child` 라고 합니다.

`child` 컴포넌트 안에서 사용하는 `props` 의 값을 `children` 을 전달 받은 컴포넌트에서 접근할 수 있습니다.

(그러나 이를 많이 사용하면 컴포넌트 단위 유지보수에 어려움이 존재할 수 있습니다.)  

이는 `React.Children` 에서 제공하는 Children API 를 사용하여 렌더링을 제어할 수 있습니다.

Children API 메소드는 `map`, `forEach`, `count`, `toArray` 등이 있습니다.

[맨 위로](#contents)

---

# ref

React 컴포넌트 안에서 DOM 객체를 접근하는 경우가 더러 있습니다.

간단한 예로 `input` 태그에 입력한 값을 가져오는 것입니다. 

이는 `event` 객체를 사용하면 단방향 데이터 흐름으로 처리할 수 있습니다.

```jsx
class InputField extends PureComponent {
    constructor(props){
        super(props);
        this.state = { text1: '', text2: '' };
    }

    // 데이터 바뀜에 따른 handler 함수는 event 객체를 잘 사용하면 통합해서 사용할 수 있습니다.
    _handleChange(event) {
        const { target } = event;
        this.setState({
            [ target.name ] : target.value
        });
    }

    render() {
        const { text1, text2 } = this.state;
        
        // <> 는 Fragment 와 같은 맥락입니다.
        return (
            <>
                <input type="text" name="text1" value={ text } onChange={ this._handleChange.bind(this) } />
                <input type="text" name="text2" value={ text } onChange={ this._handleChange.bind(this) } />
            </>
        );
    }
}
```

그러나 마우스나 키보드 등 입력 장치를 통한 이벤트를 굳이 거치지 않고 DOM 에 직접 접근해야 하는 경우가 있습니다.

- `input`, `textarea` 태그에 포커스.
- 특정 DOM 의 크기 추출.
- 스크롤 위치 추출 및 자동 조정.
- DOM 안에 외부 라이브러리를 사용하거나 제어할 때.

이러한 경우에는 `ref` 를 사용하는 것이 좋습니다.

예를 들어 `input` 태그에 포커싱하는 예제를 작성하면 다음과 같습니다.

```jsx
class FocusField extends PureComponent {
    constructor(props){
        super(props);

        // 또 다른 방법은 input 태그의 ref 프로퍼티에 ref => this.field = ref 로 직접 바인딩하는 방법이 있습니다.
        this.field = React.createRef();
    }

    _handleClick = () => {
        this.field.focus();
    }

    render(){
        // 참고로 Arrow Function 이고, 파라미터가 없는 handling 메소드는 그냥 전달해도 큰 상관은 없습니다.
        // 컴포넌트 안에 파라미터가 없는 Arrow Function 메소드는 this._handleClick.bind(this) 와 유사합니다.
        // 다만 onSubmit 에선 event 의 전파를 막아야 되기 때문에 event 파라미터를 포함시켜야 하고, 파라미터가 있으면 Arrow Function 으로 처리해야 합니다.
        return (
            <>
                <input type="text" ref={this.field} />
                <button onClick={ this._handleClick }>포커싱</button>
            </>
        )
    }
}
```

**`ref` 를 과다 사용하면?**

`state` 는 컴포넌트 안에 사용할 데이터를 소유해야 합니다.

허나 `ref` 는 참조를 하는 DOM 노드의 객체 인스턴스입니다.

이는 모든 컴포넌트 중의 일부에 필요할 것입니다.

하지만 단 하나의 컴포넌트에만 `ref` 를 계속 사용하는 것은 `state` 의 기본 철학에 적합하지 않습니다. 

그래서 `ref` 는 최상위 부모 컴포넌트에서 사용하여 `props` 에 전달하는 방법이 적합합니다.

**More Tutorials**

`ref` 를 응용하는 튜토리얼은 아래 포스트들을 참고하시길 바랍니다.

- https://velopert.com/1148
- https://css-tricks.com/working-with-refs-in-react/

[맨 위로](#contents)

---

# HOC(Higher Order Component)

계속 작성 하겠습니다!

[맨 위로](#contents)

---

# React Hooks

React Hooks 는 쉽게 설명하면 Functinal Component 안에서 `state` 를 사용하는 새로운 기능입니다.

이는 React v16.8 부터 사용할 수 있습니다.

React Hooks 를 응용하는 튜토리얼은 아래 포스트를 참고하시길 바랍니다.

- https://velog.io/@velopert/react-hooks

[맨 위로](#contents)

---

# Redux

계속 작성 하겠습니다!

[맨 위로](#contents)

---

# Redux-Thunk

계속 작성 하겠습니다!

[맨 위로](#contents)

---

# Redux-Saga

계속 작성 하겠습니다!

[맨 위로](#contents)

---