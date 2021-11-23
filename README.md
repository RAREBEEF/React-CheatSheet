# **React**

>**A JavaScript library for building user interfaces**  

유저 인터페이스를 만들기 위한 JS 라이브러리이다.

# **주요 키워드**
- View를 다루는 라이브러리
- 렌더링과 업데이트에만 관여한다.
- Component Based Development  
    - 독자적인 코드 블럭(HTML + CSS + JS)  
    - 작업의 단위
- Virtual DOM  
    - DOM을 직접 다루지 않고 React에게 권한을 위임한다.
- JSX  
    - JS의 확장 문법으로, JS 내에서 HTML 코드의 표현이 가능하다.
- CSR & SSR

<br/>
<br/>

# **Component Based Development**

## **Component**  
컴포넌트란 직접 이름을 지정하고 그에 대한 어트리뷰트 등을 설정하여 표현할 수 있는 구성을 말한다.  

쉽게 설명하면 컴포넌트는 HTML, CSS, JS를 한데 묶어서 지정한 스타일과 동작을 갖고 있는 태그를 만드는 것이라고 할 수 있다.

최상위 컴포넌트를 하나 구성하고, 그 하위로 타이틀 컴포넌트, 네비게이션 컴포넌트, 컨텐츠 컴포넌트, 푸터 컴포넌트 등을 삽입하는 방법을 통해 하나의 웹페이지를 제작할 수 있다. 이러한 구조를 컴포넌트 트리라고 부르며, 돔 트리와 거의 동일한 형태를 갖고있다.

<br/>
<br/>

# **Virtual DOM**
React는 가상의 돔 트리를 통해 이전과 이후 상태를 비교하여 바뀐 부분만 자동으로 수정해주기 때문에 직접 바뀐 부분을 찾아서 수정할 필요가 없다.

<br/>
<br/>

# **CSR & SSR**

## **CSR**

>**Client Side Rendering**

JS가 로드되고 React 애플리케이션의 실행이 완료되기 전까지 화면에 아무것도 출력되지 않으며, 동작도 불가능하다.

## **SSR**

> **Server Side Rendering**  

HTML만 로드되면 React 애플리케이션의 실행이 완료되지 않았어도 화면에 출력되지만, 동작은 애플리케이션 실행이 완료된 후에 가능하다.

<br/>
<br/>

# **React 핵심 모듈**

1. **ReactDOM**  
    ```js
    import ReactDOM from "react-dom";
    ```

    리액트 컴포넌트를 HTML Element와 연결하는 역할을 한다.
    
    ```js
    ReactDOM.render(
      <Hello name="RAREBEEF" />,
      documnet.querySelector(".greeting")
    );
    ```

2. **React**  
    ```js
    import React from "react";
    ```
    리액트 컴포넌트를 만들 때 사용한다.
    ```js
    class Hello extends React.Component {
      render() {
        return (
          <span>
            Hello {this.props.name}
          </span>
        );
      };
    };
    ```

<br/>
<br/>

# **프로젝트 생성**

CRA를 이용한 프로젝트 생성과 그 외 편의를 위한 패키지 설치에 대해 설명한다.

## **CRA 설치**
`$ npx create-react-app 프로젝트경로`  
위 명령으로 리액트 프로젝트를 간단하게 시작할 수 있다. Webpack과 Babel 등을 기반으로 하며 리액트와 필요한 패키지들이 자동으로 설치된다.  

- CLI

  - `$ npm start`  
  개발 서버 오픈

  - `$ npm build`  
  프로젝트 빌드

  - `$ npm test`  
  Jest를 통한 test

  - `$ npm eject`  
  React에서 분리


## **ESLint**
ESLint는 코드 규칙을 설정하고 그에 맞춰 코드를 작성할 수 있도록 도와준다.  

CRA를 설치할 경우 함께 설치된다.

package.json 에서 `"eslintConfig"` 에 rules를 추가하고 다양한 코드 규칙을 지정할 수 있다.  

CRA를 설치했는데 ESLint가 동작하지 않을 경우 초기화를 한 번 진행하고, 생성된 .eslintrc.js 파일에서 규칙 등 구성 옵션을 지정하여 사용한다. 이 경우 package.json 파일의 "eslintConfig" 항목은 제거.

*예시, 세미콜론 항상 붙이기*
```json
"rules": {
  "semi": ["error", "always"]
}
```

### **별도로 설치할 경우**  
`$ npm i eslint -D`  
를 통해 설치가 가능하며, 설치 후 `$ npx eslint --init` 명령을 통해 eslint를 초기화하고 옵션을 지정할 수 있다.

몇 가지 선택을 거쳐 옵션 설정이 완료되면 **.eslintrc.js 구성 옵션 파일**이 생성된다. 이 파일 내에서 코드 규칙을 포함하여 매우 세부적인 옵션 설정이 가능하다.


### **CLI**
문법 체크는 `$ npx eslint 파일명` 을 통해 가능한데, **eslint vscode 플러그인**을 설치하면 별도의 명령 없어도 빨간 밑줄로 코드 규칙에 어긋나는 부분을 알려준다.

`$ npx eslint 파일명 --fix` 명령어를 사용하면 규칙에 어긋나는 부분을 자동으로 수정해준다.

### **JSX 코드 에러 발생 시**
JSX 부분이 규칙에 어긋난다고 나타날 경우 eslint 구성 옵션 파일의 rules 부분에 아래 내용을 추가한다.  

`import React` 가 없는 경우와 JS 파일 내에서 JSX 코드를 사용하는 경우를 허용하는 규칙이다.
```js
"react/react-in-jsx-scope": "off",
"react/jsx-filename-extension": [1, { extensions: [".js", ".jsx"] }]
```

## **Prettier**
Prettier 역시 코드를 일관되고 가독성이 좋게 수정해주는 역할을 한다.  

`$ npm i prettier -D`

위 명령으로 npm으로 설치할 수도 있지만, vscode의 플러그인에서 설치하는 것을 권장한다.

플러그인 설치 후 vscode 설정에서 default fomatter를 prettier로 지정하고 Format on save를 활성화하면 저장 시마다 자동으로 코드가 수정된다.

npm으로 설치한 경우 코드 규칙을 수정하고 싶다면 프로젝트 루트에 .prettierrc.json 구성 옵션 파일을 생성하고 그 내부에 규칙을 작성하면 된다.
```json
// 규칙 예시: 작은 따옴표 사용하기
{
  "sicgleQuote": true
}
```

또한 Prettier와 ESLint는 충돌을 일으킬 수 있는 규칙이 존재한다.  
둘을 같이 사용할 경우 아래 내용을 추가 수행한다.

1. 추가 모듈 설치  
  `$ npm i eslint-plugin-prettier eslint-config-prettier -D`

2. .eslint 구성 옵션에 아래 내용 추가
  ```
  {
    "plugins": ["prettier"],
    "extends": ["eslint:recommended", "plugin:prettier/recommended"],
    "rules": {
      "prettier/prettier": "error"
    }
  }
  ```

## **husky**
특정 git hook에 특정 명령을 실행할 수 있도록 도와준다.

프로젝트의 git 버전 관리를 시작한 뒤에 설치해야한다.

- husky 설치  
  `$ npm i husky -D`

- git hook 설치  
  `$ npx husky install`

- package.json "scripts"에 명령 추가  
  `"prepare": "husky install"`

- 활용 예시, 버전 commit 전에 `$ npm test` 실행하기  
  `$ npx husky add .husky/pre-commit "npm test"`

## **lint-staged**
lint-staged와 husky를 연결하여 commit 이전에 eslint와 prettier를 실행하도록 할 수 있다.

- lint-staged 설치  
  `$ npm i lint-staged -D`

- husky 지정  
  `$ npx husky add .husky/pre-commit "npx lint-staged"`

- lint-staged로 실행할 내용 지정,  
  package.json에 작성한다.
  ```json
  "lint-staged": {
    "**/*.js": [
      "eslint --fix",
      "prettier --write",
      "git add ."
    ]
  }
  ```

## **React Dev Tools**
React Developer Tools를 이용하여 컴포넌트를 디버깅할 수 있다. 크롬의 플러그인으로 설치가 가능하다.  

설치 후 리액트 앱의 개발 서버를 열고 크롬 개발자 모드에서 상단의 >> 버튼을 클릭하면 Components 와 Profiler 라는 항목이 추가된 것을 볼 수 있다.  

Component 탭에서는 컴포넌트의 Props와 state 등의 값을 변경해보고 앱이 어떤 식으로 변경되는지 확인해볼 수 있다.

<br/>
<br/>

# **Component 만들기**
React의 컴포넌트는 대표적으로 **클래스와 함수를 사용**하여 만들 수 있다.  
함수는 일반 함수와 화살표 함수 두 가지 방법 모두 사용 가능하다.  

컴포넌트를 사용하기 위해서는 export/import가 필요하다.  
default와 named 모두 가능하다.

## **Class Component**
```js
// 컴포넌트 정의
import React from "react";

class ClassComponent extends React.Component {
  render() {
    return <div>RAREBEEF</div>;
  };
};

export default ClassComponent;

// 컴포넌트 사용
// HTML의 #root 태그에 컴포넌트가 삽입된다.
import React from "react";
import ReactDOM from "react-dom";
import ClassComponent from "---.js";

ReactDOM.render(
  <ClassComponent />,
  document.querySelector("#root1")
);
```

## **Function Component**
```js
// 컴포넌트 정의(일반 함수 & 화살표 함수)
import React from "react";

export function NomalFunctionComponent() {
  return <div>RAREBEEF</div>;
};

export const ArrowFunctionComponent = () => {
  return <div>RAREBEEF</div>;
};

// 컴포넌트 사용
import React from "react";
import ReactDOM from "react-dom";
import {NomalFunctionComponent, ArrowFunctionComponent} from "---.js";

ReactDOM.render(
  <NomalFunctionComponent />,
  document.querySelector("#root2")
);
ReactDOM.render(
  <ArrowFunctionComponent />,
  document.querySelector("#root3")
);
```

<br/>
<br/>

# **React.createElement()**
```js
React.crateElement(
  type,       // 태그 이름 or 컴포넌트 or Fragment
  [props],      // 컴포넌트에 넣을 데이터 객체
  children[, children...]  // 자식으로 넣을 요소'들'
);
```
위의 `React.createElement()` 를 사용하여 컴포넌트를 만들 수도 있다.  

다만 트리의 중첩이 증가할수록 굉장히 복잡해지는 단점이 존재하여 잘 쓰이지 않고 **JSX**를 사용하여 컴포넌트를 만들게 된다.

<br/>

사용 예시 1
```js
ReactDOM.render(
  React.createElement("h1", null, "h1 태그 삽입"),
  document.querySelector("#root");
);
```
결과물 1
```html
<div id="root">
  <h1>h1 태그 삽입</h1>
</div>
```

<br/>

사용 예시 2, 사전에 정의된 컴포넌트 전달
```js
const Component = ()=> {
  return React.createElement(
    "h2",
    null,
    "h2 태그 삽입"
  );
};

ReactDOM.render(
  React.createElement(Component, null, null),
  document.querySelector("#root")
);
```
결과물 2
```html
<div id="root">
  <h2>h2 태그 삽입</h2>
</div>
```

<br/>

사용 예시 3, 쿼리 셀렉터 대상으로 직접 삽입
```js
ReactDOM.render(
  React.createElement(
    React.Fragment,
    null,
    "React.Fragment 예시1",
    "React.Fragment 예시2",
    "React.Fragment 예시3",
  ),
  document.querySelector("#root")
);
```
결과물 3
```html
<div id="root">React.Fragment 예시1React.Fragment 예시2React.Fragment 예시3</div>
```

<br/>
<br/>

# **JSX**
`React.createElement()`의 단점을 극복하고자 나온 문법이 JSX이다.  

JSX는 HTML의 **태그 트리 구조를 JS 내에 그대로 작성**이 가능한 문법이다. 이 코드가 실행될 때는 **Babel**의 해석을 거쳐 `React.createElement()` 를 사용한 문법으로 **자동 변환**된다. 따라서 JSX 문법을 사용하기 위해서는 Babel이 선행되어야 한다.  

