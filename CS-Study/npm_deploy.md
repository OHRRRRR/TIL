# 프로젝트를 npm에 배포하려면 어떤 설정이 필요할까

npm(Node Package Manager)에 패키지를 배포하려면 몇 가지 설정이 필요합니다.

## 1. `package.json` 설정

프로젝트 루트 디렉터리에 `package.json` 파일을 작성해야 합니다.

```json
{
  "name": "my-awesome-package",
  "version": "1.0.0",
  "description": "이 패키지는 멋진 기능을 제공합니다.",
  "main": "index.js",
  "scripts": {
    "test": "jest"
  },
  "keywords": ["utility", "npm", "package"],
  "author": "Your Name",
  "license": "MIT"
}
```

- `name`: 패키지 이름 (고유해야 함)
- `version`: 배포할 패키지 버전
- `description`: 패키지 설명
- `main`: 진입 파일 (예: `index.js`)
- `scripts`: 테스트 및 빌드 스크립트 정의
- `keywords`: npm 검색 시 노출될 키워드
- `license`: 라이선스 종류 (보통 `MIT`, `Apache-2.0` 등)

## 2. `.npmignore` 설정

배포하지 않을 파일을 `.npmignore` 파일에 추가합니다.

```txt
node_modules
test
.git
.gitignore
.env
```

## 3. npm 로그인 및 배포

npm 계정이 없다면 [npm 공식 사이트](https://www.npmjs.com/)에서 가입 후 터미널에서 로그인합니다.

```sh
npm login
```

이후 배포를 진행합니다.

```sh
npm publish
```

배포가 완료되면, `npm install my-awesome-package` 명령어로 설치할 수 있습니다.

---

</br>

# 브라우저 렌더링 과정

브라우저가 HTML, CSS, JavaScript를 받아서 화면에 표시하는 과정을 렌더링(Rendering)이라고 합니다.

### 1. HTML 파싱 (Parsing)

- HTML을 읽어 **DOM(Document Object Model)**을 생성합니다.
- `<script>` 태그를 만나면 기본적으로 JavaScript 실행을 위해 파싱을 멈춥니다.

### 2. CSS 파싱 및 스타일 계산

- CSS를 읽고, 각 요소에 적용할 스타일을 계산하여 **CSSOM (CSS Object Model)**을 만듭니다.

### 3. 렌더 트리(Render Tree) 생성

- DOM과 CSSOM을 결합하여 **렌더 트리**를 생성합니다.
- `display: none;` 같은 스타일이 적용된 요소는 렌더 트리에 포함되지 않습니다.

### 4. 레이아웃(Layout, Reflow)

- 요소들의 크기와 위치를 계산합니다.

### 5. 페인팅(Painting)

- 요소의 색상, 그림자, 배경 등을 픽셀 단위로 칠하는 과정입니다.

### 6. 합성(Compositing)

- 여러 개의 레이어를 합쳐서 최종 화면을 생성합니다.

</br>

# 브라우저는 어떻게 동작하나요?

브라우저는 사용자가 웹사이트를 방문할 때 요청(Request)부터 화면에 표시(Rendering)하는 과정까지 수행합니다.

### 1. URL 입력 & 요청(Request)

- 사용자가 주소창에 URL을 입력하면 브라우저가 **DNS 조회**를 통해 서버의 IP 주소를 찾습니다.
- `GET /index.html HTTP/1.1` 같은 요청을 서버로 보냅니다.

### 2. 서버 응답(Response)

- 서버가 HTML, CSS, JavaScript 등의 데이터를 응답으로 보냅니다.
- 브라우저는 응답을 받으면 **캐시(Cache)**에 저장하여 재사용합니다.

### 3. HTML, CSS, JS 파싱 및 실행

- HTML을 파싱하여 **DOM 트리**를 생성합니다.
- CSS를 적용하여 스타일을 결정합니다.
- JavaScript를 실행하여 동적인 기능을 추가합니다.

### 4. 렌더링(Rendering)

- DOM과 CSSOM을 결합하여 화면을 그립니다.
- 사용자의 스크롤, 클릭 등 이벤트에 따라 페이지를 업데이트합니다.

## 브라우저 최적화 방법

- CDN(Content Delivery Network) 사용
- HTTP/2, Gzip 압축 활용
- JavaScript 파일을 `defer` 또는 `async`로 로드
- 이미지 최적화 (WebP 사용 등)
