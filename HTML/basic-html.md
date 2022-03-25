# HTML 기본지식
> 개요

HTML(Hyper Text Markup Language)는 웹에서 사용하는 문서양식을 말한다. 주로 tag를 사용하여 문서의 구조등을 기술한다.

> 특징

- 지금도 개발 중이고, 다양한 기능이 계속 추가되고 있다.
- 멀티미디어 요소를 별도의 플러그인 없이도 재생가능하다.
- 서버와 클라이언트 사이에 소켓 통신이 가능하다.
- Semanic tag 추가로 tag의 내용만을 검색해서 보다 빠르게 검색을 진행 할 수 있다.
  
> 작동 원리

- 서버는 클라이언트의 요청 내용을 분석하여 결과값을 HTML로 전송한다.
- 서버는 결과 값을 전송한 후 클라이언트와 연결 종료한다.
- 클라이언트는 서버로부터 전달받은 HTML을 웹 브라우저에 표시한다.
- 각 웹브라우저는 브라우저 엔진이 내장되어 있고, 이 엔진이 tag를 해석해서 화면에 표시한다.

> HTML tag

- tag는 시작 tag와 종료 tag로 쌍을 이루거나, 시작 tag만 존재하는 경우도 있다.
- 종료 tag는 '/'로 구분하여 중첩되지 않도록 한다.
- 각각의 tag는 속성과 속성의 값이 존재한다.
```html
<a href = "www.google.com"> go naver </a>
시작 tag / 속성이름 / 속성 값 /         / 종료 tag
```

- tag에는 어느 tag에나 넣어서 사용 할 수 있는 글로벌 속성이 있다.

| 글로벌 속성 | 설명 |
|:-:|:-:|
| class | tag에 적용할 스타일의 이름을 지정한다. <br><br>  ex) `<div class = "content" ... > ... </div>`|
| dir | 내용의 텍스트 방향을 지정한다. 왼쪽 >> 오른쪽 (default, ltr)  오른쪽 >> 왼쪽 (rtl) <br><br>  ex) `<p dir = "rtl"> 오른쪽에서 왼쪽으로 표시됨, </p>` |
| id | tag에 유일한 ID를 지정한다. JavaScript에서 주로 사용. <br><br> ex) `<input type = "text" id = "userid" >` |
| style | 인라인 스타일을 적용하기 위해 사용 <br><br>  ex) `<p style = "color: red; text-align: center;"> ... </p>` |
| title | tag에 추가 정보를 지정, tag에 마우스 포인터를 위치시킬 경우 title의 값 표시 |
<br>

1. 주석
    - 주석의 내용은 브라우저에 출력이 되지 않는다.
    - HTML tag의 내용을 설명하기 위해 쓴다.
```html
<!-- 주석은 이렇게 사용한다. -->
```
<br>

2. 구성요소
   - `<html>` tag는 HTML 문서 전체를 정의한다.
   - `<head>`와 `<body>`로 구성되어있다.
   - ```html
        <!DOCTUPE html>
        <html>
            <head> <!-- 브라우저에게 HTML 문서의 머리부분임을 인식시킨다. (외부에 나타나지 않음) -->
                <meta charset="UTF-8">
                <title> 제목 </title>
            </head>

            <body> <!-- 브라우저에 보여질 문서의 내용을 작성한다. -->
                내용
            </body>
        </html>
        ```
    - id 속성은 중복하여 값을 가질 수 없으므로 이를 이용하여 문서 내에서 tag를 유일하게 식별가능하게 한다.
   - class 속성은 중복하여 값을 가질 수 있다. 이를 이용하여 여러 tag에 공통적인 특성을 부여할 수 있다.

<br><br>

3. 포맷팅 요소
   - 포맷팅 요소에는 화면에는 동일하게 출력되지만 각 요소가 가진 의미가 다른 것이 있을 수 있다.

