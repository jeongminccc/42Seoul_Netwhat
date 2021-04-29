# 1. 소개 
Netwhat will allow you to discover the network and to learn about its inner workings.  
This will allow you to understand how some things work that you already use in your  
everyday life.  

# 2. 학습 내용

# What is IP address

## IP
Internet Protocol의 준말이며, 인터넷 사용에 있어 데이터(패킷)를 주고받는 것과 관련된 규약, 즉 프로토콜 중 하나이다. 패킷이 어떤 식으로 작성 되어야 하고, 주소를 어떻게 탐색할지에 대한 룰을 정해놓은 것이라고 볼 수 있다.  

TCP가 데이터의 효율적인 전달(쪼개고 합치기)과 관련된 규칙을 담당한다면, IP는 이런 데이터를 어떻게 어디로 전달하면 되는지와 관련된 규칙을 담당한다.  

## IP 주소
이런 프로토콜 안에서 데이터가 전송되어야 하는 곳의 주소를 지칭한다. 네트워크마다 고유의 주소가 있다.  

### IPv4 & IPv6
IPv4란 8비트 4개의 조합, 32비트로 이루어진 표기방식을 말한다.
```
255.255.255.255  
192.168.0.1  
```

IPv4의 네트워크 주소 조합 개수는 총 42억개인데, 인터넷의 발달로 인해 부족한 IP주소때문에, 더 많은 조합이 가능한 IPv6로 옮기고 있는 추세이다.  

## 클래스
클래스는 IP주소의 타입이다. 인터넷 초창기에는 네트워크를 개인들에게 공개할 생각이 없었고, 그런 이유로 특정 용도에 따라 클래스를 구분 지어 놓은 역사가 있다고 한다.

- __A 클래스__ 의 IP주소는 첫번째 숫자가(옥텟) 1 ~ 126. 사설 IP는 10.0.0.0 ~ 10.255.255.255
- __B 클래스__ 의 IP주소는 첫번째 숫자가(옥텟) 128 ~ 191. 사설 IP는 172.16.0.0 ~ 172.31.255.255
- __C 클래스__ 의 IP주소는 첫번쨰 숫자가(옥텟) 192 ~ 223. 사설 IP는 192.168.0.0 ~ 192.168.255.255  

__D와 E클래스__ 는 멀티캐스팅이나 정부 차원에서 사용하는 __특수한 클래스__ 이다.  
그리고 우리가 __localhost__ 라고 지칭하는 127.0.0.1에서 127의 경우 엄밀히 따지자면 A 클래스에 속하겠지만, 보통은 자기 자신이라고 참고하면 된다. 이를 __local loopback__ 이라고 부른다.  

IP 주소의 클래스 구분은 단순히 첫 번쨰 옥텟의 숫자 범위 뿐만이 아니라 어디까지가 네트워크 id이고 호스트 영역인지를 구분하는 기준이 되기도 한다.  

```
Class A -> 네트워크.호스트.호스트.호스트  
Class B -> 네트워크.네트워크.호스트.호스트  
Class C -> 네트워크.네트워크.네트워크.호스트
```

이렇기에 자연스럽게 클래스 A의 네트워크는 24bits 조합만큼의 호스트를 포함할 수 있기 때문에 규모가 큰 기관에서 주로 사용했던 것으로 이해할 수 있다.

## 사설 & 공인 IP

- 공인 IP 주소 : 어떠한 네트워크가 갖는 고유한 주소.  __Router 주소__
- 사설 IP 주소 : 하나의 네트워크 안에서 주어지는 상대적인 주소. __Router에 연결된 각각의 기기의 주소__ 

즉 우리 집에는 하나의 네트워크만이 연결되지만, 그 안에서 많은 기기가 고유한 주소를 가친채로 그 네트워크를 통해 다른 네트워크와 소통할 수 있다. (다른 집의 네트워크가 내 컴퓨터와 동일한 __사설 IP주소__ 를 가질 수 있다)  

