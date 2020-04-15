## HTTP 1.0 vs 1.1

**HTTP**

- HTTP는 HyperText Transfer Protocol의 약자로서, 인터넷에서 주로 사용하는 데이터를 송/수신 하기 위한 프로토콜이다.
- 최초 HTTP를 이용한 데이터 송수신은 GET 방시의 HTML을 위주(문서 표현)로 이루어졌으나, 추후에는 여러 메소드 및 미디어 타입이 추가됨에 따라 확장을 했다.



**HTTP 1.0**

- HTTP는 원래 0.9v 부터 시작되었다고 하지만, 사실상 1.0버전이 상용화 되어 1996년부터 사용되기 시작했다.
- HTTP 1.0은 단순히 open/operation/close 방식을 취하고 있는 단순한 구조이다.
- TCP Connection당 하나의 URL만 fetch하며, 매번 request/response가 끝나면 연결이 끊기므로 필요할 때마다 다시 연결해야하는 단점이 있어 속도가 현저히 느리다.
- URL의 크기가 작고 한번에 가져올 수 있는 데이터의 양이 제한되어 있다.



**HTTP 1.0의 단점**

- HTTP 1.0에서는 open/close를 위한 flow의 제한으로 대역폭이 적게 할당되어 연결되는데, 이로 인해 congestion information이 자주 발생하고 disconnect가 반복적으로 나타나게 된다.
- 반복되는 disconnect 현상으로 인해 한 서버에 계속해서 접속을 시도하게 되면 과부하가 걸리고 성능이 떨어지게 되는 문제가 발생한다.
- **이런 문제를 해결하기 위해 HTTP 1.1이 등장한 것이다.**



**HTTP 1.1**

- HTTP의 인터넷에서 impact를 줄이고 cache를 두어 인터넷 프로토콜 수행이 빠르게 될 수 있도록 성능을 향상하고 있다.
- multiple request에 대한 처리가 가능하고 request/response가 파이프라인 방식으로 진행이 가능하다.



**HTTP 1.0 vs HTTP 1.1**

<img src="https://user-images.githubusercontent.com/40616436/79342851-9d439600-7f68-11ea-9a1c-80782d6cbb6e.png" alt="image" style="zoom:50%;" />

- **cache**
  - HTTP 1.0에서는 주로 Last-Modified, 즉 Dates에만 의존하여 cache를 다루지만, HTTP 1.1에서는 1.0에서 지원해주는 기능 이외에 client에서 사용 가능한 미디어 타입을 명시하여 지원해주고 있다.
    - 또한, HTTP 1.1에서는 cache의 내용이 적절한지의 여부를 판단하기 위해 if-Match, if-None-Match를 사용하고 있다.
- **Response Header**
  - HTTP 1.0에서는 location과 server 및 WWW-Authenticate를 이용하고 있다.
  - HTTP 1.1에서는 client에서 request를 보낸 후 server에서 응답 메시지를 생성하기 까지의 시간을 나타내는 age가 도잆되었다.
- **HTTP Method**
  - HTTP 1.0에서는 GET, HEAD, POST의 method가 사용된다.
    - GET : Request-URI에서 지정한 정보를 Entity Body로 전달해달라는 요청
    - HEAD : Header의 정보만 요구
    - POST : Request 메시지의 body에 포함된 자원을 Request-URI로 넘겨주는 경우 사용
  - HTTP 1.1에서는 OPTION, PUT, DELETE, TRACE의 method가 사용된다.
    - OPTION : 통신과 관련된 선택사항들에 대한 정보를 요구하는 경우
    - PUT : Request 메시지에 포함되어 있는 data를 지정한 Request-URI로 저장하기 위함
    - DELETE : 특정 resource를 지우기 위함
    - TRACE : 최종 destination까지의 Loopback을 테스트하기 위함



**정리**

- HTTP 1.0은 매번 필요시에만 connection을 open/close하는 기능을 해결하기 위해, HTTP 1.1을 도입하여 HTTP 1.1에서는 multiple connection을 open할 수 있도록 한다.
- 몇몇 entity의 경우에는 그 길이를 몰라 이를 해결하기 위해서, HTTP 1.1에서는 chunked encoding을 도입하여 해결하고 있다.
- 또한, HTTP 1.1에서는 전송한 data를 압축하여 전달하므로 data의 양을 줄이고 있다.