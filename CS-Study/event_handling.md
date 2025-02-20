# 이벤트 버블링, 캡처링, 이벤트 위임

JavaScript의 이벤트 모델에서 **이벤트 버블링(Event Bubbling), 이벤트 캡처링(Event Capturing), 이벤트 위임(Event Delegation)**은 DOM 요소의 이벤트 전파 방식과 효율적인 이벤트 처리를 이해하는 데 중요한 개념입니다.

---

## 1. 이벤트 버블링(Event Bubbling)

### 이벤트 버블링이란?

이벤트가 발생하면 **가장 깊은 요소(자식 요소)에서부터 시작하여 부모 요소 방향으로 이벤트가 전파되는 현상**을 말합니다. 즉, 특정 요소에서 이벤트가 발생하면, 그 이벤트는 해당 요소의 부모 요소까지 전파됩니다.

### 이벤트 버블링의 동작 방식

1. 가장 먼저 **이벤트가 발생한 요소(이벤트 타겟, Event Target)**에서 이벤트가 실행됩니다.
2. 그다음 **이벤트가 부모 요소로 전파**되며, 최상위 요소(`<html>` 요소)까지 올라갑니다.

### 이벤트 버블링 예제

```html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>이벤트 버블링</title>
  </head>
  <body>
    <div id="parent">
      <button id="child">클릭하세요</button>
    </div>

    <script>
      document.getElementById("parent").addEventListener("click", function () {
        alert("부모 요소 클릭");
      });

      document.getElementById("child").addEventListener("click", function () {
        alert("자식 요소 클릭");
      });
    </script>
  </body>
</html>
```

</br>

## 2. 이벤트 캡처링(Event Capturing)

### 이벤트 캡처링이란?

이벤트가 부모 요소에서 시작하여 자식 요소로 전파되는 방식을 의미합니다. 이벤트 캡처링은 버블링과 반대 방향으로 동작합니다.

### 이벤트 캡처링의 동작 방식

1. \*\*이벤트가 최상위 요소(<html>)에서 시작하여 점점 하위 요소로 내려옵니다.
2. 가장 마지막에 \*\*이벤트가 발생한 요소에서 실행됩니다.

### 이벤트 캡처링 예제

```html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>이벤트 캡처링</title>
  </head>
  <body>
    <div id="parent">
      <button id="child">클릭하세요</button>
    </div>

    <script>
      document.getElementById("parent").addEventListener(
        "click",
        function () {
          alert("부모 요소 클릭");
        },
        true
      ); // true를 설정하여 캡처링 모드 활성화

      document.getElementById("child").addEventListener("click", function () {
        alert("자식 요소 클릭");
      });
    </script>
  </body>
</html>
```