위에서 설명한 사설 IP주소의 범위는 일반적으로 사설 IP로 활용할 수 있도록 각각의 클래스에서 공인 IP로 사용되지 않게 분리해둔 주소이다.  
`192.168.0 으로 시작하는 주소`

## 포트 & NAT

### NAT(Network Address translation)
보통 하나의 집에서 하나의 와이파이를 사용하기 때문에, 집안의 모든 기기는 같은 공인 IP주소를 가지게 된다. 이렇게 여러 기기가 하나의 네트워크(라우터)에 연결되어 있는 것을 LAN(Local-Area Network)라고 부른다. 그리고 라우터를 통해 연결되는 외부의 네트워크들이 모여 있는 것을 WAN(Wide-Area Network)라고 부른다. (결국 인터넷은 거대한 WAN이다)  

그리고 WAN을 통해 우리집 라우터의 공인 IP주소로 전송되는 데이터가 있을때, 정확하게 각각의 기기에 매핑이 되도록 해주는 것을 __NAT(Network Address Translation)__ 이라고 한다.  

### 포트
각각의 IP는 여러 포트를 가지고 있다. 인터넷에서 무언가 들어올 수 있는 통로가 각각의 컴퓨터(혹은 기기)마다 여러개 있다고 생각할 수 있다. 그리고 우리의 Router 또한 포트가 여러개 있는데, 이때 우리가 사용하는 Router의 특정 포트 번호로 들어오는 데이터를 LAN에 연결된 다른 IP주소의 특정 포트로 보내도록 지시하는 것이 __포트 포워딩__ 이다.  

### 게이트웨이 Gateway
게이트웨이는 다른 네트워크로 통하는 __Access Point__ 라고 이해할 수 있다. Router가 있다면, 그 Router의 IP주소를 의미하게 된다. 정확히는 Router의 사설 IP주소일 것이고, 기본적으로는 가능한 호스트 중 가장 첫번째이다. 만약 내 컴퓨터의 사설 IP주소가 192.168.0.4라고 했을 때, Defalut Gateway는 192.168.0.1인 것이다. Defalut Gateway를 주소창에 치고 접속하면 라우터 설정으로 넘어가게 된다.

# What is a Netmask

네트워크의 주소 부분의 비트를 1로 치환한 것이다.  

사용중인 IP주소가 있을떄, 첫 옥텟의 숫자를 보고 Class를 알아낸 뒤, 그에 맞는 Netmask를 만들고 이를 IP주소와 AND 연산하면 __네트워크 주소를 얻을 수 있다.__

# What is the subnet of an IP with Netmask

## 서브넷
말 그대로 하나의 네트워크를 쪼개 만든 네트워크이다. 하나의 네트워크는 또 한번 여러 서브넷으로 나뉠 수 있는데, 네트워크를 조각내어 관리한다면 다음과 같은 장점들이 존재한다.  

- 보안
- 관리
- 속도 & 성능

회사 안에서 하나의 네트워크로 모든 기기가 연결되어 있다고 가정해 보자. 어떤 부서 떄문에 네트워크를 통제해야 할 때, 모두 하나의 네트워크 안에 있으니 모두가 영향을 받게 된다.  

그런데 부서마다 네트워크를 일정부분 떼어주고 알아서 __관리__ 하게 한다면, 관리도 편할뿐 더러 서로 영향을 주지 않고 접속하지 못하니 부서 간의 __보안__ 도 보장이 되는 원리이다.  

```
그냥 새로운 네트워크를 할당받으면 되지 않을까?  
-> 결국 IPv4의 고갈과도 관련이 있다. 앞서 설명한 LAN, NAT 또한 부족한 IPv4 주소를 어떻게든 모든 기기가 사용하여 인터넷에 연결하기 위한 방법 중 하나이듯, 서브넷도 마찬가지 이다.  
```

