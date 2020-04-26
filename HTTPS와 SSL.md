## HTTPS와 SSL

**HTTPS vs HTTP**

- HTTP는 Hypertext Transfer Protocol의 약자이다.
  - 즉, HTML을 전송하기 위한 방식이다.
- HTTPS와 HTTP의 차이를 살펴보면 둘 다 HTML을 전송하기 위한 방식이라는 측면은 동일한데, S에서 차이가 판가름된다.
- HTTPS에서 마지막 S는 Over Secure Socket Layer의 약자로 보안이 강화된 HTTP라는 것을 짐작할 수 있다.
  - **HTTPS는 HTTP와 다르게 보안 장치가 덧붙여 있는 것으로 볼 수 있다.**
- HTTPS를 이용하여 메시지를 전송하게 되면 제 3자는 해당 메시지를 감청하거나 조작할 수 없게 한다. 
  - Ex. 로그인을 위해서 서버로 비밀번호를 전송할 때 HTTP를 사용하면 메시지를 중간에 감청할 수 있다.
  - Ex. 중요 문서 같은 것을 전송하고자할 때 중간에서 데이터를 변조할 수 있는 일이 일어날 수 있다.



**HTTPS와 SSL**

- SSL 위에서 HTTPS가 동작한다.

  <img src="https://user-images.githubusercontent.com/40616436/80310959-2b950300-8818-11ea-8d4a-10be470d08ce.png" alt="image" style="zoom:50%;" />

- 그림을 살펴보면 SSL은 HTTP 보다 더 포괄적인 것이고, SSL 통신 방법 위에서 동작하는 서비스 중 하나가 HTTP이다.

- HTTP가 SSL을 이용하게 되면 그것이 바로 HTTPS가 되는 것이다.



**SSL과 TLS**

- SSL : 사용자의 정보를 더 안전하게 주고받기 위해 나타난 프로토콜
- TLS : SSL이 폭넓게 사용되다가 표준화 기구인 IETF의 관리로 변경되면서 TLS로 바뀐 것이다.
- 결국, SSL과 TLS은 같은 것으로 볼 수 있다.