아래와 같은 JSX 문법을 사용하여 컴포넌트의 구조를 만들 수 있다.
```js
ReactDOM.render(
  <div className="container">
    <h1>Hello, JSX!</h1>
    <ul>
      <li>Hi</li>
      <li>Hello</li>
    </ul>
  </div>,
  document.querySelector("#root")
);
```

## **문법 규칙**

1. 최상위 요소는 1개여야한다.

2. 최상위 요소를 리턴할 경우 ()로 감싸야한다.

3. 자식들을 바로 렌더링하고 싶을 경우(Fragment) 최상위 요소로 내용이 없는 태그 `<> </>`를 사용한다.

4. JS 표현식(보간법)의 사용은 `{}` 만으로 가능하다. ($ 필요 x)

5. `if`문은 사용할 수 없다.

    - 삼항 연산자 혹은 `&&`을 사용한다.

6. style을 사용하여 CSS 인라인 선언이 가능하다.

7. `className` 으로 클래스 적용이 가능하다.

8. 자식 요소가 있으면 꼭 닫아야하고 닫힌 태그도 `/`를 반드시 입력해야 한다.

<br/>
<br/>

# **Props & State**

Props와 State는 변경이 발생하면 렌더가 다시 일어난다.  

렌더는 `render()` 함수를 통해 이루어지는데, Props 혹은 State가 변경되면 `render()` 함수가 재실행된다.

Props & State는 컴포넌트 정의에서 매우 중요한 부분이다.

- **Props**  
컴포넌트 외부에서 컴포넌트에게 주는 데이터이다.  

- **state**  
컴포넌트 내부에서 변경할 수 있는 데이터이다.


<br/>

## **Props**

### **함수 컴포넌트의 Props**

- **정의**  
컴포넌트 정의 함수의 매개변수로 props를 선언하고,  
반환문에서 표현식을 사용해 props의 프로퍼티를 호출한다.  
해당 프로퍼티에 대한 정의가 아직 되어있지 않지만 우선 호출한다.
    ```js
    export default function Component(props) {
      return <div><h1>{props.message}</h1></div>
    };
    ```

- **사용**  
`render()` 함수 내부에서 컴포넌트를 호출할 때 props의 프로퍼티와 값을 선언/할당한다.
    ```js
    ReactDOM.render(
      <Component message="Hello, world!">,
      document.querySelector("#root")
    );
    ```

- **기본값**  
props는 기본값을 할당할 수 있다.
  ```js
      Component.defaultProps = {
        message: "기본 메세지"
      };
  ```


<br/>

### **클래스 컴포넌트의 Props**
사용은 위 함수 컴포넌트와 동일하다. 정의에서만 약간의 차이가 있다.

- **정의**  
함수와 다르게 매개변수로 props를 정의하는 대신 클래스의 props를 참조하기 때문에 this를 앞에 붙인다.
    ```js
    export default class Component extends React.Component {
      render() {
        return (
          <dvi>
            <h1>
              {this.props.message}
            </h1>
          </dvi>
        );
      };
    };
    ```

- **기본값**  
함수와 같은 방법으로 기본값을 할당할 수 있다.  
클래스는 `static` 키워드를 통해 기본값을 할당할 수도 있다.
    ```js
    class Component extends React.Component {
      render() {
        return (
          <div>
            <h1>
              {this.props.message}
            </h1>
          </div>
        )j
      };
      static defaultProps = {
        message: "기본 메세지"
      };
    };
    ```

<br/>

## **State**
State는 클래스 컴포넌트에서만 사용이 가능하지만 뒤에 나올 Hook을 통해 함수 컴포넌트에서도 사용이 가능하다.

클래스에서 state는 항상 객체로 정의되며, state의 값을 변경하기 위해서는 React에서 정의된 메소드를 거쳐야 한다. 이 내용은 뒤에서 더 자세하게 다룬다. 

두 가지 방법으로 정의가 가능하며 호출은 Props와 동일하게 표현식으로 이루어진다.

- **첫 번째 정의 방법**  

    ```js
    export default class Component extends React.Component {
      state = {
        count: 0
      };
      render() {
        return (
          <dvi>
            <h1>
              {this.state.count}
            </h1>
          </dvi>
        );
      };
    };
    ```

- **두 번째 정의 방법**
생성자 함수를 이용하는 방법이다.  
생성자 함수를 사용하기 위해서는 `extends` 한 `React.Component` 로 부터 props를 상속 받아야 한다.
    ```js
    export default class Component extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          count: 1
        };
      };
      render() {
        return (
          <dvi>
            <h1>
              {this.state.count}
            </h1>
          </dvi>
        );
      };
    };
    ```
  
- **값 변경 방법**
클래스에 아래 메소드를 추가하여 값을 변경할 수 있다.
  ```js
  // 첫 번째 방법,
  // 객체를 통째로 새로 만든다.
  componentDidMount() {
      setTimeout(() => {
        this.setState({
          count: this.state.count + 1
        });
      }, 1000);
    };

  // 두 번째 방법, 
  // 이전 객체를 이어받아서 사용한다.
  componentDidMount() {
      setTimeout(() => {
        this.setState((prevState) => {
          const newState = {count: prevState.count + 1};
          return newState;
        })
      }, 1000);
    };
  // 혹은
  componentDidMount() {
      setTimeout(() => {
        this.setState((prevState) => ({...prevState, count: prevState.count + 1 }));
      }, 1000);
    }
  ```

<br/>

## **children**
children은 props의 일종으로, 부모 컴포넌트가 자식 컴포넌트를 값으로 갖게 된다.  
```html
<container>
  <item />
</container>
```
위와 같은 컴포넌트 트리에서 `container` 는 `{children: "item"}` 이라는 props를 부여받게 된다.  

children은 주로 컴포넌트의 재사용성을 높이기 위해 사용된다. 부모 컴포넌트는 그 내부에서 children 이라는 이름으로 자식 컴포넌트를 호출할 수 있게 된다.

<br/>
<br/>

# **Event Handling**
JSX를 통해서 이벤트를 핸들링할 수 있다.  
이벤트는 props를 통해 지정한다. props의 프로퍼티명이 이벤트와 연결되면 해당 이벤트에 연결되는 방식을 갖는다.

이벤트명은 camelCase로 작성해야하며,  
`onClick`, `onMouseEnter` 와 같이 `on` 뒤에 이벤트명을 붙여서 작성해야 한다.  

프로퍼티의 값으로는 함수가 들어간다.
실제 DOM 요소에만 사용이 가능하며, 컴포넌트에 사용하면 일반 props로 전달된다.

이벤트를 JSX에서 인라인으로 지정하는 방법과 별도의 메소드로 분리하는 방법이 있다.

## **JSX 인라인 방식**
```js
<div>
  <button onClick={() => console.log("Clicked")}>
    Click
  </button>
</div>
```

## **메소드 방식**
이벤트 핸들러를 별도의 메소드로 분리한다.  
분리된 메소드는 JSX 내부에서 props를 통해 호출된다.

메소드 방식은 this의 범위를 컴포넌트 클래스로 바인딩 해야한다. 화살표 함수를 사용하거나 `bind()` 함수를 사용할 수 있다.  

화살표 함수를 사용하는 방법이 더 간단하기 때문에 주로 사용된다.
```js
// 화살표 함수로 바인딩
export default class Component extends React.Component {
  state = {
    count: 0
  };
  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.click}>click</button>
      </div>
    )
  };
  click = () => {
    this.setState({count: this.state.count + 1})
  }
};

// 바인딩 함수
// 생성자 함수 내부에서 바인딩한다.
export default class Component extends React.Component {
  constructor(props) {
    super(props);
    this.click = this.click.bind(this);
  };
  state = {
    count: 0
  };
  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.click}>click</button>
      </div>
    )
  };
  click() {
    this.setState({count: this.state.count + 1})
  };
};
```

<br/>
<br/>

# **Component Lifecycle**
컴포넌트 라이프사이클은 이 컴포넌트가 브라우저에 렌더링되는 순간부터 사라지는 순간까지를 의미한다.  

리액트는 이 라이프사이클의 각 지점을 메소드로 구분해두었다. 이 메소드들을 통해 해당 지점에서 컴포넌트를 제어할 수 있도록 해준다.  

버전 16.3을 기점으로 변화가 있었다. 이 문서에서는 16.3 이전 버전을 기준으로 먼저 설명 후 16.3 이후 변경점에 대해서 다시 소개한다.

<br/>

## **16.3 이전 버전**

### **컴포넌트 생성 및 마운트**
예시
```js
componentWillMount() {
  console.log("will mount");
};
```

- `constructor()`  
컴포넌트 생성, 생성자 함수이다.  

- `componentWillMount()`  
컴포넌트 마운트 직전 

- `render()`  
컴포넌트 마운트  

- `componentDidMount()`  
컴포넌트 마운트 직후

<br/>

### **컴포넌트 업데이트**
예시
```js
shouldComponentUpdate(nextProps, nextState) {
  console.log("should update", nextProps, nextState);
  return false
};
```

- `componentWillReceiveProps`    
  props가 업데이트 될 경우. 
  매개변수로 전달 받을 props를 사용할 수 있다.

- `shouldComponentUpdate`  
  props 혹은 state를 업데이트 한 직후.  
  컴포넌트를 업데이트 해야하는지 결정하며, 불필요한 렌더를 방지할 수 있기 때문에 리액트 애플리케이션의 최적화에서 중요한 부분을 차지한다.  
  매개변수로 전달 받은 props와 state를 사용할 수 있다.  
  `false`를 반환하면 props와 state가 업데이트는 되지만 화면을 다시 렌더링하지는 않는다.  
  `true` 를 반환하면 다시 렌더링한다.

- `componentWillUpdate`  
  props와 state를 업데이트한 후 다시 렌더링하기 직전.  
  이 부분에서는 `setState` 와 같은 함수를 사용하면 안된다.  
  매개변수로 전달 받은 props와 state를 사용할 수 있다. 

- `render`  

- `componentDidUpdate`  
  다시 렌더링한 직후.  
  매개변수로 이전 props와 state를 사용할 수 있다.

<br/>

### **컴포넌트 언마운트**

- `componentWillUnmount` 

<br/>

## **16.3 이후 변경점**

### **요약**
~~`componentWillMount`~~ => `getDerivedStateFromProps`  

~~`componentWillReceiveProps`~~ => `getDerivedStateFromProps`  

~~`componentWillUpdate`~~ => `getSnapshotBeforeUpdate` *(렌더와 실제 출력 사이로 실행 위치 변경)*

`componentDidCatch` 추가


### **세부 내용**
`getDerivedStateFromProps` 메소드는 `static` 키워드를 통해 컴포넌트 클래스의 정적 메소드로 지정해야하며 리턴값이 존재해야 한다. 이 리턴값은 state의 값을 변경한다.   
이 메소드는 `render()` 가 실행될 상황이라면 무조건 호출된다고 볼 수 있다.    
따라서 다른 라이프사이클에서 props와 state가 업데이트 되어 `render()` 가 재실행된다 해도 이 메소드가 특정 props와 state 값을 반환하고 있다면 해당 값으로 렌더된다.  
매개변수로 nextProps, prevState 를 사용할 수 있다.  
특수한 경우에만 주로 사용된다.

`getDerivedStateFromProps` 사용 예시
```js
static getDerivedStateFromProps(nextProps, prevState) {
  console.log("getDerived", nextProps, prevState);
  return {
    age: 24
  };
};
```

<br/>

`getSnapshotBeforeUpdate` 의 리턴값은 `componentDidUpdate` 에서 세번째 매개변수로 사용할 수 있다.  
렌더 전/후의 상황을 연결할 때 사용할 수 있다.