## 서브넷 마스크
IP주소를 읽을 때 어디까지가 네트워크 아이디인지를 알려주는 척도가 된다.

```
192.168.0.1 (주소)  
255.255.255.0 (Class C 서브넷 마스크)  

(A면 255.0.0.0, B면 255.255.0.0)
```

하지만 이렇게 하게된다면 낭비되는 주소가 생긴다는 문제가 발생하는데, Class C의 경우 대략 250개 정도의 호스트를 보유할 수 있는데 어떠한 기관에서 100개 정도의 호스트만 감당할 수 있는 네트워크를 필요로 한다고 가정해 보자. 클래스로만 구분된 네트워크로만 할당을 하자니 제일 작은 클래스 C의 호스트 수는 벌써 200개가 넘고, 낭비가 발생하게 된다.  

이런 발상에서 시작한 것이 __CIDR(Classless Inter-Domain Routing)__ 이다.  

# What is the broadcast address of a subnet

## Broadcast
- 같은 네트워크 상의 모든 PC에 데이터를 주는 방식  
- 주로 MAC주소는 모르고 IP주소만 알고있을 때 PC의 __MAC주소를 알기 위해__ -> "이 네트워크 안에 이런 IP주소 가진 PC는 응답해주세요" 같은 느낌  
- 서버가 다수의 클라이언트에 서비스 하기 위해서 사용하기도 함  

```
- Unicast : 1:1로 데이터를 전달하는 통신 방식
- Multicast : 다수가 있는 네트워크에서 그 중 일부하고만 통신할 떄 사용
```

# What are the different ways to represent an ip address with the Netmask

## CIDR
Classless Inter-Domain Routing, 클래스로만 구분된 네트워크의 한계를 극복하기 위한 수단으로 개발되었다. 기존의 클래스만을 이용하면 서브넷 마스크는 8자리 단위로만 끊기게 되어 낭비되는 것이 많은데, CIDR을 이용하면 네트워크 ID로 사용하는 범위를 자유롭게 표기할 수 있게 되어 네트워크를 조금 더 세부적인 단위로 쪼갤 수 있다. 서브넷과 CIDR은 결국 네트워크를 자른다는 의미로 같은 것으로 볼 수 있고, 다만 CIDR은 특수한 표기법을 따른다.  

```
192.168.0.1/24 (CIDR 방식)  
```

슬래시 뒤에 적힌 숫자는 몇 개까지의 bit이 네트워크 id인지 의미하게 된다. 기존의 클래스로만 구분한다면 뒤에 따라오는 숫자는 8, 16, 24 정도 였겠지만 CIDR에서는 17, 25등 자유롭게 표기 할 수 있다.  

/15의 경우 호스트 범위가 어떻게 될까?
```
158.167.18.156/15

-> 앞의 15 비트만 1과 AND 연산

10011110.10100110.00000000.00000001 (158.166.0.1)
~
10011110.10100110.00000000.00000001 (158.167.255.254)
```

- 호스트 영역이 모두 0 (158.166.0.0)인 주소는 __네트워크 자체의 주소__ 이다.  
- 호스트 영역이 모두 1 (158.167.255.255)인 주소는 __브로드 캐스트 주소__ 이다.  

브로드캐스트 주소란 해당 네트워크 모든 호스트에게 정보를 전달할 때 사용되는 주소이다.

# What are the differences between public and private IPs

## 사설 & 공인 IP

- 공인 IP 주소 : 어떠한 네트워크가 갖는 고유한 주소.  __Router 주소__
- 사설 IP 주소 : 하나의 네트워크 안에서 주어지는 상대적인 주소. __Router에 연결된 각각의 기기의 주소__ 

즉 우리 집에는 하나의 네트워크만이 연결되지만, 그 안에서 많은 기기가 고유한 주소를 가친채로 그 네트워크를 통해 다른 네트워크와 소통할 수 있다. (다른 집의 네트워크가 내 컴퓨터와 동일한 __사설 IP주소__ 를 가질 수 있다)  

