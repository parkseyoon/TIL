# HTML 코딩 컨벤션

## 1. Syntax
- 들여쓰기는 2개의 공백 문자(소프트탭)을 사용. 다른 규칙으로 통일하여 작성해도 된다.
- 모든 엘리먼트 명과 애트리뷰트 명은 케밥 표기법(kebab-case)으로 작성.
- 모든 애트리뷰트 값은 큰 따옴표(")로 감싸기.
- 주석은 `<!-- -->` 처럼 기본 표기하고

```html
<!-- start : 20220329 수정 및 추가 -->
<div> 내용내용내용내용내용내용내용내용내용 </div>
<!-- end : 20220329 수정 및 추가 -->
```

또는

```html
<!-- 20220329 수정 및 추가 -->
<div> 내용내용내용내용내용내용내용내용내용 </div>
<!-- // 20200330 수정 및 추가 -->
```

## 2. Doctype
- Doctype은 HTML5 DTD 로 선언. <br> `<!DOCTYPE html>` HTML5 로 지정

<br>

자기 마침 태그(Self-Closing Tags)에 후행 슬래시(/)를 사용금지.

```hmtl
<!-- Bad -->
<input />
<br />

<!-- Good -->
<input>
<br>
```

## 3. Metadata

`<head>` 엘리먼트의 자식 엘리먼트는 아래의 순서대로 작성.

1. Charset
2. X-UA-Compatible
3. Viewport
4. Title
5. Meta
6. Style
7. JavaScript

```html
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no" >
<title>Hello, World!</title>
<meta content="" property="og:title">
<meta content="" property="og:url">
<meta content="" property="og:description">
<meta content="" property="og:image">
<meta content="website" property="og:type">
<meta content="" property="og:site_name">
<link rel="stylesheet" href="foo.css">
<script src="bar.js"></script>
```

### A. Charset

문서의 언어셋은 UTF-8으로 선언.

```html
<meta charset="utf-8">
```

<br>

### B. X-UA-Compatible

PC용 웹사이트는 최신 버전의 IE로 렌더링하기 위해 문서모드를 Edge로 선언.

```html
<meta http-equiv="X-UA-Compatible" content="ie=edge">
```

<br>

### C. Viewport

모바일 기기에서 실제 렌더링 되는 영역과 뷰포트의 크기를 조절. 또한 줌 레벨도 조정가능.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no" >
```

<br>

- `width=device-width`: 페이지의 너비를 기기의 스크린 너비로 설정한다. 즉, 렌더링 영역을 기기의 뷰포트의 크기와 같게 만들어준다.
- `initial-scale=1.0` : 처음 페이지 로딩 시 확대/축소가 되지 않은 원래 크기를 사용하도록 한다. 0~10 사이의 값을 가진다.
- `minimum-scale` : 줄일 수 있는 최소 크기를 지정. 0~10 사이의 값을 가진다.
- `maximum-scale` : 늘일 수 있는 최대 크기를 지정. 0~10 사이의 값을 가진다.
- `user-scalable` : yes 또는 no 값을 가지며, 사용자가 화면 확대/축소 지정.

<br>

위의 줌 레벨은 1이 원래크기이고, 0.5라면 50% 축소를 뜻한다.

## 4. Elements

### a. 스타일 제어가 어려운 엘리먼트

자식 엘리먼트 태그가 한정적이거나(ex. `<table>`) 스타일 제어에 한계를 가진 엘리먼트(ex. `<select>`)가 컴포넌트의 루트 역할로 쓰일 땐 나중에 발생할 유지보수를 고려해 `<div>`나 `<span>` 엘리먼트로 감싸는 것을 추천.

```html
<!-- Not Bad -->
<table class="table"></table>
<select class="combobox"></select>

<!-- Good -->
<div class="table">
    <table></table>
</div>
<span class="combobox">
    <select></select>
</span>
```

<br>

### b. 테이블 제목
- `<caption>` 엘리먼트의 뷰를 숨길 때는 새로운 엘리먼트로 감싸서 숨간다. `<caption>`을 바로 숨긴다면 브라우저에 따라 스타일이 깨질 수도 있다. <br> 테이블의 제목이 필요없거나 이미 제공되었다면 생략. 컨텐츠를 중복 제공 X

```html
<!-- Bad -->
<table>
    <caption class="blind">My Caption</caption>
</table>

<!-- Good -->
<table>
    <caption>
        <div class="blind">My Caption</caption>
    </caption>
</table>
```

<br>

### c. 입력 필드
회원가입 폼의 입력 필드처럼 너비, 높이가 유동적이라면 인라인 스타일로 제어. 이렇게 하면 불필요한 클래스 생성을 막을 수 있다.

```html
<!-- Bad -->
<input type="text" class="input input--width-120">
<input type="text" class="input input--width-180">

<!-- Good -->
<input type="text" class="input" style="width:120px">
<input type="text" class="input" style="width:180px">
```

<br>

## 5. Attributes
- 애트리뷰트는 변하지 않는 것부터 먼저 선언. 애트리뷰트의 순서가 비슷한 엘리먼트끼리 통일되므로 검색하기 좋다.
- id는 하나의 페이지 안에서 이름이 유일해야하고, name은 중복 될 수 있다. <br> 따라서 다로따로 접근할 때는 id 값을 이용하고, 그룹으로 접근할 때는 name을 활용하는 식으로 편의성을 가질 수있다. <br> 하지만 대체적으로 ajax 통신을 직접하지 않고 마크업 기준으로만 작업한다면 id만 쓰는 것을 추천. 다수 선택은 class로 사용하는 것을 추천한다. (name은 주로 form 요소로써 통신하는 목적으로 주 사용.)

```html
<input class="input" type="text" id="userId" name="userId" title="아이디" style="width: 100px">
<input class="input" type="password" id="userPw" name="userPw" title="비밀번호" style="width: 120px">
```

### a. Boolean 애트리뷰트
- HTML5에서는 Boolean 애트리뷰트를 선언하는 것 만으로도 true 값을 가진다. 필요하지 않다면 값을 작성하지 않는게 좋다.

```html
<!-- Not Bad -->
<button disabled="true"></button>

<!-- Good -->
<button disabled></button>
```

### b. name 애트리뷰트
- name 애트리뷰트 값은 비즈니스 로직을 작성하는 언어의 네이밍 규칙에 맞게 작성(캐멀케이스로 작성)하는 것을 권장한다.
- name 이 없을 시 id 값을 캐멀케이스로 작성.

```html
<!-- camelCase -->
<form class="form-group" id="myForm" name="myForm">
    <input class="input" type="text" id="myUserName" name="myUserName">
</form>
```

<br>

## Import
- HTML5에서 CSS와 JS파일을 불러올 때 type 애트리뷰트는 이미 기본값을 가진다. 필요하지 않다면 선언하지 않는다. <br> `<script>` 엘리먼트는 가급적 `<head>` 또는 `<body>` 엘리먼트의 가장 마지막에 작성한다. <br> (웹브라우저는 `script` 엘리먼트를 만나면 처리가 끝날 때까지 HTML 파싱을 멈춘다.)

<br>

```html
<!-- Bad -->
<script type="text/javascript">
    // Javascript code
</script>

<!-- Good -->
<script>
    // Javascript code
</script>
```

<br>

- `<head></head>` 태그 내에서 로드 순서 지키기. (CSS 태그를 자바스크립트 태그 앞에 두기.)
- 자바스크립트 전에 CSS 태그를 두면 브라우저의 렌더링 속도를 높이는 병렬 다운로드가 가능해진다.
  
<br>

```html
<!-- Not recommended -->
<script src="jquery.js"></script>
<script src="foo.js"></script>
<link rel="stylesheet" href="foo.css">

<!-- Recommended -->
<link rel="stylesheet" href="foo.css">
<script src="jquery.js"></script>
<script src="foo.js"></script>
```