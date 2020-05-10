## 3-way Handshake

> TCP는 3-way handshake 과정을 통해 연결을 설정하고 4-way handshake를 통해 해제한다.

**3-way Handshake란?**

TCP 3-way Handshake는 TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 **먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.**

3-way Handshake의 역할은, **양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하는 것이다.**

<img src="https://user-images.githubusercontent.com/40616436/81503765-6e7ace80-9320-11ea-82d6-49e00e900c36.png" alt="image" style="zoom:50%;" />

**3-way Handshake의 과정을 살펴보자.**

1. 클라이언트는 서버에 접속을 요청하는 SYN 패킷을 보낸다. 이 때 클라이언트는 SYN을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태가 된다.
2. 서버는 SYN 요청을 받고 클라이언트에게 요청을 수락한다는 ACK와 SYN Flag가 설정된 패킷을 발송하고 클라이언트가 다시 ACK로 응답하기를 기다린다. 이 때 서버는 SYN_RECEIVED 상태가 된다.
3. 클라이언트는 서버에게 ACK를 보낸 후부터는 연결이 이루어지고 데이터가 오가게 되는 것이다. 이 때 서버 상태는 ESTABLISHED가 된다.



 **4-way Handshake란?**



<img src="https://user-images.githubusercontent.com/40616436/81503940-7a1ac500-9321-11ea-9442-d1b86065188c.png" alt="image" style="zoom:50%;" />

**4-way Handshake 과정을 살펴보자.**

1. 클라이언트가 연결을 종료하겠다는 FIN Flag를 전송한다.
2. 서버에서는 FIN 패킷을 정상적으로 받았다는 ACK를 클라이언트에 전송해준다. 그 후 서버는 CLOSE-WAIT 상태로 빠져든다.
3. 연결을 종료한 후 서버는 클라이언트에게 FIN Flag를 전송해준다.
4. 서버로부터 전송된 FIN Flag를 받은 클라이언트는 확인을 알리는 ACK를 서버로 전송한 후, 일정 시간동안 TIME-WAIT 상태에 빠지게 된다.
5. 클라이언트로 부터 ACK를 받은 서버는 소켓을 Close하고 두 TCP간의 세션이 종료된다.
6. TIME-WAIT에 빠진 클라이언트는 서버로 부터 FIN을 수신하더라도, 일정시간동안 세션을 유지하며 도착하지 않은 패킷을 기다린다.



**연결 종료를 3-way Handshake 대신 4-way Handshake로 왜 해야하나?**

클라이언트가 데이터 전송을 마쳤다고 하더라도 서버는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 먼저 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문이다.



**TIME-WAIT는 왜?**

여기서 클라이언트가 서버로부터 FIN을 수신하더라도 일정시간 세션을 유지하는 이유는, 서버에서 FIN을 전송하기 전에 클라이언트가 전송한 패킷이 라우팅 지연이나 패킷 유실로 인한 재전송 등으로 인해 해당 ACK 패킷이 FIN 패킷보다 늦게 도착하는 상황을 대비해야하기 때문이다.

- 클라이언트에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 드롭되고 데이터는 유실될 것이다. 이러한 현상에 대비하여 클라이언트는 서버로부터 FIN을 수신하더라도 일정시간(default 240) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 되는데, 이 과정을 TIME_WAIT이다.



[https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake](https://mindnet.tistory.com/entry/네트워크-쉽게-이해하기-22편-TCP-3-WayHandshake-4-WayHandshake)



https://real-dongsoo7.tistory.com/73





