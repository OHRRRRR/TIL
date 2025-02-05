## < Components and Props >

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/7df3beb4-7310-45fc-9c9c-d82b65d35bde/b3638e82-0dcc-4bd3-a6b5-903fc86756f2/image.png)

react component는 붕어빵 틀 의미

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/7df3beb4-7310-45fc-9c9c-d82b65d35bde/588219e2-cd75-4a64-b49d-f03757d24680/image.png)

props는 붕어빵에 들어가는 재료를 의미

### 1) Component

: 작은 컴포넌트들이 모여 하나의 컴포넌트 구성, 컴포넌트들이 모여 전체 페이지 구성

- Component 만들기

  1. Function Component (주로 사용) → hook 사용

     ```html
     //하나의 props객체를 받아서 인사말이 담긴 react element를 리턴 function
     Welcome(props) { return
     <h1>안녕, {props.name}</h1>
     ; }
     ```

  2. Class Component (React.Component를 상속받아서 만듦)

     ```html
     class Welcome extends React.Componenet { render() { return
     <h1>안녕, {this.props.name}</h1>
     ; } }
     ```

- 특징
  - Component 이름은 항상 대문자로 시작해야 함

### 1-1) Component 렌더링

```html
//welcome이라는 함수 컴포넌트를 선언하고, Welcome name="인제"라는 값을 가진
element를 파라미터로해서 ReactDOM.render함수를 호출 리액트는 Welcome 컴포넌트에
name:인제라는 props를 넣어서 호츨하고, 그 결과로 react element 생성 function
Welcome(props) { return
<h1>
  안녕, {props.name}
  <h1>
    ; } const element = <Welcome name="인제" />; ReactDOM.render( element,
    document.getElementById('root') );
  </h1>
</h1>
```

### 1-2) Component 합성

: 리액트는 Component 안에 또 다른 Component를 쓸 수 있음 → 따라서 복잡한 화면을 여러 개의 Component로 나눠서 구현 가능

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/7df3beb4-7310-45fc-9c9c-d82b65d35bde/84464c70-515e-40f1-8c88-306756c86c58/image.png)

```html
//props의 값을 다르게해서 Welcome 컴포넌트 여러번 사용 function Welcome(props) {
return
<h1>
  Hello, {props.name}
  <h1>
    ; } functiom App(props) { return (
    <div>
      <Welcome name="Mike" />
      <Welcome name="Steve" />
      <Welcome name="Jane" />
    </div>
    ) } ReactDOM.render(
    <App />, document.getElementById('root')
  </h1>
</h1>
```

### 1-3) 컴포넌트 추출

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/7df3beb4-7310-45fc-9c9c-d82b65d35bde/6c6ccbc8-12f0-4fe8-b06f-dfb98d3888f2/image.png)

```html
//user-info 컴포넌트 추출
```

```html
function Avatar(props) { return (
<img className="avatar" src="{props.user.avatarUrl}" alt="{props.user.name}" />
```

< Avatar 컴포넌트 추출 후 수정 >

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/7df3beb4-7310-45fc-9c9c-d82b65d35bde/53a8cbf7-0ad8-43c5-91b3-502bb888858d/image.png)

### 2) Props (proprety)

: react component의 속성

: 컴포넌트에 전달할 다양한 정보를 담고 있는 자바스크립트 객체

- 특징
  - Read- Only: 값을 변경할 수 없음 (붕어빵이 다 구워지면 속재료 바꿀 수 없음)
  - 다른 props의 값으로 element 생성하는 방법 → 새로운 값을 컴포넌트에 전달하여 새로 element를 생성
  - 모든 리액트 컴포넌트는 props를 직접 바꿀 수 없고, 같은 props에 대해서는 항상 같은 결과를 보여줄 것
- Props 사용법

: App 컴포넌트 내에서 Profile 컴포넌트를 사용하고, 그 안에 name, introduction, viewCount라는 속성을 사용함

```html
//jsx 사용하는 형태 function App(props) { return (
<Profile
  name="소플"
  introduction="안녕하세요, 소플입니다."
  viewCount="{1500}"
  -
>
  중괄호를 사용하면 무조건 자바스크립트 코드 사용 /> ); }</Profile
>
```
