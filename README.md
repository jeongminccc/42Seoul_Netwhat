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

### 서브넷
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

### 서브넷 마스크
IP주소를 읽을 때 어디까지가 네트워크 아이디인지를 알려주는 척도가 된다.

```
192.168.0.1 (주소)  
255.255.255.0 (Class C 서브넷 마스크)  

(A면 255.0.0.0, B면 255.255.0.0)
```

하지만 이렇게 하게된다면 낭비되는 주소가 생긴다는 문제가 발생하는데, Class C의 경우 대략 250개 정도의 호스트를 보유할 수 있는데 어떠한 기관에서 100개 정도의 호스트만 감당할 수 있는 네트워크를 필요로 한다고 가정해 보자. 클래스로만 구분된 네트워크로만 할당을 하자니 제일 작은 클래스 C의 호스트 수는 벌써 200개가 넘고, 낭비가 발생하게 된다.  

이런 발상에서 시작한 것이 __CIDR(Classless Inter-Domain Routing)__ 이다.  

### CIDR
Classless Inter-Domain Routing, 클래스로만 구분된 네트워크의 한계를 극복하기 위한 수단으로 개발되었다.  


# What is the broadcast address of a subnet
# What are the different ways to represent an ip address with the Netmask
# What are the differences between public and private IPs
# What is a class of IP addresses
# What is TCP
# What is UDP
# What are the network layers
# What is the OSI model
# What is a DHCP server and the DHCP protocol
# What is a DNS server and the DNS protocol
# What are the rules to make 2 devices communicate using IP addresses
# How does routing work with IP
# What is a default gateway for routing
# What is a port from an IP point of view and what is it used for when connecting to another device