`getSnapshotBeforeUpdate` 사용 예시  
```js
// DOM에 지속적으로 내용이 추가되며 스크롤이 늘어날 때, 스크롤을 가장 최하단으로 유지하기.
let el = 0;

export default class Component extends React.Component {
  state = {list: []};
  
  render() {
    return (
      <div id="list" style={{height: 100, overflow: "scroll" }}>
        {this.state.list.map(el => {
          return <div>{el}</div>;
        })}
      </div>
    )
  };

  componentDidMount() {
    setInterval(() => {
      this.setState((state) => ({
        list: [...state.list, el++]
      }))
    }, 1000)
  };

  getSnapshotBeforeUpdate(prevProps, prevState) {
    if (prevState.list.length === this.state.list.length) return null
    const list = document.querySelector("#list");
    return list.scrollHeight - list.scrollTop;
  };

  componentDidUpdate(prevProps, prevState, snapshot) {
    console.log(snapshot);
    if (snapshot === null) return;
    const list = document.querySelector("#list");
    list.scrollTop = list.scrollHeight - snapshot;
  };
};
```

<br/>

`componentDidCatch`

에러 발생 시 전체 웹사이트가 마비되는 문제를 해결하기 위해 등장한 라이프 사이클이다.  

컴포넌트의 에러 체크를 담당하는 라이프 사이클로, 이 라이프 사이클에서 에러를 감지했을 경우 대체 컴포넌트(에러 안내 페이지 등)를 출력하도록 하는 등 예상치 못한 에러에 대응이 가능하다.  

에러를 체크할 컴포넌트는 트리 최상위일 것을 권장한다. 자기 자신에게서 발생한 에러는 감지하지 못한다는 단점이 있지만 대신 모든 하위 컴포넌트들의 에러를 한 번에 감지할 수 있기 때문이다.

`componentDidCatch` 사용 예시  
```js
export default class Component extends React.Component {
  state = {
    hasError: false
  };
  render() {
    if (this.state.hasError) {
      return (
        <div>Error</div>
      )
    }
    return (
      <div><RealComponent /></div>
    )
  };
  componentDidCatch(error, info) {
    this.setState({hasError: true});
  };
};
```

<br/>
<br/>

# **React Router**

- **기존의 웹 라우팅 과정**

  1. 서버에 "/" 경로 요청  
  2. 클라이언트로 "/" 에 해당하는 페이지 전송  
  3. "/" 페이지 출력
  4. 서버에 다른 경로 요청  
  5. 클라이언트로 해당하는 페이지 전송

<br/>

- **SPA 라우팅 과정**

  1. 서버에 "/" 경로 요청  
  2. 클라이언트로 React App 전송   
  3. React App은 요청 받은 "/" 경로에 해당하는 컴포넌트를 브라우저에 출력   
  4. 다른 페이지로 이동할 경우 서버에 별도의 요청 없이 React App에서 해당 경로의 컴포넌트 출력 

<br/>

SPA 라우팅을 위해서는 별도의 패키지를 설치해야한다. SPA 라우팅을 구현하는 패키지는 여러가지 있지만 react-router-dom 이 가장 대표적이다.  

라우팅 패키지는 CRA에 포함되어 있지 않아서 별도로 설치해야한다.

`npm i react-router-dom`

<br/>

## **기본 문법**
```js
import {BrowseRouter, Route} from "react-router-dom"
```

1. 각 페이지에 해당하는 컴포넌트 작성 

2. `Route` 컴포넌트에서 각 페이지에 해당하는 경로와 컴포넌트 지정  

3. `Route` 컴포넌트들을 `BrowserRouter` 컴포넌트로 감싼다.  

4. 브라우저의 요청 경로에 `Route` 의 경로가 포함되면 해당 컴포넌트를 출력한다.

```js
import {BrowserRouter, Route} from "react-router-dom";
import Home from "./home.js";
import Login from "./login.js";
import Profile from "./profile.js";

export default App() {
  return (
    <BrowserRouter>
      <Route path="/" component={Home}>Home page</Route>
      <Route path="/login" component={Login}>Login page</Route>
      <Route path="/profile" component={Profile}>Profile page</Route>
    </BrowserRouter>
  );
};
```
### **`exact`**

위 예시는 브라우저에서 요청한 주소에 "/" 이 포함되어 있으면 `Home` 컴포넌트를,  
"/login" 이 포함되어 있으면 `Login` 컴포넌트를,  
"/profile" 이 포함되어 있으면 `Profile` 컴포넌트를 출력하게 된다.  

이 때 "/login" 과 "/profile" 은 모두 "/" 도 포함하고 있기 때문에 `Home` 컴포넌트도 함께 출력된다.  

만약 위처럼 포함되는 경로가 아닌 완벽히 일치하는 경우에만 컴포넌트를 출력하고 싶다면 `Route` 컴포넌트에 `exact` 속성을 추가하면 된다.  

```js
<Route path="/" exact component={Home}> Home page </Route>
```

<br/>

## **Dynamic Routing**
url을 통해 특정 파라미터를 받는 등의 동적 url에 대응하기 위한 동적 라우팅 방법이다.

`Route` 컴포넌트의 `path` 의 값에 `:` 를 붙이고 파라미터를 정의할 수 있다.  
이 때 파라미터가 없는 기존의 `Route` 도 유지한다.

이 후 브라우저에서 경로 뒤에 파라미터 값을 붙여서 요청해도 실제 출력되는 페이지는 기존의 페이지이며, 파라미터 값은 컴포넌트의 `props.match.params`에 `string`으로 저장되어 참조가 가능하다.  

ex)  
1. `path="/profile/:id"` 정의.

2. 브라우저에서 "/profile/123" 페이지 요청.  

3. 실제 로드되는 페이지는 "/profile" 이며, "123" 은 `props.match.param.id` 에 저장.

<br/>

```js
// url 파라미터 id의 값을 변수 id에 저장.
// id가 있을 경우 id도 출력
export default function Profile(props) {
  const id = props.match.params.id;
  return (
  <div>
    <h2>Profile page</h2>
    {id && <span>{id}</span>}
  </div>
  );
}
```

```js
// 기본 profile 페이지와 파라미터 id를 정의한 profile 페이지를 각각 만든다.
// 파라미터 id의 값은 props.match.params.id 에 저장된다.
// ex) "/profile/123", props.match.params.id == 123
import Profile from "./profile.js";

<BrowserRouter>
  <Route path="/profile" exact component={Profile}></Route>
  <Route path="/profile/:id" component={Profile}></Route>
</BrowserRouter>
```

<br/>

## **Query string**
쿼리 스트링도 동적 라우팅의 일종이다.

쿼리 스트링의 가장 큰 특징은 별도의 `Route` 컴포넌트를 추가하지 않아도 쿼리 스트링 url을 통해 해당 페이지에 접근이 가능하다는 점이다.  
일반적인 동적 라우팅과는 달리 파라미터를 정의한 별도의 `Route`를 추가할 필요가 없다.

쿼리스트링은 간단하게 url에 `?` 를 붙여서 key=value 쌍으로 작성할 수 있다.  
ex) "/about?name=rarebeef"

url로 전송한 `?name=rarebeef` 는 컴포넌트의 `props.location.search` 에 `string`으로 저장된다.  

별도의 사전 세팅 없이도 저장은 자동으로 되니 해당 값을 참조하여 사용하는 방법만 알면 된다.

<br/>

### **쿼리 스트링 값 참조**  

쿼리 스트링 값은 컴포넌트의 `props.location.search` 에 `"?key=value"` 형태의 `string` 덩어리로 저장된다. 따라서 이 덩어리를 key와 value로 구분하여 가공할 필요가 있다.

- **URLSearchParams**  

  첫 번째는 `URLSearchParams` 라는 브라우저 내장 객체를 사용하는 방법이다. 브라우저 내장 객체이기 때문에 브라우저에 따라서 지원하지 않을 수 있다. IE는 버전에 상관 없이 지원하지 않는다.

  ```js
  export default function About(props) {
    const serchParams = props.location.search;  // "?key=value"
    const obj = new URLSearchParams(serchParams);
    console.log(obj.get("key")); // value
    return <div>About</div>;
  }
  ```

- **query-string 패키지**  

두 번째는 query-string 패키지를 사용하는 방법이다.  
`$ npm i query-string -S`
```js
import queryString from "query-string"
```

패키지를 `import` 하고 `queryStirng.parse()` 메소드를 사용하면 쿼리 스트링을` {key: value}` 형태로 파싱해준다.

```js
import queryString from "query-string";

export default function About(props) {
  const serchParams = props.location.search;  // "?key=value"
  const query = queryString.parse(serchParams); 
  console.log(query); // {key: value}
  return (
    <div>
      <h2>About page</h2>
      {query.name && <span>{query.name}</span>}
    </div>
  );
}
```

<br/>

## **Switch & NotFound**
```js
import {Switch} from "react-router-dom"
```
`Switch` 는 react-router-dom 에서 지원하는 컴포넌트이다.  

`Switch` 는 여러 `Route` 중 순서대로 먼저 맞는 **하나의 컴포넌트만 출력**하며, 따라서 `exact`를 사용하지 않는 로직을 만들 수 있다.

또한 어느 `path` 에도 해당하지 않을 경우 보여지는 컴포넌트를 지정하여 Not Found 페이지를 만들 수 있다. 가장 마지막에 `Route` 컴포넌트를 추가하고 `path`를 지정하지 않으면 된다.  
이 경우 루트 경로인 "/"는 `exact` 를 붙여야 한다. 모든 경로는 루트 경로를 포함하기 때문이다.

가장 위 `Route` 부터 순차적으로 비교해 먼저 맞는 컴포넌트를 출력하기 때문에 가장 범위가 넓고 포괄적인 경로의 `Route` 를 아래쪽에 배치하고 좁은 범위의 경로를 갖는 `Route` 를 위쪽에 배치할 필요가 있다.

```js
import {BrowserRouter, Route, Switch} from "react-router-dom"
import Home from "./pages/home"
import Profile from "./pages/profile"
import About from "./pages/about"
import NotFound from "./pages/notFound"

export default function App() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/profile/:id" component={Profile}></Route>
        <Route path="/profile" component={Profile}></Route>
        <Route path="/about" component={About}></Route>
        <Route path="/" exact component={Home}></Route>
        <Route component={NotFound}></Route>
      </Switch>
    </BrowserRouter>
  );
}
```

<br/>

## **링크**  
```js
import {Link} from "react-router-dom"
```
react-routing을 사용할 때 `<a>` 태그를 사용하여 페이지를 이동할 경우 리액트 앱 전체를 다시 로드하게 된다.  

따라서 react-router-dom 에서 지원하는 `Link` 컴포넌트를 통해 페이지를 이동하도록 해야한다.

`Link` 컴포넌트는 `to` props로 경로를 지정하게 된다.

```js
import { Link } from "react-router-dom";

export default function Links() {
  return (
    <ul>
      <li>
        <Link to="/">Home</Link>
      </li>
      <li>
        <Link to="/profile">Profile</Link>
      </li>
      <li>
        <Link to="/profile/1">Profile/1</Link>
      </li>
      <li>
        <Link to="/about">About</Link>
      </li>
      <li>
        <Link to="/about?name=rarebeef">About?name=rarebeef</Link>
      </li>
    </ul>
  );
};
```

<br/>

## **NavLink**
```js
import {NavLink} from "react-router-dom"
```
NavLink는 active 상태에 대한 클래스, 스타일 등의 다양한 지정이 가능하다.  

```js
import { NavLink } from "react-router-dom";

const activeStyle = { color: "green" };

export default function NavLinks() {
  return (
    <ul>
      <li>
        <NavLink to="/" exact activeStyle={activeStyle}>
          Home
        </NavLink>
      </li>
      <li>
        <NavLink to="/profile" exact activeStyle={activeStyle}>
          Profile
        </NavLink>
      </li>
      <li>
        <NavLink to="/profile/1" activeStyle={activeStyle}>
          Profile/1
        </NavLink>
      </li>
      <li>
        <NavLink
          to="/about"
          activeStyle={activeStyle}
          isActive={(match, location) => {
            return match !== null && location.search === "";
          }}
        >
          About
        </NavLink>
      </li>
      <li>
        <NavLink
          to="/about?name=rarebeef"
          activeStyle={activeStyle}
          isActive={(match, location) => {
            return match !== null && location.search === "?name=rarebeef";
          }}
        >
          About?name=rarebeef
        </NavLink>
      </li>
    </ul>
  );
}
```
`activeStyle` 로 액티브 상태의 스타일을 지정할 수 있다.  
`path` 처럼 동작하기 때문에 겹치는 경로에 대해서는 `exact` 를 붙여서 제어할 필요가 있다.  

