## DNS(Domain Name System)

> 개인 컴퓨터의 웹에서 [www.naver.com을](http://www.naver.com%EC%9D%84) 입력하면 어떤 과정을 통해 접속하는 지 살펴보자.

DNS는 IP 주소를 기억하는 것이 어렵기 때문에 DNS가 등장한 것이다. DNS의 과정을 간략히 말하면 웹에서 [www.naver.com을](http://www.naver.com%EC%9D%84) 입력하면 IP를 알아내기 위해 사용자에서 가장 가까운 곳에 위치한 DNS 서버에 [www.naver.com의](http://www.naver.com%EC%9D%98) IP주소를 문의하여 접근하게 되는 것이다.

DNS의 상세한 과정을 알기 전에 먼저 Host와 IP 주소에 대해서 알아보자.

---

#### **IP 주소와 Hosts의 개념**

-   Host : 인터넷에 연결된 컴퓨터 한대 한대
    
-   IP address : Host끼리 통신을 하기 위해 필요한 주소.
    

2대의 컴퓨터가 인터넷 통신을 위해 반드시 필요한 것은 IP 주소이다. 단, 모든 IP 주소를 기억하는 일은 너무 어려우므로 이것을 해결하기 위해 운영체제마다 hosts라는 파일이 존재한다. 이 파일에 IP와 도메인 이름을 저장해두면 도메인 이름을 통해 다른 host에 접근할 수 있다.

---

#### **Hosts 파일을 설정하는 방법**

**맥 OS의 경우 /etc/hosts**에 있다.

![image](https://user-images.githubusercontent.com/40616436/83998313-41f7b800-a99b-11ea-94cf-e1b389243465.png)

---

#### **도메인 이름과 보안**

Hosts 파일을 변조해서 평소에 사용하던 도메인 이름을 입력할 경우 다른 사이트로 접근할 수가 있다. 이 처럼 hosts 파일은ㅇ 보안에 취약하기 때문에 변조가 되지 않도록 주의해야한다.

예로, 은행 사이트를 동일하게 만들어서 hosts를 가짜 사이트로 변조한 후 개인 정보를 입력할 수 있게끔 하는 사례도있었다. 이런 일을 fishing이라고 하는데, 이런 변조 사항을 확인하기 위해서 전송 프로토콜이 https로 시작하는 사이트인지 확인해보면 된다.

---

#### **DNS의 내부 원리**

**_DNS Server_**

DNS Server는 IP 주소와 Domain 이름을 기억하는 기능과 Client가 Domain 이름을 물어보면 IP를 알려주는 기능을 갖고 있다.

만약 [www.naver.com이라는](http://www.naver.com%EC%9D%B4%EB%9D%BC%EB%8A%94) url로 이동하고자 한다면,

1.  로컬 DNS 서버에 해당 url이 등록되어 있는 지 확인 후 있으면 바로 IP주소를 알려준다.
2.  만약 IP 주소를 못찾을 시 **루트 DNS 서버**에게 문의 후 루트 DNS 서버는 최상위 도메인이 .com인 것을 확인 후 ".com"이 등록된 네임 서버의 IP Address를 전달한다. 즉 com 도메인을 관리하는 DNS 서버에 문의해보라고 로컬 DNS 서버에게 .com DNS 서버의 IP주소를 알려주는 것이다.
3.  로컬 DNS 서버는 이제 com DNS 서버에게 해당 url([www.naver.com](http://www.naver.com)) 을 문의한다. 역시나 com DNS 서버에는 해당 url([www.naver.com)이](http://www.naver.com)%EC%9D%B4) 없으므로 "naver.com"을 관리하는 DNS 서버에게 문의하도록 로컬 DNS 서버에게 naver.com DNS 서버의 IP주소를 알려준다.
4.  로컬 DNS 서버는 이제 naver.com DNS 서버에게 해당 url([www.naver.com)을](http://www.naver.com)%EC%9D%84) 문의한다. "naver.com 도메인을 관리하는 DNS 서버"에는 "[www.naver.com"에](http://www.naver.com"%EC%97%90) 대한 IP 주소가 있으므로 로컬 DNS 서버에게 해당 IP를 알려주는 것이다.

이와 같이 로컬 DNS 서버가 열 DNS 서버를 차례대로(Local DNS 서버 -> Root DNS 서버 -> com DNS 서버 -> naver.com DNS 서버) 물어보며 답을 찾는 과정을 **Recursive Query**라고 부른다.

![image](https://user-images.githubusercontent.com/40616436/84001472-a3bb2080-a9a1-11ea-9413-6c295a1c4a19.png)

실제로는 위와 같이 여러 단계를 거치게 되지만 초기의 해당 단계를 거치게 되면 그 이후로는 도메인에 대한 데이터베이스가 캐싱되어 위 단계를 거치지 않고 바로 응답이 가능하다.

그리고 좀 더 알면 좋은 것은,!

-   [http://www.naver.com/index.html](http://www.naver.com/index.html) : 이런 형식을 **URL**이라고 부른다.
-   [www.naver.com](http://www.naver.com) : 이런 형식을 **Host Name**이라고 부른다.
-   .com : 이것은 **Top-level Domain Name**이라고 부른다.
-   .naver.com : 이것은 **Second-level Domain Name**이라고 부른다.

![image](https://user-images.githubusercontent.com/40616436/84001753-3cea3700-a9a2-11ea-801a-2f4acaf3e3c9.png)

각각의 부분들을 담당하는 독자적인 Server Computer가 존재하는데,

Root는 Top-level을 담당하는 Server 목록과 IP를 알고 있으며, Top-level은 Second-level의 Server 목록과 IP를 알고 있고, Second-level은 sub 목록과 IP를 알고 있다.(즉, 상위 목록이 직속 하위 목록을 알고 있다.)

최초의 Root 네임 서버의 IP 주소에게 [www.naver.com을](http://www.naver.com%EC%9D%84) 물어보면 .com을 담당하는 Top-level을 알려주고, Top-level은 naver.com을 담당하는 Second-level을 알려주고, Second-level은 [www.naver.com을](http://www.naver.com%EC%9D%84) 담당하는 sub DNS Server에게 물어보며 sub가 해당 IP 주소를 알려주는 것이다.

---

#### **도메인 이름 등록 과정과 원리**

![image](https://user-images.githubusercontent.com/40616436/84002208-04972880-a9a3-11ea-9f95-d46177278940.png)

도메인 이름 등록 구조에서 최상위에 위치하는 것은 ICANN이라고 하는 비영리 단체이다. 이 단체는 전세계에 있는 IP 주소를 관리함과 동시에 Root Name Server의 관리자 역할을 하고 있다.

Root Name Server 밑에는 Registry라는 등록소가 존재하는데, 얘네는 Top-level domain(.com)을 관리하고 있다. 그 다음으로는 Registrar라고 하는 등록 대행자가 있는데, 등록 대행자는 등록자가 등록소에 등록하는 것을 등록해주는 대행역할을 하는 것이다.

만약 등록자가 example.com을 등록하고 싶으면 등록자는 등록대행자에게 도메인을 전달하고 등록대행자는 등록소에 해당 도메인을 등록하도록 전달한다. 하지만 기존에 도메인이 존재하면 등록할 수 없고 등록하기 위해서는 수수료를 지불해야 한다.

그리고 Root name server는 전세계에 있는 Top-level domain 서버들의 주소를 기억하고 있고, 우리의 도메인을 세팅하기 위해서는 authoritative name server를 구축해야 한다.

---

#### **도메인이 IP주소를 확인하는 방법**

_nslookup_

![image](https://user-images.githubusercontent.com/40616436/84004311-4e354280-a9a6-11ea-9bd9-6cc6301bd931.png)

_ping_

![image](https://user-images.githubusercontent.com/40616436/84004396-7329b580-a9a6-11ea-831e-d3c5b4332cca.png)

---

[

DNS 기본 동작 설명

DNS 기본 동작 설명 DNS Basic Operation December 12, 2011 | By 유창모 (cmyoo@netmanias.com)

www.netmanias.com



](https://www.netmanias.com/ko/post/blog/5353/dns/dns-basic-operation)

[

Domain Name System(DNS)의 이해

생활코딩 WEB2 - Domain Name System을 수강하며 내용을 정리한 글입니다. 이 수업을 들으니 제가 얼핏 알았던 개념을 확실하게 알 수 있었고, 대표적인 면접 문제인 브라우저의 URL 입력창에 www.naver.com

zzsza.github.io



](https://zzsza.github.io/development/2018/04/16/domain-name-system/)
