## < Rendering Elements >

- elements: 어떤 물체를 구성하는 성분, 리액트 앱을 구성하는 가장 작은 블록들

### 1) create Element 함수를 호출할 때 넣는 3가지의 파라미터

```html
React.createElement( type, [props], [...children] )
```

- type: HTML 태그 이름이 문자열로 들어가거나, 또다른 react component가 들어가게 됨
- props: element의 속성 ex) class.style
- children: 해당 element의 자식 element들이 들어감

### 2) create Element 함수 동작과정

```html
function Button(props) { return (
<button className="{`bg-${props.color}`}">
  <b> {props.children} </b>
</button>
) } function ConfirmDaialog(props) { return (
<div>
  <p>내용을 확인하셨으면 확인 버튼을 눌러주세요.</p>
  <button color="green">확인</button>
  <div>) }</div>
</div>
```

### 3) React elements

- 리액트 Elements는 자바스크립트 객체 형태로 존재, 우리 눈에 실제로 보이는 것을 기술 → 불변성
- elements 생성후에는 children이나 attributes를 바꿀 수 없음
- 따라서 변경하기 위해서는 업데이트하는 방식으로 해야함

### 4) Elements 렌더링하기

ex) element를 생성하고, 생성된 element를 root div에 렌더링하는 코드

```
const element = <h1>안녕, 리액트!</h1>
ReactDom.render(element, document.getElementById('root'));
```