또한 쿼리 스트링의 경우 실제 경로 상으로는 `?` 뒤 내용은 없는 것이나 다름 없기 때문에 `exact` 여부에 상관 없이 전부 active 상태가 된다.  
따라서 `isActive={}` 를 사용하여 액티브 상태를 별도로 제어해야 한다.  
`isActive={}` 는 값으로 함수가 들어가는데, 반환값이 true면 Active, false면 Deactive 상태가 된다.  
함수의 인자로 `match`, `location`의 `props`를 받을 수 있다. 이 두 `props`는 react-router-dom 의 컴포넌트가 기본으로 갖는 `props`이다. 이 `props`들의 상태를 비교하여 액티브 여부를 제어하면 된다.  

쿼리 스트링이 저장되는 `location.search` 를 통해 쿼리 스트링의 존재 여부를 파악할 수 있다.  

`match !== null` 을 비교하는 이유는 경로가 "/about" 일 때만 적용하기 위함이다. 해당 부분을 삭제하면 경로가 "/profile?name=rarebeef" 일 때도 액티브된다.

<br/>

## **JS로 라우팅 이동**
JS 코드로 라우팅을 이동할 때도 SPA의 이점을 살리기 위해서는 이동 방식에 유의해야 한다.  

컴포넌트의 `props.history` 에 url을 `push` 하여 페이지를 이동하는 방법을 사용할 수 있다.
```js
export default function HomeButton(props) {
  return <button onClick={home}>Home</button>;
  function home() {
      props.history.push("/");
  }
}
```

위 예시의 `HomeButton` 컴포넌트를 다른 컴포넌트에 `import` 해서 사용할 경우 인자 props를 제대로 전달받지 못해서 에러가 발생한다.  

### **props 전달**

`<button {... props}></button>` 을 추가하여 반환하는 `button` 컴포넌트에 props를 전달할 수 있지만 컴포넌트의 중첩이 발생할 때 마다 반복해서 작성해야하기 때문에 여러모로 불편하다.

react-router-dom의 `withRouter` 를 사용하면 이러한 문제를 해결할 수 있다. 컴포넌트 생성 함수 전체를 `withRouter()`로 감싸서 사용한다.  

이렇게 하면 다른 컴포넌트에서 `HomeButton` 컴포넌트를 `import` 해도 props가 함께 전달되어 정상적을 작동한다.

A 컴포넌트에서 B 컴포넌트를 호출했을 때 B를 A와 연결하고 props 등의 데이터를 전달해 사용하도록 하는 정도로 일단 이해하면 되며, `withRouter()` 에 대한 내용은 뒤에서 다룬다.

```js
import {withRouter} from "react-router-dom";

export default withRouter(function HomeButton(props) {
  return <button onClick={home}>Home</button>;
  function home() {
      props.history.push("/");
  }
});
```

<br/>

## **Redirect**
```js
import {Redirect} from "react-router-dom";
```

`Redirect` 는 react-router-dom 에서 지원하는 컴포넌트이다. `Redirect` 는 로드되면 `to=""` 가 가리키는 경로로 페이지를 이동시킨다.  

로그인 페이지를 요청했을 때 이미 로그인 된 상태면 홈 페이지를, 로그인이 안 된 상태면 로그인 페이지를 띄우도록 하는 등의 로직에서 사용이 가능하다.  

이 때 `Route` 컴포넌트에서 `component` props 대신 `render` props를 통해서 삼항 연산자를 작성할 수 있다.

```js
let isLogin = true
function App() {
  return (
    <BrowserRouter>
      <Route 
        path="/login" 
        render={() => (isLogin ? <Redirect to="/"> : <Login />)}
      />
    </BrowserRouter>
  );
};
```

<br/>
<br/>

# **style-loader**
CRA의 스타일은 Webpack을 통한 style-loader로 이루어지게 된다.  
이 때 스타일이 로드되는 방법으로 크게 두 가지가 존재한다.

- ~.css  

- ~.module.css  

이는 css 외에 sass, scss 등도 마찬가지이다.  

CRA에서는 모듈 하나만 설치하면 간단하게 sass와 scss를 사용할 수 있다.

`$ npm i sass`

<br/>

## **.css**
.css, 혹은 .scss 등의 파일을 불러오는 방법은 다음과 같다.  

```js
import "./App.css";
```

이러한 방법으로 css 파일을 불러오는 것은 매우 간단하면서도 컴포넌트 구분 없이 앱 전역에 덮어 쓰여질 수 있다는 위험성이 있다.  

따라서 이러한 .css 로드 방식을 사용할 때는 클래스의 작명에 신경쓰고 선택자의 구분을 확실히 하는 것이 중요하다.

<br/>

## **.module.css**
.module.css, 혹은 .module.scss 등의 확장자를 갖는 파일을 불러오는 방법은 아래와 같다.  

```js
import styles from "./App.module.css";
```

이러한 방식의 스타일 로드는 컴파일을 거치며 선택자가 `앱이름_클래스명__해시값` 으로 변경된다.
```scss
/* 컴파일 전 */
.nav {
  li {
    background-color: red;
  }
}

/* 컴파일 후 */
.NavList_nav__U_BBE {
  li {
    background-color: red;
  }
}
```
이 클래스 명은 `styles` 객체에 아래와 같은 형태로 저장된다.  
```js
styles = {nav: "NavList_nav__U_BBE"};
```
따라서 JSX 작성 시 클래스 이름을 다음과 같이 명시해야 스타일이 적용된다.  

```js
import styles from "Nav.module.scss"

export default function Nav() {
  return (
    <ul className={styles["nav"]}>
      <li>Hi</li>
    </ul>
  );
};
```

<br/>

## **state 값에 따른 class 변경**
state 값이 변함에 따라 class를 변경하여 스타일에 변화를 줄 수 있다.

```js
// 버튼을 클릭하면 `state.loading` 의 boolean 값을 토글
// `true` 일 경우 버튼에 `.loading` 클래스 추가

import React from "react";
import styles from "./Button.module.scss";

export default class Button extends React.Component {
  state = {
    loading: false,
  };
  render() {
    return (
      <button
        className={
          this.state.loading
            ? `${styles["button"]} ${styles["loading"]}`
            : styles["button"]
        }
        onClick={this.loading}
      >
        Button
      </button>
    );
  }
  loading = () => {
    this.setState((prevState) => {
      return { loading: !prevState.loading };
    });
    console.log(this.state.loading);
  };
}
```
복수의 클래스를 사용할 경우 띄어쓰기로 구분해야 하기 때문에 보간법과 표현식을 사용하여 클래스 사이에 띄어쓰기를 삽입하였고 삼항 연산자를 통해 클래스를 제어하였다. 

<br/>

### **classnames**
**classnames** 패키지를 사용하면 위 로직을 조금 더 간단하게 만들 수 있다.

`$ npm i classnames`

classnames 패키지는 `className()` 라는 함수를 갖고 있다.  
이 함수는 개수에 상관 없이 전달 받은 인자를 띄어쓰기로 구분한 문자열로 반환한다.  
또한 인자가 truthy일 경우 반환하고 falsy일 경우 반환하지 않는 특징을 갖고 있다.  

ex)  
```js
console.log(
  className("A", "B", {C: true}, {D: false}, "", 0, 1, null)
);
// A B C 1
```

이러한 특징을 활용하여 아래와 같이 `state.loading` 이 true일 경우민 `styles["loading"]` 클래스를 추가하도록 할 수 있다.

```jsx
import classNames from "classnames"
import styles from "./Button.module.scss"
// 생략

<button
  className={
    classNames(
      styles["button"], 
      this.state.loading && styles["loading"]
  )} 
  onClick={this.click}
>
  Button
</button>

// 생략
```

혹은 classNames 패키지의 경로에 `/bind` 를 붙여서 `import` 하고 `styles` 와 바인딩하면 클래스명을 `style["class"]` 가 아닌 `"class"`로 작성할 수 있게 된다.

또한 아래 예시와 같이 `state.loading`을 `loading`에 비구조화 할당하여 사용할 수도 있다.

```jsx
import classNames from "classnames/bind"

const cx = classNames.bind(styles);

// 생략
render() {
  const { loading } = this.state;
  return (
    <button
      className={cx("button", { loading })}
      onClick={this.click}
    >
      Button
    </button>
  );
}

// 생략
```

<br/>
<br/>

# **Styled Components**
Styled Components 방식으로 스타일을 적용할 수 있다.  

`$ npm i styled-components`


```js
const 이름 = styled.요소``
```

위와 같은 코드를 통해 styled components 를 만들 수 있다.  

위 코드의 요소 부분에는 html의 요소(태그명)가 들어가게 되고, 해당 태그로 컴포넌트가 구현된다.  

그 뒤의 백틱 \`\` 안에는 스타일 선언문을 작성할 수 있다.  

가상 클래스의 스타일 또한 선언이 가능하다.

```js
import styled from "styled-components";

const StyledButton = styled.button`
  color: black;

  :hover {
    color: white;
  }
`;

export default StyledButton;
```

이 방식으로 작성한 컴포넌트는 클래스가 랜덤값으로 자동 생성된다.  
또한 스타일 선언문에서 오류가 감지되지 않기 때문에 오타 등에 주의하며 작성해야 한다.

<br/>

## **Styled Components Props 스타일**
같은 styled components여도 props에 따라 스타일을 다르게 부여할 수 있다.   

스타일을 선언하는 백틱 내부에서 표현식을 통해 JS 코드를 작성할 수 있는데, 이 코드를 통해 props를 받아와서 처리하게 된다. 이 때 표현식 내부의 JS 코드는 항상 함수여야 한다.  

인자로 props를 전달하고 함수 내부에서 논리 연산자를 통해 좌항은 특정 prop을, 우항은 다시 백틱을 이용한 스타일 선언을 작성하여 특정 prop이 존재할 경우 해당 스타일을 적용할 수 있다.

```js
import styled from "styled-components";

const StyledButton = styled.button`
  background-color: pink;
  ${props => props.blue && `
    background-color: blue;
  `}
`;
```

또한 props로 값을 전달 받아서 스타일에 적용할 수도 있다.  
마찬가지로 스타일 선언문에서 표현식을 통해 props를 전달 받아서 처리하게 된다.  
논리 연산자 `||` 로 props가 없을 경우 기본값을 지정할 수 있다.
```js
const StyledButton = Styled.button`
  background-color: ${props => props.color || "pink"};
`
```

<br/>

## **Styled Components 복제**
```js
const RedStyledButton = styled(StyledButton)`
  background-color: red;
`;
```
위와 같이 `styled()` 함수로 styled component를 불러온 뒤 변수에 할당하여 기존의 컴포넌트를 복제할 수 있다. 이 복제한 컴포넌트에 스타일을 덮어쓰는 것도 가능하다.

<br/>

## **Styled Components 태그 변경**
```js
<StyledButton as="a" href="javascript:void(0)">Button</StyledButton>
```
`as=""` props에 원하는 태그명을 입력하여 컴포넌트의 태그를 변경할 수 있다.  

또한 태그명이 아닌 다른 styled components를 전달할 수도 있다.  
`as={StyledComponent}`   
이 경우 전달 받은 컴포넌트의 스타일을 불러와서 사용하게 된다.  

<br/>

## **Styled Components 전역 스타일**
Styled Component를 사용하면 각각의 컴포넌트에 개별적으로 스타일을 선언하기 때문에 스타일이 뒤섞여서 엉망이 되는 일을 방지할 수 있다.  

하지만 이런 장점은 전역적으로 스타일을 적용해야 할 경우 큰 단점으로 다가오기도 한다. 다행히 styled-component는 전역 스타일 선언에 대한 기능도 제공하고 있다.  

```js
const GlobalStyle = createGlobalStyle`
  button {
    border-color: purple;
  }
`;

// 생략