위에서 설명한 사설 IP주소의 범위는 일반적으로 사설 IP로 활용할 수 있도록 각각의 클래스에서 공인 IP로 사용되지 않게 분리해둔 주소이다.  
`192.168.0 으로 시작하는 주소`

# What is a class of IP addresses

## 클래스
클래스는 IP주소의 타입이다. 인터넷 초창기에는 네트워크를 개인들에게 공개할 생각이 없었고, 그런 이유로 특정 용도에 따라 클래스를 구분 지어 놓은 역사가 있다고 한다.

- __A 클래스__ 의 IP주소는 첫번째 숫자가(옥텟) 1 ~ 126. 사설 IP는 10.0.0.0 ~ 10.255.255.255
- __B 클래스__ 의 IP주소는 첫번째 숫자가(옥텟) 128 ~ 191. 사설 IP는 172.16.0.0 ~ 172.31.255.255
- __C 클래스__ 의 IP주소는 첫번쨰 숫자가(옥텟) 192 ~ 223. 사설 IP는 192.168.0.0 ~ 192.168.255.255  

__D와 E클래스__ 는 멀티캐스팅이나 정부 차원에서 사용하는 __특수한 클래스__ 이다.  
그리고 우리가 __localhost__ 라고 지칭하는 127.0.0.1에서 127의 경우 엄밀히 따지자면 A 클래스에 속하겠지만, 보통은 자기 자신이라고 참고하면 된다. 이를 __local loopback__ 이라고 부른다.  

IP 주소의 클래스 구분은 단순히 첫 번쨰 옥텟의 숫자 범위 뿐만이 아니라 어디까지가 네트워크 id이고 호스트 영역인지를 구분하는 기준이 되기도 한다.  

```
Class A -> 네트워크.호스트.호스트.호스트  
Class B -> 네트워크.네트워크.호스트.호스트  
Class C -> 네트워크.네트워크.네트워크.호스트
```

이렇기에 자연스럽게 클래스 A의 네트워크는 24bits 조합만큼의 호스트를 포함할 수 있기 때문에 규모가 큰 기관에서 주로 사용했던 것으로 이해할 수 있다.

# What is TCP

## TCP(Transmission Control Protocol)
- 인터넷 상에서 데이터를 메시지 형태로 보내기 위해 IP와 함께 사용하는 프로토콜  
- 보통 TCP/IP로 쓰인다.  
    - IP는 패킷 전달여부를 보증하지 않고 패킷을 보낸 순서와 받는 순서를 관리하지 않음.  
    그런 IP의 단점을 보완하기 위해서 TCP는 IP와 함께 쓰임  
    - IP가 패킷의 전달을 담당한다면 TCP는 패킷들이 도착을 잘 하는지, 순서는 알맞게 되어있는지 검사하는 역할  

- 가상 회선 연결방식, 연결형 서비스 제공  
- 보안적으로 높은 신뢰성  
- __데이터의 흐름 제어 및 혼잡 제어__  
    - 수신자 버퍼가 오버플로우 나는 상황을 방지하고 네트워크 내에 패킷이 과도하게 증가하는 것을 방지
- Full-Duplex, Point to Point 방식  
    - Full-Duplex : __전이중 통신__ 이라고도 하며 두 대의 단말기가 데이터를 송수신 하기 위해 각각 독립된 회선을 사용하는 방식, 데이터가 동시에 양쪽으로 전송되는 방식으로, 2차선 다리와 같다.  
    - Point to Point : 통신시 양 노드 또는 네트워크가 1 : 1 형식으로 연결된 구조  

### 3-way handshaking / 4-way handshaking

#### 3-way handshaking
TCP는 장치들 사이에 논리적인 접속을 성립하기 위해 3-way handshaking을 사용하는데, 이는 TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 __세션을 수립하는 과정__ 을 의미한다.

