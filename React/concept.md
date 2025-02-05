# < 프레임워크 vs 라이브러리 >

Angularjs와 vuejs는 프레임워크이고, 리액트는 라이브러리

- 프레임워크: 흐름의 제어 권한을 개발자가 아닌 프레임워크가 가지고 있음
- 라이브러리: 흐름에 대한 제어를 하지 않고, 개발자가 필요한 부분만 필요할 때 가져다 사용하는 것. 제어 권한이 개발자에게 있음

### <리액트 장점>

- 빠른 업데이트와 렌더링 속도 (리액트는 하나의웹페이지이므로 하나의 돔 사용)
  - virtual DOM (가상의 돔) : 돔을 직접 수정하는 것이 아닌 업데이트해야하는 최소 부분을 찾아서 업데이트
  - (DOM이란 웹페이지를 정의하는 하나의 객체, 웹사이트에 대한 정보를 모두 담고 있는 큰 그릇)
    - 화면이 업데이트 됨 = 돔이 수정된다
- Component-Based: 레고 블록 조립하듯 컴포넌트들을 모아서 개발
- 재사용성 (Reusability) → 개발 기간이 단축됨, 유지보수 용이함

### <단점>

- 방대한 학습량 : 기존과 다르므로 배워야할 새로운 개념이 많음
- 높은 상태관리 복잡도: state 관리에 익숙해져야 함
  </br>

##  < 리액트 실행 >

- VS CODE 실행
- terminal → npx create-react-app my-app 입력 ( 이때 my-app은 프로젝트 이름)
- cd my-app
- npm start
  <명령어>
  ```html
  프로젝트 생성: npx create-react-app my-app 경로변경: cd my-app 애플리케이션
  실행: npm start
  ```
    </br>

## < JSX >

: JavaScript + XML/HTML

```html
const element =
<h1>Hello, world!</h1>
; : h1태그로 둘러쌓인 문자열을 element라는 변수에 저장
```

- 역할: XML, HTML 코드를 JavaScript로 변환
- 장점: 코드간결, 가독성 향상, 보안성 올라감
- 사용법

  - html과 javascript가 섞인 형태로 코드 작성 → XML/HTML {JavaScript코드} XML/HTML

  ```html
  const name= '소플'; const element =
  <h1>안녕, {name}</h1>
  ;
  ```

  - 태그의 속성에 값을 넣는 방법

  ```html
  // 큰따옴표 사이에 문자열을 넣거나
  const element = <div tabIndex="0"></div>>;

  // 중괄호 사이에 자바스크립트 코드를 넣으면 됨
  const element = <img src={user.avatarUrl}></img>;
  ```

  - 자식을 정의하는 방법

  ```
  // div의 children은 h1,h2 태그
  const element = (
    <div>
  	    <h1>안녕하세요</h1>
  	    <h2>열심히 리액트를 공부해 봅시다!</h2>
    </div>
  );
  ```