return (
  <div>
    <GlobalStyle />
    <StyledButton />
  </div>
);
```

`creactGlobalStyle` 을 통해서 전역 스타일을 선언하고, 이 전역 스타일을 컴포넌트들과 함께 반환하면 된다.

<br />

## **Styled Components 속성 기본값**
`attrs()` 로 styled components로 만든 컴포넌트에 적용할 기본값 속성을 지정할 수 있다. 인자로 함수를 전달하고 이 함수는 객체를 반환한다.  


이 방법을 사용하면 매 번 styled components를 호출할 때 마다 같은 속성을 여러번 지정하지 않아도 된다.  

```js
const StyledA = styled.a.attrs((props) => ({
  target: "_blank",
  href: props.href || "https://naver.com"
}))`
  color: ${(props) => props.color};
`;
```

<br/>
<br/>

# **React Shadow**
`$ npm i react-shadow`

react-shadow 를 이용하여 쉐도우 돔을 만들 수 있다.  
쉐도우 돔은 다른 돔들과 분리되어 자신만의 영역을 갖고 있다. 따라서 다른 돔들에 스타일의 간섭을 주거나 받지 않기 때문에 컴포넌트 단위의 스타일 선언에 유용하다.

react-shadow 로 쉐도우 돔을 만드는 방법은 간단하다. 해당 컴포넌트의 돔 트리를 `<root.div>` 태그로 감싸면 된다.  

스타일을 적용하고 싶다면 쉐도우 돔 트리 구조에 스타일을 삽입하는 방법을 사용할 수 있다.

완벽하게 외부와 차단된 돔이기 때문에 전역 스타일을 적용 받지 못하는 것과 스타일 외에도 다양한 데이터들을 전달하지 못하는 등 장점과 단점이 뚜렷하다.

```js
import root from "react-shadow";

const styles = `
  color: red;
`;

function App() {
  return (
    <root.div>
      <h1>Hello</h1>
      <style type="text/css">{styles}</style>
    <root.div>
  );
};
```

<br/>
<br/>

# **Ant Design**
`$ npm i antd`

<a href="https://ant.design/"> Ant Design </a>

Ant Design은 이미 디자인 되어있는 여러 컴포넌트들을 제공해주는 패키지이다.  

사용하기 이전에 Ant Design의 css 파일을 최상위 JS(진입점)에서 다른 스타일보다 먼저 import 해야한다. 

```js
import "antd/dist/antd.css";
```

다만 위 방법은 모든 컴포넌트에 대한 css를 모두 import하기 때문에 효율적이지는 않다. 아래의 방법으로 내가 사용할 컴포넌트에 대한 내용만 import 할 수 있다.

```js
import Checkbox from 'antd/es/checkbox';
import 'antd/es/checkbox/style/css';
```

Ant Design 홈페이지에서 다양한 컴포넌트들을 확인해볼 수 있다. 맘에 드는 컴포넌트를 import 하기만 하면 바로 사용이 가능하다.
```js
import Checkbox from 'antd/es/checkbox';
import 'antd/es/checkbox/style/css';

function App() {
  return (
    <div>
      <Checkbox>체크박스</Checkbox>
    </div>
  );
};
```

<br/>

Ant Design은 다양한 아이콘도 제공하고 있다.  
아이콘을 사용하기 위해서는 별도로 패키지를 설치해야한다.  

`$ npm i @ant-design/icons`

<br/>

Ant Design 처럼 컴포넌트를 제공하는 패키지를 사용할 때 가장 중요한 점은 해당 컴포넌트의 API, 활용할 수 있는 Props를 체크하는 것이다.

<br/>

## **Ant Desing 레이아웃**
```js
import Row from "antd/es/row"; import "antd/es/row/style/css";
import Col from "antd/es/col"; import "antd/es/col/style/css"

const colStyle = () => ({
  backgroundColor: "red"
});

function App() {
  return (
    <div>
      <Row gutter={16} justify="center">
        <Col span={24} style={colStyle()} />
      </Row>
      <Row gutter={24}>
        <Col span={10} style={colStyle()} />
        <Col span={10} offset={4} style={colStyle()} />
      </Row>
      <Row gutter={32}>
        <Col span={8} style={colStyle()} />
        <Col span={8} style={colStyle()} />
        <Col span={8} style={colStyle()} />
      </Row>
    </div>
  );
};
```

하나의 `Row`는 24의 길이를 갖는다.  
`Col`의 props인 `span`은 `Col`의 길이를 의미하며,  
하나의 `Row` 안에 있는 모든 `Col`의 `span` 총합은 24가 되어야 한다.  

`offset` 은 총 길이 24 중 건너 뛰고 싶은 길이를 의미한다. `offset`이 부여된 `Col`은 그 값만큼 앞의 공간을 비우게 된다.

`Row`는 `gutter` 라는 props를 갖을 수 있는데, 이는 `Col` 사이의 간격을 의미한다. `gutter`의 값은 8을 제외한 8의 배수로 부여할 수 있다.  

`Row` 에 `justify` 와 `align`을 부여하여 각각 좌우와 상하 정렬을 지정할 수 있다. 가용값으로는 start, center, end, space-between, space-around, top, middle, bottom 등이 있다.

<br/>
<br/>

# **HOC**

**Higher Order Component**  

HOC는 기존의 컴포넌트를 인자로 받아서 새로운 컴포넌트로 반환하는 함수이다. Hooks의 등장으로 사용 빈도가 낮아졌다. 

```js
HOC = function(컴포넌트) { return 새 컴포넌트 }
```

앞서 살펴본 `withRouter()` 도 HOC의 일종이다.


**HOC의 주의점 & 특징**

1. `render()` 내부에서 사용하지 말 것

2. 정적 메소드는 복사되지 않기 때문에 직접 복사해야 한다.  

    - 메소드의 복사는 `$ npm i hoist-non-react-statics` 패키지를 활용.

3. 반환 시 기존의 props도 함께 전달된다.

4. 디버깅을 위해 아래와 같이 어떤 HOC를 통해 복제된 컴포넌트인지 이름을 구분할 것.
    ```js
    반환할컴포넌트.displayName = `HOC명(${기존컴포넌트.name})`
    ```




<br/>
<br/>

# **Controlled & Uncontrolled Component**

상태를 갖고 있는 대표적인 HTML 엘리먼트는 `input`이다.  
input은 현재 자신에게 입력되고 있는 정보를 상태로 갖게 된다.

엘리먼트를 소유하고 있는 컴포넌트가 해당 엘리먼트의 상태를 관리할 경우 Controlled Component, 컴포넌트가 엘리먼트의 상태를 관리하지 않고 참조만 하는 경우 Uncontrolled Component 라고 말한다.

<br/>

## **Controlled Component**  

(컴포넌트의 state == 엘리먼트의 상태) 구조를 만들고 state를 통해 엘리먼트의 상태를 관리할 수 있다.

<br/>

**input의 상태 관리 예시**  
input에 입력이 발생하면 그 값을 받아서 state에 저장하고 이 state를 input의 value에 전달한다. 이 과정에서 state가 변하기 때문에 렌더가 재실행되고 input에 입력 값이 출력되는 것을 볼 수 있다.  

input에 입력된 값을 참조할 때도 굳이 input에서 값을 꺼내는 것이 아닌 컴포넌트의 state에서 참조하면 된다. 
```js
export default class Controlled extends React.Component {
  state = {
    value: "",
  };
  render() {
    return (
      <div>
        <form>
          <input value={this.state.value} onChange={this.change} />
          <button onClick={this.click}>출력</button>
        </form>
      </div>
    );
  }

  change = (event) => {
    this.setState({ value: event.target.value });
  };

  click = () => {
    console.log(this.state.value);
  };
}
```

<Br/>

## **Uncontrolled Component**

**input의 상태 참조 예시**  

예시에서 `input`은 버츄얼이 아닌 실제 돔이기 때문에 직접 value 값을 꺼내서 참조할 수 있다. 다만 React에서는 이처럼 실제 돔에 직접 접근하는 방식을 권장하지 않는다.

```js
export default class Uncontrolled extends React.Component {
  render() {
    return (
      <div>
        <input id="input" />
        <button onClick={this.click}>출력</button>
      </div>
    );
  }

  click = () => {
    const input = document.querySelector("#input");
    console.log(input.value);
  };
}
```

**레퍼런스를 이용한 input의 상태 참조 예시**  
리액트는 실제 돔 엘리먼트의 상태를 참조할 때 레퍼런스를 이용하는 것을 권장한다.  

리액트 레퍼런스를 하나 생성하고 엘리먼트와 연결하는데,  
이 레퍼런스는 엘리먼트에 대한 데이터를 갖고 있으며 마음껏 참조가 가능하다.

```js
export default class Uncontrolled extends React.Component {
  inputRef = React.createRef();
  render() {
    return (
      <div>
        <input ref={this.inputRef}/>
        <button onClick={this.click}>출력</button>
      </div>
    );
  }

  click = () => {
    console.log(this.inputRef.current.value);
  };
}
```

<br/>
<br/>

# **Hooks**

리액트 16.8 버전부터 등장한 기능으로, Hooks 를 사용하면 function 컴포넌트에서 state를 다루고 state 관련 로직을 재사용 할 수 있다. HOC를 대체할 수 있는 기능이다.

기본 훅은 3가지 종류가 존재한다.  

- `useState`
- `useEffect`
- `useContext` (뒤에 나올 Context 챕터에서 다룬다.)

<br/>

## **useState**
`useState()` 를 통해 함수 컴포넌트에서 state를 정의하고 값을 변경해줄 수 있다.

```js
const [state명, state처리함수명] = React.useState(초기값);
```

```js
export function FunctionState() {

  const [count, setCount] = React.useState(0);  // state 정의, count에 초기값 0 할당.

  return (
    <div>
      <h1>Function State</h1>
      <span>{count}</span>
      <button onClick={click}>클릭</button>
    </div>
  )

  function click() {
    setCount(count + 1);  // state 처리 로직
  };
};
```

count에 값을 부여하는 방법이 아닌 `{count: 0}` 자체를 `useState()`에 사용할 수도 있다.

```js
export function FunctionState2() {
  const [state, setState] = React.useState({ count: 0 });  // state에 {count: 0} 할당. 처리함수도 setState로 변경.

  return (
    <div>
      <h1>Function State</h1>
      <span>{state.count}</span>      // 호출도 state.count 형태로 이루어진다.
      <button onClick={click}>클릭</button>
    </div>
  );

  // state 처리 함수. 
  // 아래처럼 인자로 기존의 state를 불러와서 처리하는 방식을 권장한다.
  function click() {
    setState((state) => ({
      count: state.count + 1,
    }));
  }
}
```

<br/>

## **useEffect**
`useEffect`는 componentDidMount, componentDidUpdate, componentWillUnmount 의 라이프 사이클 훅을 대체할 수 있다.

```js
React.useEffect(함수, 배열);
```

### **componentDidMount, componentDidUpdate**
첫번째 매개변수인 함수는 해당 라이프 사이클에 실행할 로직이다.  

두번째 매개변수인 배열은 선택 사항으로, 첫번째 인자인 함수가 실행되는 조건을 지정한다.  

배열 안의 요소로 인해 컴포넌트가 업데이트 될 때만 함수가 실행된다. 따라서 빈 배열을 전달할 시 마운트 직후 & 언마운트 직전에만 실행된다. 두번째 매개변수를 아예 전달하지 않으면 업데이트 시 항상 실행된다.

```js
export function FunctionUseEffect() {
  const [state, setState] = React.useState({ count: 0 });

  React.useEffect(() => {
    console.log(
      "componentDidMount & componenetDidUpdate by count",
      state.count
    );
  }, [state.count]);

  return (
    <div>
      <h1>Function useEffect</h1>
      <span>{state.count}</span>
      <button onClick={click}>클릭</button>
    </div>
  );
  
  function click() {
    setState((state) => ({ count: state.count + 1 }));
  }
}
```

### **componentWillUnmount**
componentWillUnmount 에 실행될 함수는 cleanup으로 전달한다.  
cleanup은 함수가 함수를 반환하는 방법을 사용한다.

함수 A가 함수 B를 반환할 경우,  
B함수는 다음 차례에 A함수가 다시 호출되면 가장 먼저 실행되고 그 이후에 A함수의 로직이 실행된다.

```js
function A() {
  console.log("A");
  return () => {console.log("B")};
};

