# 브라우저에 URL을 입력하면 생기는 일!!

인터넷 브라우저에 URL을 입력하면 어떻게 될까?

먼저 URL을 받은 브라우저는 일단 이 URL의 구조를 해석한다.
어떤 프로토콜로, 어느 도메인으로, 어떤 포트로 보낼지 해석하게 되는것이다.(이를 URL 파싱이라 부른다.)

기본적으로 URL의 구조는 다음과 같다.
![url structure](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdfjElB%2FbtqDH2sKASg%2F236MABv8iJyBDUkm4TdhkK%2Fimg.png)

어떤 프로토콜을 통해 해당 URL에 요청하고, 어떤 URl로 요청하고, 어떤 포트로 요청할 것인지 브라우저에서 각각의 프로토콜, URL, 포트를 해석하여 분석한다.

<br>

만약 포트를 입력하지 않았다면?!
> 브라우저에서 설정된 기본값을 이용해 요청하게 된다. <br>
> HTTP라면 80 포트를, HTTPS라면 443 포트를 기본값으로 요청한다.


<br>

잠깐 그전에!! HSTS에 대해 알아보고 가자.

HSTS(HTTP Strit transport security)란? <br>

>HTTP 대신 HTTPS만을 사용하여 통신해야한다고 웹사이트가 브라우저에게 알리는 보안기능이다.

그 후 HTTP로 요청이 왔다면 HTTP 응답 헤더에 `"Strict Transport Security"`라는 필드를 포함하여 응답하고 이를 확인한 브라우저는 해당 서버에 요청할 때 HTTPS만을 통해 통신하게 된다. 그리고 자신의 HSTS캐시에 해당 URL을 저장하는데 이를 HSTS 목록이라고 부른다.

이를 통해 브라우저에서는 이 HSTS 목록 조회를 통해 해당 요청을 HTTPS로 보낼지 판단한다.
HSTS 목록에 해당 URL이 존재한다면 명시적으로 HTTP를 통해 요청한다 해도 브라우저가 이를 HTTPS로 요청한다.

<br>

다음은 URL을 IP주소로 변환한다.

`www.daum.net` 이라는 주소로는 컴퓨터끼리 통신을 할 수 없다. 이를 인터넷 상에서 컴퓨터가 읽을 수 있는 IP주소로 변환해야 서로 통신이 가능하다.

브라우저에서 자신의 로컬 hosts 파일과 브라우저 캐시에 해당 URL이 존재하는지 확인한다. 존재하지 않는다면 도메인 주소를 IP주소로 변환해주는 DNS(Domain Name System) 서버에 요청하여 해당 URL을 IP주소로 변환한다.

> DNS 서버로 요청하는 과정
1. Local DNS에 해당 URL 주소의 IP주소를 요청한다.
2. Local DNS에 해당 IP주소가 존재한다면 이를 응답하고, 없다면 다른 DNS 서버와 통신한다. root DNS 서버에 해당 URL의 IP주소를 요청한다.
3. 만약 root DNS 서버에 해당 IP주소가 없다면 하위 DNS 서버에 요청하라고 응답한다. 이 응답을 받은 Local DNS는 .net 도메인을 관리하는 DNS 서버에 같은 내용을 요청한다.
4. .net DNS 서버에 해당 IP주소가 없다면 하위 DNS 서버에 요청하라고 응답한다. 이 응답을 받은 Local DNS는 daum.net 도메인을 관리하는 DNS 서버에 같은 내용을 요청한다.
5. daum.net DNS 서버에서 IP주소를 응답받은 Local DNS는 해당 IP주소를 캐싱하고 응답한다.
   
<br>

한줄로 요약하자면,
- 요청하는 DNS 서버를 조금씩 늘려나가면서 해당 URL의 IP주소를 찾는다.

라고 할 수 있겠다.

<br>

DNS서버에게 IP주소를 받았다면, 이제 해당 서버로 요청을 보낸다. IP주소를 임시로 `10.20.30.6`으로 가정해볼까 한다. 이 IP주소로 가야 하는 것은 알지만 어떻게 가야 할지 경로는 알 수 없다. 이 요청이 네트워크를 타고 어떻게 이동 할지는 네트워크 장비인 라우터의 라우팅을 통해 이루어진다.

![route img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMmiKa%2FbtqDJNaoI1G%2Fcu3Pwo3ugTC6EDyVD2PNA1%2Fimg.png)

라우터에서는 라우팅 테이블을 통해 해당 요청이 어떤 경로를 통해 가야 할지 경로를 지정해준다. 이를 통해 요청은 `10.20.30.6`을 찾아간다.

<br>

실질적인 통신을 하기 위해서는 논리 주소인 IP주소를 물리 주소인 MAC주소로 변환해야 한다. 이를 위해 해당 네트워크 내에서 ARP(Address Resolution Protocol, MAC 주소와 IP 주소를 서로 연결하는 용도로 사용)를 브로드 캐스팅한다. 해당 IP주소를 가지고 있는 노드는 자신의 MAC주소를 응답한다.

<br>

이제 대상 서버와 통신하기 위해 TCP 소켓 연결을 진행한다. 소켓 연결은 3-way-handshake라는 과정을 통해 이루어진다. 이 과정은 마치 전화를 거는 것과 유사하다. 서버에게 전화를 걸고, 서버는 해당 전화를 확인하고 전화를 받는다. 그리고 전화를 건 사람은 말한다. "여보세요"라고 하는 것처럼.

하지만 지금 하는 요청은 HTTPS 요청이다. 그렇기 때문에 서로 암호화 통신을 위한 TLS 핸드쉐이킹이 추가 된다. 이를 통해 서버와 클라이언트는 암호화 통신을 진행할 수 있다.

![3-way-handshake](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAH0pw%2FbtqDHtEcJlG%2FKvi1fTEjMO6UGPaRoTVy8K%2Fimg.png)

약간의 상황극을 도입한다면 이렇게 된다.

> 클라이언트 : 서버야 안녕?! <br>
> 서버 : 어.. 안녕, 클라이언트!! <br>
> 클라이언트 : 서버야 우리 연결하자! <br>
> 서버 : 그.. 그래..!! <br>

<br>

이제 연결이 확정되었으니 드디어 해당 URL 페이지를 달라고 서버에게 요청한다. 서버에서 해당 요청을 받고, 이 요청을 수락할 수 있는지 검사한다. 그리고 서버는 이 요청에 대한 응답을 생성하여 브라우저에게 전달한다.

<br>

서버에서 응답한 내용은 HTML, CSS, Javascript 등으로 이루어져 있다.

이를 브라우저에서 해석하여 그려준다. 각종 텍스트를 정해진 형식으로 해석하여 우리가 원하는 URL 페이지가 그려진다.