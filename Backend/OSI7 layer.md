# OSI(Open System Interconnection) 7 Layer

## 백엔드 통신을 위한 7 레이어에는 다음과 같이 구성되어 있다.

1. 물리 (Physical) - 물리적 전송 시그널 (전기신호, 전파 등)
2. 데이터 링크 - Frame (Mac Address)
3. 네트워크 - Packet (IP)
4. 전송 (Transport) - TCP / UDP - Segment (Port)
5. 세션 - Connection 맺기, TLS
6. 표현 (Presentation) - Encoding / Serialization
7. 애플리케이션 - HTTP / web-RPC / gRPC / FTP 등

## 각 레이어별로 전송 과정

7 - POST 요청을 JSON데이터를 바디에 넣어 HTTPS 서버로 전송

6 - 요청을 byte string으로 직렬화

5 - TCP 커넥션, session찾아보고 

- 없네? 그러면 연결 맺기 (3way handshake) (TLS규약 따름)
- 있으면 데이터 담아서 서버에 전송

4 - TCP 연결 맺기

- 클라이언트는 서버에게 TCP연결을 맺기 위해 SYN요청을 서버의 443포트로 보냄
- 똑같이 레이어 4, 3, 2, 1~~ 1,2,3,4서버의 레이어 5로 가서 SYN요청 확인
- 더 높은 레이어로 가지 않고 서버는 다시 클라이언트에게 ACK데이터 전송
- 클라이언트 ACK확인하여 연결 맺고 다시 서버에게 ACK전송
- 서버는 클라이언트가 보낸 ACK 확인

4 - 연결이 맺은 경우 Source Port - Data - Destination Port 이렇게 데이터를 감싸고 보냄

3 - Source IP - Data - Dest IP 로 감싸서 패킷이 됨

2 - 각 패킷은 Source Mac - Data - Dest Mac Addr로 감싸져서 단일 프레임이 됨

1 - 프레임은 비트단위로 물리적인 신호로 변환되어 전송

## 각 레이어별로 수신 과정

1 - 물리적 신호는 비트로 변환됨

2 - 비트는 프레임으로 조립됨 (S Mac - Data - Dest Mac)

3 - 프레임은 IP 패킷으로 조립됨 (S IP - Data - D IP)

4 - IP패킷은 TCP 세그먼크로 조립됨 (S Port - Data - D Port)

- SYN 세그먼트면 더 위로 안올라가고 ACK보내서 연결맺음

5 - 세션이 있으면 커넥션이 연결된 것 (무상태의 경우 세션레이어가 존재하지 않을수도)

- 오직 3way handshake가 잘 끝났을때만 여기까지 올라옴 (TCP의 경우만..)

6 - 표현층에는 flat byte를 JSON과 같이 원래 데이터로 역직렬화가 이루어짐

7 - 여기서 역직렬화된 데이터를 통해 실제 비즈니스 로직이 이루어짐