// 최초 함수 A 호출
// =>  "A" 출력
// =>  함수 A 재호출
// =>  "B" 출력
// => "A" 출력
```

따라서 `useEffect()` 로 componentWillUnmount를 제어할 때는 두번째 인자로 빈 배열을 전달하여 함수가 마운트 직후 & 언마운트 직전에만 실행되도록 한 뒤 cleanup으로 로직을 전달한다. 이렇게 하면 마운트 직후에는 기존 함수의 로직만 실행되고 언마운트 직전에는 cleanup 함수가 먼저 실행된다.

```js
React.useEffect(() => {
  console.log("componentDidMount");

  return () => {
    console.log("cleanup", "componentWillUnmount")
  };

}, []);
```
물론 필요에 따라 componentDidUpdate 시에 cleanup이 실행되도록 할 수도 있다.

<br/>

## **Custom Hooks**
훅을 커스텀하여 생성할 수 있다. 보통 `use` 로 시작하는 이름을 붙인다.  

커스텀 훅은 컴포넌트의 구조를 갖고 있지만 내부에서 `useState` 와 `useEffect` 를 통해 로직을 거쳐 특정 값을 반환하도록 작성하여 만든다.

### **브라우저 Width 받아오기**
브라우저의 Width를 받아오는 훅의 작동 방식은 아래와 같다.

1. 컴포넌트를 하나 생성한다. 이 컴포넌트는 커스텀 훅으로 쓰인다.

2. `window.innerWidth` 값을 `useState` 초기값으로 받아온다.

3. `useEffect` 를 사용하여 최초 마운트 시 이벤트 리스너를 실행한다.

    - 이벤트 리스너는 `window`의 `"resize"` 이벤트를 감시한다.

    - 이벤트가 발생하면 `setWidth`를 통해 state를 재할당한다.

4. 언마운트시 이벤트 리스너를 제거한다.


```js
// 커스텀 훅 생성
export default function useWindowWidth() {

  const [width, setWidth] = React.useState(window.innerWidth);

  useEffect(() => {
    const resize = () => {
      setWidth(window.innerWidth);
    };

    window.addEventListener("resize", resize);

    return () => {
      window.removeEventListener("resize", resize);
    };
  }, []);

  return width;
};
```

```js
// 훅 출력
export default function App() {
  const width = useWindowWidth();

  return (
    <div>
      {width}
    </div>
  );
};
```

### **Mount 여부 props를 추가하는 HOC**
기존의 컴포넌트에 마운트 여부 props를 추가하여 새로운 컴포넌트로 반환하는 HOC를 작성할 수 있다.  

작동 방식은 아래와 같다.  

1. 함수를 하나 생성한다.

2. 마운트 여부를 확인할 컴포넌트를 인자로 전달 받는다.

3. 마운트 여부(`state.hasMounted`)의 초기값을 `false`로 할당한다.

4. 컴포넌트를 렌더할 때 `hasMounted` props를 함께 전달한다.  

    - 이 때, `{...this.props}` 를 통해 기존의 props도 전달한다.

5. 컴포넌트가 마운트되면 `hasMounted` 에 `true`를 할당한다.

6. 디버깅을 위해 `displayName` 으로 새롭게 반환할 컴포넌트의 이름을 구분한다.

```js
// HOC 생성
export default function withHasMounted(Component) {
  class NewComponent extends React.Component {
    state = {
      hasMounted: false,
    };
    render() {
      const { hasMounted } = this.state;
      return <Component {...this.props} hasMounted={hasMounted} />;
    };
    componentDidMount() {
      this.setState({ hasMounted: true });
    };
  };

  NewComponent.displayName = `withHasMounted(${Component.name})`;

  return NewComponent;
};
```

```js
// HOC 사용
function App({hasMounted}) {    // 인자는 props로 대체 가능
  console.log(hasMounted);  // 인자가 props일 경우 props.hasMounted로 호출
  return (
    <div>
    </div>
  );
};

export default hasMounted(App);  // 컴포넌트를 hasMounted에 전달하고 이 내용을 반환한다.
```

### **마운트 여부 props를 전달하는 커스텀 훅**
같은 기능을 하는 위 예시의 HOC는 체크할 컴포넌트를 인자로 전달 받고 마운트 여부를 props로 전달하여 새로운 컴포넌트를 반환했지만,  
커스텀 훅은 자기 자신의 state를 통해 자신이 소속된 컴포넌트의 마운트 여부를 체크한다.

작동 방식은 다음과 같다.  

1. 컴포넌트를 하나 생성한다. 이 컴포넌트는 커스텀 훅으로 사용된다.  

2. `useState` 를 통해 `hasMounted: false` state를 생성한다.

3. `useEffect` 를 통해 최초 마운트 시 `hasNMounted: true` 를 재할당한다.

```js
// 커스텀 훅 생성
export default function useHasMounted() {
  const [hasMounted, setHasMounted] = useState(false);

  useEffect(() => {
    setHasMounted(true);
  }, []);

  return hasMounted
};
```

```js
// 커스텀 훅 사용
export default App() {
  console.log(useHasMounted());
  return (
    <div></div>
  );
};
```

<br/>

## **Additional Hooks**
리액트도 여러 유용한 훅을 제공하고 있다.  

아래에서 소개할 `useCallback`, `useMemo`, `useRef` 등은 렌더 사이에도 계속해서 유지된다는 특징이 있다.  

클래스 컴포넌트의 경우 렌더될 때 클래스 자체는 유지되고 내부의 `render` 메소드만 반복적으로 실행되는 반면에 함수 컴포넌트의 경우 함수 자체가 다시 호출되고 실행되면서 그 내부의 내용도 새롭게 다시 생성된다.  

위에서 말한 훅들을 사용하면 함수 컴포넌트에서 해당 내용들을 굳이 새로 생성하지 않고 지속적으로 유지할 수 있다는 장점이 있다. 타이머 등 지속적으로 유지하는 로직을 사용할 때 유용하다.

### **useReducer**

아래 두 가지의 경우에서 `useState` 대신 사용되는 훅이다.

- 다수의 하위값을 포함하는 복잡한 정적 로직을 만들 경우

- 다음 state가 이전 state에 의존할 경우



`useReducer` 는 `reducer`, `dispatch` 함수와 함께 사용된다.

- `reducer` : state의 값을 변경하는 로직을 갖고 있다. 사용자가 직접 정의해야 한다. 

- `dispatch` : action 객체를 인자로 받는다.  
    
    - `action` : 객체이며, 필수 프로퍼티로 `type`을 갖는다.  


대략적인 작동 방식은 특정 이벤트에서 `dispatch`에 action 타입을 전달하면 `reducer` 내부에서 해당 action 타입에 맞는 로직을 거친 뒤 새로운 state를 반환하는 방식이다.

```js
export default function UseReducer() {

  // reducer 내부에서 action에 대한 state 처리 로직 작성
  const reducer = (state, action) => {
    if (action.type === "PLUS") {
      return {
        count: state.count + 1,
      };
    }
    return state;
  };

  // useReducer를 이용한 state 정의
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <h1>{state.count}</h1>
      <button onClick={click}>클릭</button>
    </div>
  );

  // 클릭 이벤트에 dispatch(action) 실행
  function click() {
    dispatch({ type: "PLUS" });
  };
};
```

### **useMemo**
`useMemo` 는 특정 값이 렌더링마다 불필요하게 매번 반복해서 계산되는 것을 방지하고 지정한 곳에서 변경점이 일어날 때만 계산이 실행되도록 한다.

```js
//  두번째 인자 배열로 전달한 state가 변경될 때만 반환한 함수가 실행된다. 함수의 실행 결과는 지정한 이름으로 호출하여 렌더링할 수 있다.
const 이름 = useMemo(() => {
  return 실행할함수();
}, [state])
```

```js
// user의 age를 합산하는 함수
function sum(user) {
  console.log("sum...");
  return user.map((user) => user.age).reduce((l, r) => l + r, 0);
};

export default function UseMemo() {
  const [value, setValue] = useState("");

  // user state
  const [user] = useState([
    { name: "RAREBEEF", age: 24 },
    { name: "Peter", age: 200 },
  ]);

  // user에 변경점이 존재할 때만 sum() 함수를 실행한다.
  const count = useMemo(() => {
    return sum(user);
  }, [user]);
  

  return (
    <div>
      <input value={value} onChange={change} />
      <h1>{value}</h1>
      <h1>{count}</h1>
    </div>
  );

  function change(event) {
    setValue(event.target.value);
  };
};
```

### **useCallback**
`useCallback` 은 지정한 곳에서 변경점이 발생하기 전까지는 이전의 내용을 기억하고 실행하는 훅이다. 컴포넌트의 최적화에 있어서 중요한 역할을 한다. 

두번째 인자인 배열로 변경점을 체크할 요소들을 전달한다. 해당 요소에서 변경점이 발생하기 전까지는 이전에 실행한 내용을 그대로 기억하고 다음 호출에도 같은 내용이 실행된다.
```js
// value의 초기값만 출력한다.  
// value의 값이 변경되어도 초기값만 출력하게 된다.
const click = useCallback(() => {
    console.log(value);
  }, []);
.
.
.
<button onClick={click}>버튼</button>
```

### **useRef**
`useRef` 는 `React.createRef` 처럼 레퍼런스를 만드는 역할을 하는 훅이다.

```js
const buttonRef = useRef();
.
.
.
<button ref={buttonRef}>버튼</button>
```

`createRef`는 렌더될 때마다 새롭게 생성되는 반면 `useRef` 는 최초 레퍼런스를 생성하면 렌더 사이에도 계속 유지된다는 차이점이 있다.

<br/>

## **React Router Hooks**
React Router는 HOC의 일종인 `withRouter` 외에도 대신 사용할 수 있는 몇 가지의 훅을 제공한다.

**기존 `withRouter` 사용 문법**  
`withRouter` 로 함수 컴포넌트를 감싸고 컴포넌트의 인자로 props를 전달하여 사용한다.
```js
export default withRouter(function ToHome(props) {
  function home() {
    props.history.push("/");
  };
  return (
    <div>
      <button onClick={home}>Home</button>
    </div>
  );
});
```

**`useHistory` 사용 문법**  
컴포넌트에 인자가 필요 없고 history를 변수에 할당하여 사용한다.
```js
export default function ToHome() {
  const history = useHistory();
  function home() {
    history.push("/");
  };
  return (
    <div>
      <button onClick={home}>Home</button>
    </div>
  );
};
```

**`useParams` 사용 문법 (Dynamic Routing)**  
```js
export default function Profile() {
  const params = useParams();
  const id = params.id
  return (
    <div>
      <h1>Profile</h1>
      {id && <h2>ID : {id}</h2>}
    </div>
  );
};
```

<br/>
<br/>

# **컴포넌트 간 통신**

## **하위 컴포넌트로 전달**
상위 컴포넌트에서 하위 컴포넌트로 props를 전달한다.  

이 때 값의 변경은 A에서 이루어지고 값의 출력은 E에서 이루어지는데, 그 사이의 B, C, D는 props를 전달하는 징검다리 역할만 할 뿐 props를 직접 사용하지는 않는다. 때문에 이 징검다리 역할의 컴포넌트에서 누락 혹은 오버라이드가 일어나지 않도록 주의가 필요하다.

```js
export default function A() {
  const [value, setValue] = useState("변경 전");
  return (
    <div>
      <p>A</p>
      <B value={value} />
      <button onClick={click}>버튼</button>
    </div>
  );
  function click() {
    setValue("변경 후");
  }
}

function B({ value }) {
  return (
    <div>
      <p>B</p>
      <C value={value} />
    </div>
  );
}

function C({ value }) {
  return (
    <div>
      <p>C</p>
      <D value={value} />
    </div>
  );
}

function D({ value }) {
  return (
    <div>
      <p>D</p>
      <E value={value} />
    </div>
  );
}

