# HTML 폼과 유효성 검사

## 폼
폼이란 위키백과에 따르면
> 폼, 입력 폼은 웹 프로그래밍 기술의 하나이다. 클라이언트가 정보를 입력·선택하고, 웹 서버 등의 폼을 처리하는 에이전트로 제출하기 위한 기구이다.

```html
    <body>
        <form action="" method="" enctype="">
            <input type="text" name="test"> <br><br>
            <input type="submit">
        </form>  
    </body>
```

HTML의 폼은 위의 코드와 같이 클라이언트에게 보낼 input 태그를 감싸는 형태로 작성된다.

form 태그의 속성인 action은 데이터를 받아서 보낼 url 주소를 정한다.
method는 데이터를 GET, POST, PUT 등 어떤 방식으로 보낼지 정한다.
enctype은 데이터의 인코딩 방식을 정한다.

이렇게 form은 자신의 태그 안에 있는 input 태그들의 정보들을 모아 action에 설정된 url로 method에 정의된 방식으로 데이터를 enctype에 따라 보내게 된다.
이 코드는 첫번째 input인 test에 적은 값을 url로 보낸다. 하지만 action에 url을 지정하지 않았기에 아무일도 일어나지 않는다.

<br>

---

## 폼 예시

```html
    <form action="" method="" enctype="">
        <input type="text" id="tex" required> <br><br>
        <input type="checkbox" id="check" > Check <br>
        <input type="checkbox" id="check" > Check2 <br>
        <input type="radio" value="yes" name="question"> Yes <br>
        <input type="radio" value="no" name="question"> No <br>
        <input type="submit">
    </form>
```

이 코드를 브라우저에서 보면

![img](https://media.vlpt.us/images/goban/post/7defae18-ca94-4b65-aa8e-84b9647b90ba/webForm1.PNG)

이렇게 화면이 나타난다.
radio type input에 "question"이라는 name을 중복으로 줬기 때문에, YES·NO 중 하나만 선택 가능하다.

![img](https://media.vlpt.us/images/goban/post/253b0e8a-d279-474a-9938-320e999139dd/webForm2.PNG)

text type input에 required 속성을 주면 아무값도 입력을 하지 않을 경우, 입력칸을 작성하라는 문구가 뜨며 제출되지 않는다.

<br>

---

## 유효성 검사

유효성 검사를 알아보기 전에, 웹 표준이란 무엇일까
> 웹 표준은 WWW(World Wide Web)의 측면을 서술하고 정의하는 공식 표준이나 다른 기술 규격을 가리키는 일반적인 용어이다. 최근에 이 용어는 웹 사이트를 작성하는 데 중요도가 높아지고 있으며 웹 디자인, 개발과 관계가 있다.

즉, 웹 표준을 지킨다는 것은 어느 브라우저를 사용하는지 여부에 상관없이 그 웹페이지가 똑같이 보이고 정상적으로 작동한다는 것이다.

[http://validator.w3.org/](http://validator.w3.org/)

이곳에서 웹 유효성 검사를 해준다. 여기에서는 웹 표준성, 웹 호환성, 웹 접근성을 고려하여 검사를 해준다.

![img](https://media.vlpt.us/images/goban/post/b3a7681c-27f4-4941-bc94-8f65a3fe25ee/W3Cmark.jpeg)

검사를 통과하면 사이트에 이러한 마크를 달 수 있다. 웹 표준을 지키도록 사이트를 만들 때 꼭 검사를 해보자.