| tag 명 | 설명 |
|:-:|:-:|
| `<abbr>` | 생략된 약어 표시 |
| `<address>` | 연락처 정보 표시 |
| `<blockquote>` | 긴 인용문구 표시, 좌우로 들여쓰기가 된다. |
| `<q>` | 짧은 인용문구 표시, 좌우로 따옴표가 붙는다. |
| `<hr>` | 구분선 |
| `<b>, <strong>` | 굵은 글씨로 표시, 특정 문자열을 강조한다. |
| `<i>, <em>` | 기울게 표시 | 

<br><br>

4. 목록형 요소

| tag 명 | 설명 |
|:-:|:-:|
| `<ul>` | 번호 없는 목록을 표시, 항목 앞에 심볼 표시 |
| `<ol>` | 번호 있는 목록을 표시, 숫자, 알파벳, 로마숫자 등으로 표시 |
| `<li>` | 목록 항목 `<ul>`이나 `<ol>` tag 내부에서 사용 |

<br><br>

5. HTML table 모델
   - HTML table 모델은 데이터를 행과 열의 셀에 표시한다.
   - 테이블의 셀은 머리글(th)나 데이터(td)를 가질 수 있다.

```html
<table>
    <thead>
    <tr>
        <th>title 1</th>
        <th>title 2</th>
        <th>title 3</th>
    </tr>
    </thead>
    
    <tbody>
    <tr>
        <td>data 1</td>
        <td>data 2</td>
        <td>data 3</td>
    </tr>
    <tr>
        <td>data 4</td>
        <td>data 5</td>
        <td>data 6</td>
    </tr>
    </tbody>
</table>
```

![table](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6vEUI%2FbtqYN1VxELw%2FQjZBI3ZvKbSgODww1IMcG0%2Fimg.png)

- cellspading은 셀과 셀 사이의 공간을 의미한다.
- cellpadding은 셀 외곽과 셀 컨텐츠 사이의 공간을 의미한다.
  
![table](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcGuoNM%2FbtqY8G2JeEu%2FczhlK7KWXQSAKeGkyzfnOk%2Fimg.png)

- colspan : 두개 이상의 열(Column)을 하나로 합치기 위해 사용
- rowspan : 두개 이상의 행(Row)를 하나로 합치기 위해 사용

<br><br>

6. 링크 요소
   
   - anchor 속성은 `<a>` tag를 사용하며, 하나이 문서에서 다른 문서로 연결하기 위해 하이퍼링크를 사용하며 서로 중첩해서 사용 할 수 없다.
   - href 속성은 하이퍼링크를 클릭했을 때 이동할 문서의 URL이나 문서의 책갈피를 지정한다.
   - target 속성은 하이퍼링크를 클릭했을 때 현재 윈도우 또는 새로운 윈도우에서 이동할지를 지정한다.
   - | 속성 값 | 설명 |
        |:-:|:-:|
        | _blank | 링크 내용이 새 창이나 새 탭에서 열린다. |
        | _self | target 속성의 기본 값으로 깅크가 있는 화면에서 열린다. |
        | _parent | 프레임을 사용 했을 때 링크 내용을 부모 프레임에 표시한다. |
        | _top | 프레임을 사용 했을 때 프레임에서 벗어나 링크 내용을 전체 화면으로 표시한다. |
   - #anchor 는 같은 페이지 안에서 특정 요소를 클릭 시 그 위치로 한 번에 이동시킨다.
   - link 속성은 link tag를 사용하며 문서와 외부 자원을 연결하기 위해 사용한다. `<head>` 위치에 정의하며 여러 자원을 연결 할 수 있다.
   - rel 속성은 현재 문서와 연결된 문서 사이의 연관관계를 지정하기 위해 사용한다.
   - href 속성은 연결된 문서의 위치를 지정하기 위해 사용한다.

<br><br>