function E({ value }) {
  return (
    <div>
      <p>E</p>
      <p>{value}</p>
    </div>
  );
}
```

<br/>

## **상위 컴포넌트로 전달**
하위 컴포넌트에서 상위 컴포넌트로 값 변경이 전달될 때는 상위 컴포넌트에서 값을 변경하는 함수를 정의한 뒤 하위로 전달한다.  

하위 컴포넌트에서 전달 받은 함수를 실행하여 상위 컴포넌트의 값을 변경하는 방식이다. 

```js
export default function A() {
  const [value, setValue] = useState("변경 전");
  return (
    <div>
      <p>A</p>
      <p>{value}</p>
      <B setValue={setValue} />
    </div>
  );
}

function B({ setValue }) {
  return (
    <div>
      <p>B</p>
      <C setValue={setValue} />
    </div>
  );
}

function C({ setValue }) {
  return (
    <div>
      <p>C</p>
      <D setValue={setValue} />
    </div>
  );
}

function D({ setValue }) {
  return (
    <div>
      <p>D</p>
      <E setValue={setValue} />
    </div>
  );
}

function E({ setValue }) {
  return (
    <div>
      <p>E</p>
      <button onClick={click}>버튼</button>
    </div>
  );

  function click() {
    setValue("변경 후");
  }
}
```

<br/>

## **Context API**
위에서 살펴본 컴포넌트 간 통신 방법은 최종 컴포넌트에 도달하기까지 모든 중첩 관계의 컴포넌트를 거쳐가며 props를 전달해야하는 문제점이 있었다.  

Context를 이용하면 불필요한 props 전달 과정 없이 컴포넌트 트리 전체에 데이터를 제공할 수 있다.

최상위 컴포넌트(Provider)에서 데이터를 set하고 그 모든 하위 컴포넌트에서 데이터를 get하는 구조를 갖게 된다.

## **데이터 Set**

데이터를 Set하는 과정은 아래와 같다.

1. Context 생성

2. `<컨텍스트.Provider>` 로 컴포넌트 감싸기

3. 데이터를 정의 / 할당하고 `value` 로 전달하기

```js
// Context 생성
const UserContext = React.createContext();

export default UserContext;
```

```js
// index.js에서 Provider로 컴포넌트 감싸기
// 데이터 정의/할당하고 Provider에 value로 전달하기
const users = [
  {id: 0, name: "rarebeef"},
  {id: 1, name: "Peter"}
];