```
Client -> Server : TCP SYN(Synchronize sequence numbers)
Server -> Client : TCP SYN ACK(acknowledgment)
Client -> Server : TCP ACK
``` 

1. A 클라이언트는 B 서버에 접속을 요청하는 SYN 패킷을 보낸다. 이때 A 클라이언트는 SYN을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태이다.

2. B 서버는 SYN 요청을 받고 A 클라이언트에게 요청을 수락한다는 ACK과 SYN flag가 설정된 패킷을 발송하고 A가 다시 ACK으로 응답하기를 기다린다. 이때 B 서버는 SYN_RECEIVED 상태이다.  

3. A 클라이언트는 B 서버에게 ACK을 보내고 이후부터는 연결이 이루어 지고 데이터가 오가게 되는것이다. 이떄 B 서버 상태가 성립(ESTABLISHED)이다. 

#### 4-way handshaking
__세션을 종료하기위한 과정__ 을 의미한다.

1. 클라이언트가 연결을 종료하겠다는 FIN flag를 전송한다.

2. 서버는 일단 확인메세지를 보내고 자신의 통신이 끝날떄까지 기다린다. (TIME_WAIT)

3. 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN flag를 전송한다.

4. 클라이언트는 확인했다는 메세지를 보낸다.

# What is UDP

## UDP (User Datagram Protocol)
- __데이터를 데이터그램 단위로 처리하는 프로토콜__
- 서로 정보를 주고 받을때 어떠한 신호절차를 거치지 않고 보내는 쪽에서 __일방적으로 데이터를 전달__ 하는 방식
- 보내는 쪽에서 받는 쪽이 데이터를 받았는지 확인하지 않음
- 비 연결형 서비스이기 때문에 연결을 설정하고 해제하는 과정이 존재하지 않는다.
- 패킷에 순서를 부여하여 재조립하거나 흐름을 제어하는 기능같은 것이 없어 __TCP보다 속도가 빠르고 네트워크 부하가 적다.__
- 신뢰성 있는 데이터 전송을 보장할 수 없다.
- 신뢰성 보다는 연속성이 중요한 서비스로, 주로 __실시간 서비스__ 에 이용된다.
- 흐름제어가 없기에 패킷의 확인이 불가능 하다.  

# What are the network layers & What is the OSI model

## OSI model / OSI 7 계층
네트워크 통신이 일어나는 과정을 7단계로 나눈 것. 분할 정복 알고리즘의 개념과 같이 복잡한 문제를 해결하고자 할 때, 나누어서 생각하면 쉽게 해결할 수 있다는 취지이다.

- __데이터의 흐름을 알기위함__ : 계층별 기능을 통해 전반적인 흐름 이해가 쉬워진다.
- __문제해결이 쉬워짐__ : 계층별로 구분을 해둬 어느부분에서 문제가 생겼는지 파악이 쉽다.
- __표준화__ : 네트워크의 초창기 각 장비회사에선 서로 다른 프로토콜을 이용했는데 OSI model을 통해 서로 같은 프로토콜을 사용하게 되고 타 회사간 장비의 통신이 가능해졌다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcijRJX%2FbtqAgTUAX4u%2FMiSobdh9uTZ3ByAHAasix1%2Fimg.png" width="350px" height="400px"></img>
<img src="https://img.router-switch.com/media/wysiwyg/Help-Center-FAQ/Router/network-layer-protocols.jpg" width="430px" height="330px"></img><br/>

### __7계층 : 응용계층 (Application Layer)__

사용자와 바로 연결되어 있으며 Application Software를 도와준다.  
사용자로부터 정보를 입력받아 하위 계층으로 전달하고 하위 계층에서 전송한 데이터를 사용자에게 전달  
데이터 생성을 목적으로 사용자에게 인터페이스와 네트워크 서비스 제공  
__파일 전송, DB, 메일 전송__ 등 여러가지 응용 서비스를 네트워크에 연결해주는 역할을 한다.  

- 프로토콜 : __DHCP, DNS, FTP, HTTP__