7. 프레임 요소
   - 화면의 일부분에 다른 문서를 포함한다.
   - src 속성은 포함시킬 외부 문서의 경로를 지정한다. (URL도 가능)
   - height, width 속성은 프레임 사이즈를 지정한다.
   - ```html
        <body>
            <h2>iframe 연습</h2>
            iframe은 현재 문서에 다른 문서를 포함시켜 나타내고 싶을 때<br>
            사용하는 태그로 src속성에 나타날 문서명을 설정한다.<br>
            <br><br><br>
       <iframe src = "http://www.github.com" width = "500" height = "300" scrooling = "yes" align = "center" name = "f1"></iframe>
        </body>
        ```

<br><br>

8. form control 요소
   - 사용자로부터 데이터를 입력 받아 서버에서 처리하기 위한 용도로 사용된다.
   - 사용자는 HTML form에 적절한 데이터를 입력한 후 서버로 전송한다.
   - 사용자가 입력하기 위한 control 요소들은 모두 `<form>` tag 하위에 위치해야 서버로 전송된다.

| tag 명 | 설명 |
|:-:|:-:|
| `<form>` | 사용자에게 입력 받을 항목을 정의, form tag 내부에 여러개의 control 요소를 포함한다. |
| `<input>` | 텍스트 box, 체크 box, 라디오 버튼 등 사용자가 데이터를 입력 할 수 있도록 한다. |
| `<textarea>` | 여러 줄의 문자를 입력 할 수 있도록 한다. |
| `<button>` | 버튼을 표시한다. |
| `<select>` | select box를 표시한다. |
| `<optgroup>` | select box의 각 항목들을 그룹화 한다. |
| `<option>` | select box의 각 항목들을 정의한다. |
<br>

9. input 요소
    - type 속성에 따라 여러 가지 형태로 화면에 표시
    - id 속성은 여러번 사용된 폼 요소를 구분하기 위해서 사용한다.

| type | 설명 |
|:-:|:-:|
| text | 한 줄의 텍스트를 입력할 수 있는 텍스트 상자 |
| password | 비밀번호를 입력 할 수 있는 필드. ( ' * '로 표시) |
| search | 검색 상자 |
| tel | 전화번호를 입력 할 수 있는 필드 |
| url | URL 주소를 입력 할 수 있는 필드 |
| email | 메일 주소를 입력 할 수 있는 필드 |
| date | 사용자 지역을 기준으로 날짜 (년, 월, 일) |
| datetime | 국제 표준시로 설정된 날짜와 시간 (년, 월, 일, 시, 분, 초, 분할 초) |
| number | 숫자를 조절 할 수 있는 화살표 |
| radio | 주어진 항목에서 1개만 선택 할 수 있는 라디오 버튼 (단일선택) |
| file | 파일을 첨부 할 수 있는 버튼 |
| submit | 서버 전송 버튼 |
| button | 기능이 없는 버튼 |
<br><br>

10. 공간 분할 요소

| type | 설명 |
|:-:|:-:|
| div | block 형식으로 공간을 분할. 웹 사이트의 레이아웃을 만들 때 사용한다.<br>div 태그를 사용하여 각각의 블록(공간)을 알맞게 배치하고 CSS를 활용하여 스타일을 적용한다. |
| span | inline 형식으로 공간을 분할.<br>`<div>`와 `<p>` 태그와 함께 웹 페이지의 일부분에 스타일을 적용시키기 위해 사용한다. |

<br>

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fci92wo%2FbtqYN1gYE6l%2FHtvA9lQM1iG1B1nBpakLzK%2Fimg.jpg)

- div와 span을 여러개를 만들어 나란히 나열하였을 때, div는 자동 줄 바꿈이 일어나면서 세로로, span은 줄 바꿈이 일어나지 않고 가로로 나열한다.
- 동일한 문장을 감쌌을 때, div는 박스 형태로 영역이 설정되고 그 안에 정렬됩니다. 하지만 span은 줄 단위로 영역이 설정되기 때문에 박스 형태가 아닌 텍스트가 노출되는 영역만 포함한다.
- div의 margin은 4방향 모두 적용이 되며, span의 margin은 양옆으로만 적용한다.