ReactDOM.render(
  <React.StrictMode>
    <UserContext.Provider value={users}>
      <App />
    </UserContext.Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```

## **데이터 Get**

데이터를 get하는 방법은 크게 3가지가 있다.  

- Consumer  

- Class 컴포넌트 - `this.context`  

- Function 컴포넌트 - `useContext`

### **Consumer**
컨슈머는 Context 컴포넌트를 불러오고 그 내부에서 함수를 통해 데이터를 꺼내서 사용하는 방법이다. 

```js
return (
  <컨텍스트.Consumer>
    {처리함수}
  </컨텍스트.Consumer>
);
```

```js
// 예시
export default function A() {
  return (
    <UserContext.Consumer>
      {(users) => (
        <ul>
          {users.map((user) => (
            <li>{user.name}</li>
          ))}
        </ul>
      )}
    </UserContext.Consumer>
  );
}
```

### **this.context**
클래스 컴포넌트에서 사용 가능한 방법으로,  
`static contextType` 에 사용할 Context를 설정하고 `this.context`를 변수에 할당하여 사용하는 방법이다.  

한 가지 Context 밖에 불러오지 못한다는 단점이 존재한다.

```js
static contextType = 컨텍스트;
const 변수 = this.context;
```

```js
export default class B extends React.Component {
  render() {
    const users = this.context;
    return (
      <div>
        <ul>
          {users.map((user) => (
            <li>{user.age}</li>
          ))}
        </ul>
      </div>
    );
  }

  static contextType = UserContext;
}
```

### **useContext**
함수 컴포넌트에서 사용 가능한 방법으로,  
`useContext` 의 인자로 Context를 전달하고 그 리턴값인 value를 변수에 할당하여 사용하는 방법이다.  

여러 컨텍스트를 할당하여 사용이 가능하다.

```js
const 변수 = useContext(컨텍스트);
```

```js
export default function C() {
  const users = useContext(UserContext);
  return (
    <div>
      <ul>
        {users.map((user) => (
          <li>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

<br/>
<br/>

# **React Test**
Unit Test는 통합 테스트에 비해 빠르고 통합 테스트 진행 전에 먼저 문제를 찾아낼 수 있다.

## **JEST**
### **설치 & 세팅**
`$ npm i jest -D`

package.json 파일의 scripts 부분에 `"test": "jest"` 라는 명령을 추가한다.

CRA로 리액트 프로젝트를 시작하면 별도의 설치와 세팅이 필요 없다.

### **문법**

프로젝트 폴더 내부에 테스트 파일을 만든다. 테스트 파일명은 "테스트할파일명.test.js" 로 작명한다.

그 안에 아래와 같이 테스트 코드를 작성한다. 첫번째 인자로 테스트 이름, 두번째 인자인 함수로 테스트 할 내용을 작성한다. 

인자로 전달한 함수의 내용은   
`expect(체크할 내용).toBe(기대값);`  
와 같은 구조로 작성한다.

```js
// 10 + 20 의 결과가 30인지 테스트하는 코드
test("10 + 20 = 30 test", () => {
  expect(10 + 20).toBe(30);
});
```

`test()` 함수는 `it()` 으로 작성하여 사용해도 된다.

`$ npm test` 명령으로 테스트를 시작하면 JEST는 자동으로 .test.js 확장자 파일, \_\_tests__ 폴더 내부에 들어있는 파일 등을 감지해서 테스트를 돌리게 된다.


### **테스트 코드 분류**
`describe()` 함수로 여러 테스트 함수를 각각 카테고리별로 분류해서 묶을 수도 있다.  

첫번째 인자로 카테고리명, 두번때 인자로 함수가 들어가는데 이 함수 내부에 묶을 테스트 함수들을 넣으면 된다.  

이 `describe()`는 중첩이 가능하다.

```js
describe("add", () => {
  it("10+20=30 test", () => {
    expect(10 + 20).toBe(30);
  });
  it("5+3=8 test", () => {
    expect(5+3).toBe(8);
  });
})
```

### **참조형 데이터 테스트**

객체와 같은 참조형 데이터는 `toBe()` 로 결과를 비교할 시 모습은 같아도 다른 메모리 주소를 가리키기 때문에 테스트 실패 결과가 나온다. 이러한 경우에는 `toEqual()` 을 통해 결과를 비교해야 한다.

### **자동 테스트**
`$ npx jest --watchAll`
파일 수정이 감지되면 자동으로 테스트가 실행된다.

### **`expect`와 사용 가능한 함수**
- **`toBe`**  
```js
expect(10 + 20).toBe(30);
```
결과와 기대값이 완벽히 같은지 테스트한다.  
참조형 데이터는 모습이 같아도 같지 않다고 판단한다.

- **`toEqual`**  
```js
expect({ id: 0 }).toBe({ id: 0 });
```
결과와 기대값이 같은지 테스트한다.  
참조형 데이터도 모습이 같으면 같다고 판단한다.

- **`toHaveLength`**  
```js
expect("RAREBEEF").toHaveLength(8);
```
`length` 를 체크한다.

- **`toHaveProperty`**  
객체가 속성을 포함하는지 체크한다.  
선택사항인 두번째 인자로 해당 속성의 값까지 체크할 수 있다.
```js
expect({name: "RAREBEEF"}).toHaveProperty("name");
```  
```js
expect({name: "RAREBEEF"}).toHaveProperty("name", "RAREBEEF");
```

- **`toBeDefined`**  
대상이 정의 되었는지(undefined가 아닌지) 체크한다.  
```js
expect({name: "RAREBEEF"}.name).toBeDefined();
  });
```

- **`toBeFalsy`**  
대상이 falsy 한 값인지 체크한다.  
```js
expect(0).toBeFalsy();
```

- **`toBeGreaterThan`**  
값이 더 큰지 체크한다.  
```js
expect(0).toBeGreaterThan(-1);
```

- **`toBeGreaterThanOrEqual`**  
값이 더 큰거나 같은지 체크한다.  
```js
expect(0).toBeGreaterThanOrEqual(-1);
```

- **`not.~`**  
위 함수들 앞에 붙여 사용한다. 부정형으로 변환한다.

<br/>

## **React Component Test 예시**

### **예시 컴포넌트**
  ```js
  import { useEffect, useState, useRef } from "react";
  export default function Button() {

    // 버튼 텍스트 상수화
    const BUTTON_TEXT = {
      NORMAL: "Before click",
      CLICKED: "Clicked",
    };

    // state 정의
    const [state, setState] = useState({ p: BUTTON_TEXT.NORMAL });

    // 타이머 초기화 방지
    const timer = useRef();

    // 언마운트시 타이머 삭제
    useEffect(() => {
      return () => {
        if (timer.current) {
          clearTimeout(timer.current);
        }
      };
    }, []);

    return (
      <div>
        <p>{state.p}</p>
        {/* 버튼의 텍스트에 따라 활성화 상태 변경*/}
        <button onClick={click} disabled={state.p === BUTTON_TEXT.CLICKED}>
          button
        </button>
      </div>
    );

    // 클릭 이벤트
    function click() {
      setState({ p: BUTTON_TEXT.CLICKED });

      // 5초 뒤 원상복귀
      timer.current = setTimeout(() => {
        setState({ p: BUTTON_TEXT.NORMAL });
      }, 5000);
    }
  }
  ```

### **예시 테스트**
  ```js
  import { act, fireEvent, render } from "@testing-library/react";
  import Button from "./Button";

  describe("Button", () => {


    it("Component render", () => {

      // <Button /> 컴포넌트 불러오기
      const button = render(<Button />);

      // <Button /> 컴포넌트 생성 체크하기
      expect(button).not.toBeNull();
    });


    it("Button == HTMLButtonElement", () => {

      // <Button /> 컴포넌트의 메소드 중 getByText 불러오기
      const { getByText } = render(<Button />);

      // <Button /> 컴포넌트 내부에서 "button" 텍스트를 포함한 요소 불러오기
      const buttonElement = getByText("button");

      // 불러온 요소가 HTMLButton 엘리먼트인지 체크하기
      expect(buttonElement).toBeInstanceOf(HTMLButtonElement);
    });


    it("After clicking the Button => Print 'Clicked'", () => {
      const { getByText } = render(<Button />);

      const buttonElement = getByText("button");

      // 버튼에 클릭 이벤트 실행
      fireEvent.click(buttonElement);

      // "Clicked" 텍스트를 포함한 요소 불러오기
      const p = getByText("Clicked");

      // 불러온 요소가 null이 아닌지 체크하기
      expect(p).not.toBeNull();

      // 불러온 요소가 HTMLParagraph 엘리먼트인지 체크하기
      expect(p).toBeInstanceOf(HTMLParagraphElement);
    });


    it("Before clicking the Button => Print 'Before click'", () => {
      const { getByText } = render(<Button />);
      const p = getByText("Before click");
      expect(p).not.toBeNull();
      expect(p).toBeInstanceOf(HTMLParagraphElement);
    });


    it("5 seconds after clicking the button => print 'Before click'", () => {
      // 페이크 타이머
      // 실제 시간이 아닌 가상에서 시간이 흐른 것으로 처리한다.
      // 따라서 시간이 흐르기를 기다릴 필요가 없다.
      jest.useFakeTimers();

      const { getByText } = render(<Button />);

      const buttonElement = getByText("button");

      fireEvent.click(buttonElement);

      // 페이크 타이머 5초 카운트
      // 컴포넌트를 렌더링하고 갱신해주는 코드는 act() 안에 넣어야 한다.
      act(() => {
        jest.advanceTimersByTime(5000);
      });

      const p = getByText("Before click");

      expect(p).not.toBeNull();

      expect(p).toBeInstanceOf(HTMLParagraphElement);
    });


    it("5 seconds after clicking the button => Disable button", () => {
      jest.useFakeTimers();

      const { getByText } = render(<Button />);

      const buttonElement = getByText("button");

      fireEvent.click(buttonElement);

      // 클릭 후 버튼 비활성화 체크
      // @testing-library의 jest-dom에서 추가된 toBeDisabled() 사용
      expect(buttonElement).toBeDisabled();

      act(() => {
        jest.advanceTimersByTime(5000);
      });

      // 5초 후 버튼 활성화 체크
      expect(buttonElement).not.toBeDisabled();
    });
  });
  ```

  <br/>
  <br/>

# **Optimizing Performance**
컴포넌트를 필요할 때만 렌더하도록 만들어서 어플리케이션의 퍼포먼스를 향상할 수 있다.

## **Reconciliation**
Reconciliation 는 렌더 전 후의 일치 여부를 판단하는 규칙이다.  

- 서로 다른 타입의 두 요소는 다른 트리를 만든다.  

- key prop을 통해 변경하지 않을 하위 요소를 지정할 수 있다.

아래와 같은 상황들에서 리액트는 요소를 다시 렌더링할지 아니면 유지할지를 각각 다르게 결정한다.

1. 두 컴포넌트의 하위 컴포넌트가 동일해도 상위 컴포넌트가 다를 경우 하위의 동일한 컴포넌트도 다르다고 인식하고 렌더 시 전부 새롭게 렌더링한다. 

2. 같은 DOM일 때 속성만 다를 경우 다시 렌더하지 않고 속성만 갱신한다. 이는 인라인 방식의 스타일 선언도 마찬가지이다.

3. 같은 컴포넌트일 때 props 혹은 state가 다를 경우 마운트/언마운트는 이루어지지 않고 업데이트만 이루어진다.

4. 처음엔 A 와 B, 두번째는 A와 B와 C 컴포넌트의 렌더를 반복할 때   

  - AB는 계속 동일하기 때문에 리액트는 C 컴포넌트만 반복적으로 마운트/언마운트한다.  

5. 처음엔 B 와 C, 두번째는 A 와 B 와 C 컴포넌트의 렌더를 반복할 때 

  - A 컴포넌트만 맨 앞에 추가하면 될 것 같지만 리액트는 그런 식으로 동작하지 않는다.

  - 리액트 입장에서는 처음과 두번째 렌더에서 B 와 C 컴포넌트의 순서가 다르기 때문에 동일하다는 근거를 찾지 못하기 때문이다.  

  - 리액트는 결국 BC를 AB로 업데이트하고 C를 추가로 마운트하는 방법을 택한다.  

<br/>

### **Key prop**
위 5번과 같은 상황에서 리액트에게 같은 컴포넌트라는 것을 전달하기 위한 prop이 바로 key이다.  

서로 다른 상황의 렌더에서 **같은 컴포넌트에 같은 값의 key를 부여**하여 다른 렌더 상황에서 같은 컴포넌트는 다시 렌더하지 않고 유지하도록 할 수 있다.

<br />

### **shouldComponentUpdate & React.PureComponent**
하위 컴포넌트에 `shouldComponentUpdate` 를 추가하여 상위 컴포넌트가 업데이트 될 때 하위 컴포넌트의 불필요한 업데이트를 방지할 수 있다.

```js
import "./App.css";
import React from "react";

class User extends React.Component {
  shouldComponentUpdate(prevProps) {
    for (const key in this.props) {
      if (prevProps[key] !== this.props[key]) {
        return true;
      }
    }
    return false;
  }

  render() {
    console.log("User render");
    const { name } = this.props;
    return <div>{name}</div>;
  }
}

class App extends React.Component {
  state = {
    text: "",
    users: [
      { id: 1, name: "RAREBEEF" },
      { id: 2, name: "Peter" },
    ],
  };

  render() {
    const { text, users } = this.state;

    return (
      <div>
        <input type="text" value={text} onChange={this._change} />
        <ul>
          {users.map((user) => {
            return <User {...user} key={user.id} />;
          })}
        </ul>
      </div>
    );
  }

  _change = (event) => {
    this.setState({
      ...this.state,
      text: event.target.value,
    });
  };
}

export default App;
```

혹은 클래스 컴포넌트의 `extends` 를 `React.PureComponent` 로 할 경우 별도의 `shouldComponentUpdate` 를 작성하지 않아도 이미 내장된 상태로 컴포넌트가 생성된다.

```js
class User extends React.PureComponent {
  render() {
    console.log("User render");
    const { name } = this.props;
    return <div>{name}</div>;
  }
}
```

`shouldComponentUpdate` 혹은 `React.PureComponent` 사용할 때 주의할 점은 컴포넌트 혹은 DOM의 이벤트 props에 인라인 방식으로 함수를 직접 작성하지 않는 것이다. 직접 작성할 경우 props의 값에 함수가 매번 새로 생성되고 할당되기 때문에 업데이트가 반복해서 이루어진다.

따라서 클래스 컴포넌트에서 메소드를 정의하고 이 메소드를 이벤트 props에 할당하는 방법을 사용해야 한다.

<br/>

### **React.memo()**
함수 컴포넌트의 경우 `shouldComponentUpdate` 혹은 `React.PureComponent` 를 사용할 수 없기 때문에 앞서 알아본 `React.memo()` 를 사용한다. 
```js
const User = React.memo(({name}) => {
  console.log("User render")
  return (
    <div>{name}</div>
  )
});
```

<br/>

### **React.useCallback()**
클래스 컴포넌트는 이벤트 props에 인라인 방식으로 함수를 작성할 경우 매번 다시 렌더가 발생하기 때문에 클래스의 메소드로 따로 분리하여 함수를 정의하였다.  

함수 컴포넌트에서는 메소드를 생성할 수 없다. 따라서 이전의 방법이 먹히지 않기 때문에 앞서 알아본 `useCallback()` 을 사용하여 함수를 매 번 생성하지 않고 이전의 함수를 다시 불러오는 방법을 사용해야 한다.

```js
const click = React.useCallback(() => {}, []);
```

<br/>
<br/>

# **createPortal**
`ReactDOM.createPortal()` 메소드는 자신이 속한 DOM이 아닌 다른 DOM에 children을 삽입할 수 있도록 해준다. 
```js
// Modal.js
// Modal 컴포넌트의 children을 #modal 돔에 연결한다.
// 이 때 Modal 컴포넌트가 #modal 돔에 속해있지 않지만
// createPortal 메소드로 연결이 가능하다.
import ReactDOM from "react-dom";

const Modal = ({children}) => {
  ReactDOM.createPortal(children, document.querySelector("#modal"))
  };

export default Modal
```

```js
// App.js
// 앞서 만든 Modal 컴포넌트에 children을 넣어준다.
// 이 App 컴포넌트는 #root 돔에 삽입되지만
// createPortal로 <Modal>의 children은 #Modal에 삽입된다.
import React, {useState} from "react";
import Modal from "./components/Modal.js";

function App() {

  const [visible, setVisible] = useState(false);

  function open() {
    setVisible(true);
  };
  function close() {
    setVisible(false)
  };

  return (
    <div>
      <button onClick={open}>OPEN</button>
      <Modal>
        <div onClick={close}>
          Hello, world!
        </div>
      </Modal>
    </div>
  );
};

export default App;
```

<br/>
<br/>

# **React.forwardRef**
하위 컴포넌트의 레퍼런스를 상위 컴포넌트에서 만들고 사용할 수 있다.  

상위 컴포넌트에서 레퍼런스 생성   
-> 하위 컴포넌트로 레퍼런스 전달   
-> 레퍼런스를 생성할 요소에 레퍼런스 전달   



```js
// MyInput.js
// 함수 컴포넌트를 React.forwardRef() 로 감싼다.
// 컴포넌트의 함수 인자로 props와 ref를 받아오고,
// 레퍼런스를 생성할 요소에 전달한다.

import React from "react";

export default React.forwardRef(
  function MyInput(props, ref) {
    return (
    <div>
      <p>MyInput</p>
      <input ref={ref} />
    </div>
    )
  }
)
```

```js
// App.js
// 하위 컴포넌트 요소의 레퍼런스를 생성한다.
// 생성한 컴포넌트를 하위 컴포넌트에 전달한다.

function App() {
  const myInputRef = useRef();
  const click= () => {
    console.log(myInputRef.current.value);
  };

  return (
    <div>
      <MyInput ref={myInputRef} />
      <button onClick={click}>send</button>
    </div>
  );
};
```

<br />
<br />

# **SPA 프로젝트 배포**
- 서버가 모든 요청을 처리하는 방식이 아니다.  

- 라우팅 경로에 상관 없이 리액트 앱을 받아서 실행한다.  

- 라우팅은 리액트 앱 실행 이후 적용된다.  

- static 파일을 제외한 모든 요청은 index.html로 응답하여 404 Not found 등을 방지한다.

static을 제외한 요청을 index.html로 대체하는 것은 아래 네가지 방법으로 작업한다.

- `$ serve -s build`

- AWS S3

- node.js express

- NginX

<br/>

## **serve -s build**

1. serve 패키지를 전역 설치한다.  
    - `$ npm i serve -g`

2. serve 명령을 -s 옵션으로 build 폴더를 지정하여 실행한다.  

    - `$ serve -s build`
  
    - -s 옵션은 어떤 라우팅으로 요청해도 index.html을 응답하도록 한다.

<br/>

## **AWS S3**
아마존 웹 서비스를 이용한 배포이다.  

AWS에 버킷을 생성하고 build 폴더 내의 모든 파일을 업로드한다.  

이후 정적 웹사이트 호스팅을 활성화하고 인덱스 문서와 오류 문서를 index.html로 지정한다.

마지막으로 퍼블릭 엑세스 차단을 해제하고 버킷 정책을 수정하여야 url을 통해 배포한 웹에 접근이 가능하다. 이 문서에서는 설명하지 않는다.  

<br/>

## **NginX**

<br/>

## **node.js express**
`$ npm i express`

루트 경로에 server.js 파일을 생성하고 아래 내용을 입력한다.
```js
// express & path import
const express = require("express");
const path = require("path");

const app = express();

// static 경로 지정
app.use(express.static(path.join(__dirname, "build")));

// static 외 경로 지정
app.get("*", (req, res) => {
  res.sendFile(path.join(__dirname, "build", "index.html"));
});

// 포트 지정
app.listen(9000);
```
`$ node server.js` 명령으로 서버를 오픈하고 지정한 포트로 접근이 가능하다.

<br/>

## **SSR 이해**
서버에서 응답을 가져올 때 static 파일만 가져오는 것이 아닌 서버에서 응답 값을 만들어서 내려주고 이후에 static 파일을 내려주게 된다.  

- React Component를 브라우저가 아니라 node.js에서 사용한다.

- `ReactDOMServer.renderToString(<App />);`

    - 결과가 문자열이며, 이를 응답으로 내려준다.  

- 라우팅, 리덕스와 같은 처리를 서버에서 진행한다.

    - 복잡하고 어렵다.

- JSX가 포함된 코드를 서버에서 읽을 수 있도록 babel 설정이 필요하다.

static 파일을 다 내려받은 이후에는 SPA처럼 동작한다.

```js
// express & path import
const express = require("express");
const path = require("path");
const ReactDOMServer = require("react-dom/server");
const React = require("react");
const fs = require("fs");

const app = express();

// static 경로 지정
app.use(express.static(path.join(__dirname, "build")));

app.get("/test", (req, res) => {
  // 리액트 앱 실행 전 보여줄 컴포넌트 생성
  const ssr = ReactDOMServer.renderToString(
    React.createElement("div", null, "Hello")
  );

  // 생성한 컴포넌트를 끼워넣는다.
  const indexHtml = fs
    .readFileSync(path.join(__dirname, "build", "index.html"))
    .toString()
    .replace('<div id="root"></div>', `<div id="root">${ssr}</div>`);

  res.send(indexHtml);
});

// static 외 경로 지정
app.get("*", (req, res) => {
  res.sendFile(path.join(__dirname, "build", "index.html"));
});

// 포트 지정
app.listen(9000);

```
