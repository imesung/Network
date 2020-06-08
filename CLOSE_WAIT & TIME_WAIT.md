## CLOSE_WAIT & TIME_WAIT

> 대고객 서비스를 운영하다 보면 매우 많은 트래픽이 발생하고 웹 서버가 제대로 응답하지 못하는 경우가 있는데, 이는 CLOSE_WAIT이기 때문이다.

시스템이 느려지거나 멈추는 현상 - Hang up과 Slowdown

- Hang up
  - Server의 Instance는 실행되고 있으나 아무런 응답이 없는 상황을 말한다.
- Slowdown
  - Server의 Instance의 response time이 급격히 떨어지는 상태를 말한다.

Hang up이나 Slowdown의 현상은 대부분 Network, User Application, WEB/WAS(Servlet Engine), JVM, DBMS 다섯가지 요소 중 하나 이상의 병목 현상으로 인해서 발생하게 된다.

---

TCP 연결이 해제 될때는 FIN 패킷, ACK 패킷을 한 번씩 주고 받으면서 연결을 종료하게 된다. 이 때, Close 요청을 먼저한 주체가 누구냐에 따라 Active Close와 Passive Close 대상이 달라진다.

Server와 Client로 보면 안 된다. Server가 먼저 연결 해제요청을 할 수도 있고, Client가 먼저 연결 해제요청을 할 수도 잇다.

- Active Close : TCP 연결 해제를 요청한 대상
- Passive Close : TCP 연결 해제를 수신한 대상

<img src="https://user-images.githubusercontent.com/40616436/84006601-fa2c5d00-a9a9-11ea-9c81-943ddeb5b1ef.png" alt="image" style="zoom:50%;" />

FIN 패킷의 의미는 '더 이상 보낼 데이터가 없으니 연결을 해제하고 싶다'라는 의미로 볼 수 있고, ACK 패킷의 의미는 '확인완료'라는 의미로 볼 수 있다.

---

**CLOSE_WAIT**

FIN 요청을 수신한 Passive Close는 CLOSE_WAIT 상태로 변경된다. 이후, Passive Close는 즉시 Close를 실행하지 않고, TCP 포트를 사용 중인 프로세스에게 종료 명령을 내리고 Close 명령을 실행할 때가지 대가히게 된다. 즉 CLOSE_WAIT는 Close명령을 실행할 때가지 기다리는 상태를 말한다.

---

**TIME_WAIT**

Active Close 대상이 FIN 패킷에 대한 ACK 응답을 송신한 후, 즉시 Disconnect를 하지 않는다. 60초 정도 뒤에 실제 연결을 Disconnect 하게 된다.