### __6계층 : 표현계층 (Presentation Layer)__

표현계층은 송신측과 수신측 사이에서 __데이터의 형식(png, jpg, jpeg..)을 정해준다.__ 받은 데이터를 코드 변환, 구문 검색, 암호화, 압축의 과정을 통해 올바른 표준 방식으로 변환해준다.  

- 프로토콜 : __JPG__, MPEG, SMB, AFP

### __5계층 : 세션계층 (Session Layer)__

통신 세션을 구성하는 계층으로, __포트__ 번호를 기반으로 연결한다. __통신장치 간의 상호작용을 설정하고 유지하며 동기화한다.__ 동시 송수신(Duplex), 반이중(Half-Duplex), 전이중(Full-Duplex) 방식의 통신과 함께 체크 포인팅과 유후, 종료, 다시 시작 과정등을 수행한다.  

- 프로토콜 : NetBIOS, __SSH__ , TLS

### __4계층 : 전송계층 (Transport Layer)__

__발신지에서 목적지(End-to-End)간 제어와 에러를 관리__ 한다. 패킷의 전송이 유효한지 확인하고 전송에 실패된 패킷을 다시 보내는 것과 같은 신뢰성있는 통신을 보장하며, 헤드에는 세그먼트가 포함된다. 주소 설정, 오류 및 흐름제어, 다중화를 수행한다.  

- PDU : 세그먼트(Segment)
- 프로토콜 : __TCP, UDP__ , ARP, RTP
- 장비 : 게이트웨이, L4스위치

### __3계층 : 네트워크계층 (Network Layer)__

네트워크 계층은 __기기에서 데이터그램이 가는 경로를 설정__ 해주는 역할을 한다. 라우팅 알고리즘을 사용하여 최적의 경로를 선택하고 송신측으로부터 수신측으로 전송한다. 이때, 전송되는 데이터는 패킷단위로 분할하여 전송한 후 다시 합쳐진다. Link Layer가 Node to Node 전달을 감독한다면, Network Layer는 각 패킷이 목적지까지 성공적이고 효과적으로 전달되도록 한다.  

- PDU : 패킷
- 프로토콜 : __IP__ , ICMP 등
- 장비 : 라우터, L3스위치

### __2계층 : 링크계층 (Link Layer)__

링크계층은 __네트워크 기기들 사이의 데이터 전송__ 을 하는 역할을 한다. 시스템 간의 오류없는 데이터 전송을 위해 패킷을 프레임으로 구성하여 물리계층으로 전송한다. 네트워크 계층에서 정보를 받아 주소와 제어정보를 헤더와 테일에 추가한다.  

- PDU : 프레임
- 프로토콜 : 이터넷, MAC, PPP, ATM, __LAN, Wifi__
- 장비 : 브릿지, 스위치

### __1계층 : 물리계층 (Physical Layer)__

물리계층은 OSI 모델의 최하위 계층에 속하며, 상위 계층에서 전송된 데이터를 __물리 매체(허브, 라우터 ,케이블 등)를 통해 다른 시스템에 전기적 신호를 전송__ 하는 역할을 한다.  

- PDU : 비트
- 프로토콜 : Modem, __Cable__, Fiber, RS-232C
- 장비 : 허브, 리피터  

## TCP/IP 모델  

OSI 참조 모델은 말 그대로 참조 모델일 뿐 실제 사용되는 인터넷 프로토콜은 OSI 7계층 구조를 완전히 따르지는 않는다. 인터넷 프로토콜 스택은 현재 대부분 TCP/IP를 따른다.  

TCP/IP는 인터넷 프로토콜 중 가장 중요한 역할을 하는 TCP와 IP의 합성어로 데이터의 흐름 관리, 정확성 확인, 패킷의 목적지 보장을 담당한다. __데이터의 정확성 확인은 TCP가, 패킷을 목적지까지 전송하는 일은 IP가 담당한다.__   <br/>

