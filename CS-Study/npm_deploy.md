# 프로젝트를 npm에 배포하려면 어떤 설정이 필요할까

npm으로 배포하려면 당연히 npm으로 생성한 프로젝트가 있어야 함

```
npm init -y
```

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

### 버전 관리

버전 체계는 일반적으로 major, minor, patch로 구성된다. 예를 들어 버전이 1.2.3인 경우 각각 매칭되는 구성요소는 다음과 같다.

major : 1
minor : 2
patch : 3
다른 글에 워낙 잘 정리되어 있어서 글을 안 남기려고 했는데, 각각의 개념을 최대한 간략하게 정리하면 다음과 같다.

- major : 주 버전이라고 하며, 소프트웨어의 주요 변경사항이나 업그레이드를 나타낸다. major가 올라간다는 것은 기존 버전과 호환되지 않는 큰 변화가 존재할 수 있음을 암시한다.
- minor : 부 버전이라고 하며, 새로운 기능이 추가되거나 기존 기능이 개선되었음을 나타낸다. minor가 올라간다는 것은 주 버전과의 호환성을 유지하면서 새로운 기능이 추가되었거나 개선되었음을 암시한다.
- patch : 패지 버전이라고 하며, 주로 버그 픽스, 코드 수정 등의 작은 변경 사항은 나타낸다. 주 버전과 부 버전 사이의 패치가 이루어지며 기존 기능의 오류를 수정하거나 안정성을 개선하는데 주로 사용된다.

npm 또한 위와 같은 버전 체계를 따르며, package.json의 version을 변경하는 명령어를 제공한다.

```txt
# PATCH 한 단계 올림
npm version patch

# MINOR 한 단계 올림
npm version minor

# MAJOR 한 단계 올림
npm version major

# 직접 버전 변경
npm version [VERSION]
```

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

## 4. 패키지 배포 자동화

패키지 배포를 자동화하기 위해 GitHub Actions를 활용하였다. 먼저, GitHub Actions로 배포하는 과정을 정리해보면 다음과 같다.

1. master 브랜치에 커밋되면, package.json의 version에도 변경점이 있는지 확인한다.
2. 변경점이 있으면 이전 커밋과 현재 커밋의 package.json의 version을 확인한다.
3. 이 둘이 서로 다른 경우 현재 커밋을 기준으로 tag를 생성하고 push한다.
4. 3번 작업이 완료되면 release를 생성한다.
5. 4번 작업이 완료되면 npm에 배포한다.
6. 5번 작업이 완료되면 GitHub Packages에 배포한다.

위에도 언급했지만, 사실상 6번은 GitHub Packages로 배포한다기보다도 GitHub Repository에 현재 npm 버전을 보여주기 위한 용도로 이용하였다.

위의 논리대로 동작하는 코드는 다음과 같다.

- master 브랜치에 push 될 때, package.json의 내용이 변경되면 실행

```sh
on:
  push:
    branches: [master]
    paths: ['package.json']
```

- 이전 커밋과 현재 커밋에서 package.json의 version을 outputs에 저장

```sh
jobs:
  diff:
    runs-on: ubuntu-22.04
    outputs:
      previous: ${{ steps.version.outputs.previous }}
      current: ${{ steps.version.outputs.current }}
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 2
      - id: version
        run: |
          previous=$(git show HEAD^:package.json | grep '"version"' | awk -F '"' '{print $4}')
          current=$(git show HEAD:package.json | grep '"version"' | awk -F '"' '{print $4}')
          echo "previous=v$previous" >> $GITHUB_OUTPUT
          echo "current=v$current" >> $GITHUB_OUTPUT
```

- 현재 버전을 기준으로 tag 생성 후 push
- 이전 커밋과 현재 커밋의 package.json의 version이 다른 경우 실행

```sh
jobs:
  diff:
  create-tag:
    needs: diff

    if: needs.diff.outputs.previous != needs.diff.outputs.current
    runs-on: ubuntu-22.04
    outputs:
      tag: ${{ steps.tag.outputs.tag }}
    steps:
      - uses: actions/checkout@v4
      - id: tag
        run: |
          tag=${{ needs.diff.outputs.current }}
          git tag $tag
          git push origin $tag
          echo "tag=$tag" >> $GITHUB_OUTPUT
```

- tag가 생성되면 release도 생성

```sh
jobs:
  diff:
  create-tag:
  create-release:
    needs: create-tag
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
      - uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ needs.create-tag.outputs.tag }}
          release_name: ${{ needs.create-tag.outputs.tag }}
          draft: false
          prerelease: false
```

- release가 생성되면 npm에 배포

```sh
jobs:
  diff:
  create-tag:
  create-release:
  npm-publish:
    needs: create-release
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          registry-url: https://registry.npmjs.org
      - env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
        run: |
          npm ci
          npm run build
          npm publish
```

- npm에 배포완료 후 GitHub Packages로도 배포

```sh
jobs:
  diff:
  create-tag:
  create-release:
  npm-publish:
  github-packages:
    needs: npm-publish
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          registry-url: https://npm.pkg.github.com
      - env:
          NODE_AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          npm ci
          npm run build
          npm publish
```

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