<img src="https://image.ahnlab.com/info/securityinfo/upload_/net_0506_08.gif
"></img><br/>

데이터는 아래 그림과 같이 단계별로 헤더(Data -> Segment -> Datagram -> Frame)을 붙여 전송하며 이를 `데이터 캡슐화`라고 한다.  

<center><img src="https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile22.uf.tistory.com%2Fimage%2F99803C415BA2F07C069823
"></img></center><br/>

# What is a DHCP server and the DHCP protocol

## DHCP (Dynamic Host Configuration Protocol)  

TCP/IP 프로토콜에서는 각 컴퓨터들이 고유 IP를 가져야만 인터넷에 접속할 수 있다. 이때 네트워크 관리자는 ISP(Internet Service Provider)로 부터 주소를 할당받는다.  

네트워크 관리자는 할당받은 IP주소 블록 내에서 각 컴퓨터, 호스트에 `IP주소, 서브넷 마스크, 기본 게이트웨이 IP주소, DNS서버 IP주소` 를 할당하고 관리한다. 이 과정을 자동으로 관리할 수 있게 해주는 것이 __DHCP__ 이다. 즉, __IP의 동적인 할당을 자동으로 관리해주는 것, IP의 임대__  

DHCP를 통한 IP주소 할당은 임대라는 개념을 가지고 있는데 이는 DHCP 서버가 IP주소를 영구적으로 단말에 할당하는 것이 아니고 __임대기간을 명시하여 그 기간 동안만 단말이 IP주소를 사용__ 하도록 하는 것이다. 단말은 __IP 주소 임대기간 갱신__ 을 DHCP에 요청하여 임대기간을 연장할 수 있으며 더이상 임대가 필요치 않으면 __IP주소 반납 절차__ 를 수행하게 된다.  

### DHCP 서버와 클라이언트  

#### __DHCP 서버__ 

클라이언트에게 IP할당 요청이 들어오면 IP를 부여해주고 할당 가능한 IP의 관리를 맡는다.  

DHCP가 설정해주는 주소 정보들은 아래와 같다. 
1. IP주소 : 192.168.0.4
2. 서브넷 마스크 : 255.255.255.0
3. 기본 게이트웨이 : 192.168.0.1
4. DNS 서버 IP 주소 : 210.220.163.82 / 219.250.363.130  

#### __DHCP 클라이언트__

시스템 시작시 DHCP서버에 자신의 시스템을 위한 IP주소를 요청하고 그를 통해 TCP/IP 설정을 초기화 한 후 다른 호스트와 TCP/IP를 사용해서 통신을 할 수 있게 된다.  

<center><img src="https://1.bp.blogspot.com/-y4NqGSGK0r8/XYRQwIeYIiI/AAAAAAAACOA/yxXGKYtmX_Ybu9CITlyBJ9aSAoms3g9DgCLcBGAsYHQ/s640/%25EC%25BA%25A1%25EC%25B2%2598.JPG
"></img></center><br/>

### DHCP 임대 절차

IP 주소 할당 절차에 사용되는 DHCP 메시지는 아래 그림과 같이 4개의 메세지로 구성되어 있다.  

<center><img src="https://www.netmanias.com/ko/?m=attach&no=1987
"></img></center><br/>

1. DHCP Discover
ㄴㅇㅁㄴㅇ

### DHCP의 장단점

__장점__ : PC수가 많거나 PC자체의 변동사항이 많을 경우 IP 설정이 자동으로 되기 때문에 효율적이고 IP 할당이 자동이므로 IP 충돌을 막을 수 있다.  

__단점__ : DHCP 서버에 의존하기 떄문에 서버가 다운되면 IP할당이 제대로 이루어지지않는다.  


# What is a DNS server and the DNS protocol
# What are the rules to make 2 devices communicate using IP addresses
# How does routing work with IP
# What is a default gateway for routing
# What is a port from an IP point of view and what is it used for when connecting to another device
