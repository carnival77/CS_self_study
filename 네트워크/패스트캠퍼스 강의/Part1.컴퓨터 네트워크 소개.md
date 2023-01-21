- [1. 컴퓨터 네트워크와 인터넷](#1-컴퓨터-네트워크와-인터넷)
  - [1.1. 네트워크와 인터넷](#11-네트워크와-인터넷)
    - [1.1.1. 네트워크](#111-네트워크)
    - [1.1.2. 인터넷](#112-인터넷)
    - [1.1.3. OSI 7계층 (Layer)](#113-osi-7계층-layer)
    - [1.1.4. TCP/IP (Transmission Control Protocol/Internet Protocol)](#114-tcpip-transmission-control-protocolinternet-protocol)
  - [1.2. 그 밖에 자주 사용되는 용어들](#12-그-밖에-자주-사용되는-용어들)
    - [1.2.1. IP 주소 (Address)](#121-ip-주소-address)
    - [1.2.2. 패킷 교환 (Packet Switching)](#122-패킷-교환-packet-switching)
  - [1.3. 통신을 위한 기본 동작](#13-통신을-위한-기본-동작)
    - [1.3.1. 요청(Request)](#131-요청request)
    - [1.3.2. 인지(Indicate)](#132-인지indicate)
    - [1.3.3. 응답(Response)](#133-응답response)
  - [1.4. 확인(Confirm)](#14-확인confirm)
- [2. 네트워크의 유형](#2-네트워크의-유형)
  - [2.1. LAN (Local Area Network)](#21-lan-local-area-network)
  - [2.2. WAN (Wide Area Network)](#22-wan-wide-area-network)
  - [2.3. 크기 유형](#23-크기-유형)
- [3. 네트워크의 계층별 역할](#3-네트워크의-계층별-역할)
  - [3.1. OSI(Open Systems Interconnection Reference Model) 7계층](#31-osiopen-systems-interconnection-reference-model-7계층)
  - [3.2. OSI 7 계층과 TCP/IP의 관계](#32-osi-7-계층과-tcpip의-관계)
  - [3.3. 종단 간의 연결](#33-종단-간의-연결)
  - [3.4. 물리 계층(Physical Layer)](#34-물리-계층physical-layer)
  - [3.5. 데이터 링크 계층(Data Link Layer)](#35-데이터-링크-계층data-link-layer)
    - [3.5.1. 데이터 링크 - 노드 대 노드(Hop-to-Hop)의 전달 책임](#351-데이터-링크---노드-대-노드hop-to-hop의-전달-책임)
    - [3.5.2. 데이터 링크 계층의 전달 요소](#352-데이터-링크-계층의-전달-요소)
      - [3.5.2.1. 물리주소의 데이터 전달  과정](#3521-물리주소의-데이터-전달--과정)
  - [3.6. 네트워크 계층(Network Layer)](#36-네트워크-계층network-layer)
    - [3.6.1. 네트워크 계층 - 발신지 대 목적지 전달](#361-네트워크-계층---발신지-대-목적지-전달)
    - [3.6.2. 네트워크 계층의 전달 흐름](#362-네트워크-계층의-전달-흐름)
  - [3.7. 전송 계층(Transport Layer)](#37-전송-계층transport-layer)
    - [3.7.1. 전송 층에서의 전달](#371-전송-층에서의-전달)
      - [3.7.1.1. 메세지의 프로세스 대 프로세스 전달](#3711-메세지의-프로세스-대-프로세스-전달)
      - [3.7.1.2. 전송 계층의 전달 예시](#3712-전송-계층의-전달-예시)
  - [3.8. 세션 계층(Session layer)](#38-세션-계층session-layer)
  - [3.9. 표현 계층(Presentation layer)](#39-표현-계층presentation-layer)
  - [3.10. 응용 계층 (Application Layer)](#310-응용-계층-application-layer)
  - [3.11. 각 계층과 프로토콜 비교](#311-각-계층과-프로토콜-비교)
- [4. 추가 참고 자료](#4-추가-참고-자료)


# 1. 컴퓨터 네트워크와 인터넷

## 1.1. 네트워크와 인터넷

### 1.1.1. 네트워크

- 종단 시스템(end system) : PC나 스마트폰처럼 네트워크 송수신 주체

- 프로토콜(Protocol) : 두 이종 시스템을 연결하기 위한 규약

- 통신을 목적으로 실제 물리적으로 선으로 연결되어 있거나 무선으로 연결

### 1.1.2. 인터넷

- 회사 혹은 소규모의 네트워크에서 전세계 네트워크와 연결된 상태

- 다양한 애플리케이션 서비스가 제공되고 있다

- 종단 시스템은 보통 ISP(Internet Service Provider)에 의해 연결된다

### 1.1.3. OSI 7계층 (Layer)

- 네트워크 구성 요소를 7개의 계층으로 역할을 나눈 표준 모델

- 각 계층별 역할을 통해 통신 규격(프로토콜)을 만족

- 일부 하위 계층은 하드웨어에서 구현되며, 상위 계층은 소프트웨어로 구현

### 1.1.4. TCP/IP (Transmission Control Protocol/Internet Protocol)

- OSI 7계층이 나오기 전 널리 사용되던 사실상 표준 역할

- 각 계층별 역할에 따라 역할이 나누어짐

## 1.2. 그 밖에 자주 사용되는 용어들

### 1.2.1. IP 주소 (Address)

- 통신 자료를 최종적으로 전달하기 위해 필요한 송/수신 위치 정보

- 보통 IPv4 주소를 사용하며, 주소 부족을 해결하기 위해 IPv6가 개발됨

### 1.2.2. 패킷 교환 (Packet Switching)

- 종단 간에 전송되는 데이터를 **패킷(Packet)** 이라는 단위로 전달함

- 패킷은 네트워크를 통해 일정한 순서 없이 보내지며 어떤 경로를 통해 이동되는지는 네트워크 상황에 따라 다르다.

## 1.3. 통신을 위한 기본 동작

### 1.3.1. 요청(Request)

전송하는 종단 장치에서 상대방에 서비스를 요청한다

### 1.3.2. 인지(Indicate)

수신하는 장치에서 작업 요청(이벤트)을 확인한다

### 1.3.3. 응답(Response)

수신하는 장치에서 요청 받은 작업에 대해 적절히 응답한다.

## 1.4. 확인(Confirm)

전송 측에서 응답 데이터를 최종적으로 확인한다.

# 2. 네트워크의 유형

## 2.1. LAN (Local Area Network)

- 일정 그룹의 지역 네트워크 (집, 사무실, 학교 등)

- 소규모로 묶이며 사설망 등을 연결해 구축

## 2.2. WAN (Wide Area Network)

- 원거리 통신망으로 넓은 범위 연결 (국가, 대륙 등)

## 2.3. 크기 유형

LAN < WAN < Internet

![image](https://user-images.githubusercontent.com/52997401/213849006-48332e46-f943-4ce6-89f7-08013bbe72a8.png)

# 3. 네트워크의 계층별 역할

## 3.1. OSI(Open Systems Interconnection Reference Model) 7계층

> OSI 7계층이란, 통신 접속에서 완료까지의 과정을 네트워크 통신을 구성하는 요소들에 따라 7단계로 정의한 국제 통신 표준 규약이다.
> 
> 이를 통해 계층별 기능과 통신 과정을 단계별로 파악할 수 있어, 특정한 곳에 이상이 생기면 그 단계만 수정할 수 있기 때문에 편리하다.

- 이 모델은 프로토콜을 기능별로 나눈 것이다.
- 각 계층은 하위 계층의 기능만을 이용하고, 상위 계층에게 기능을 제공한다.
- '프로토콜 스택' 혹은 '스택'은 이러한 계층들로 구성되는 프로토콜 시스템이 구현된 시스템을 가리키는데, 프로토콜 스택은 하드웨어나 소프트웨어 혹은 둘의 혼합으로 구현될 수 있다.
- 일반적으로 하위 계층들은 하드웨어로, 상위 계층들은 소프트웨어로 구현된다.

## 3.2. OSI 7 계층과 TCP/IP의 관계

![](https://media.vlpt.us/images/jogiyo/post/0e189400-41bb-4f42-a4c0-e9b0564053d3/image.png)

![image](https://user-images.githubusercontent.com/52997401/213849086-d0a9d1be-1c03-433a-81ad-2294af0b0f19.png)

## 3.3. 종단 간의 연결

![image](https://user-images.githubusercontent.com/52997401/213849153-234ef56a-af42-4b2a-bf5c-c7d05a40ca12.png)

## 3.4. 물리 계층(Physical Layer)

- 개요
  
  - 물리적 매체(통신 케이블 등 기계적, 전기적, 전송매체)를 통해 데이터를 신호로 변환한 <mark>비트 스트림 전송</mark>을 담당
  
  - 물리적인 장치와 인터페이스가 전송을 위해 필요한 기능과 처리절차 규정
  
  - 전송 단위 : Bit

- 물리 계층의 주요 기능
  
  - 인터페이스와 매체의 물리적인 특성 : 장치와 전송 매체 간의 인터페이스 특성을 규정
  
  - 비트의 표현 : 비트를 전송하기 위해 전기적 또는 광학적인 신호로 부호화
  
  - 데이터 속도 : 신호가 유지되는 비트의 주기를 규정
  
  - 비트의 동기화 : 송신자와 수신자는 같은 클록을 사용

![image](https://user-images.githubusercontent.com/52997401/213849228-70120b34-750c-4cec-b214-fcf375aa2059.png)

- 프로토콜
  
  - MAC(Medium Access Control) 필요
    
    - 자유경쟁 (선착순)
      
      - CSMA(Carrier Sense Multiple Access)
      
      - **CSMA/CD(CSMA/Collison Detection)**
    
    - Token
  
  - CSMA/CD -> IEEE 802.3
    
    - 한 slot의 크기 잼 신호 = 51.2 us = 64byte 전송소요시간
    
    - 16번까지 재시도

## 3.5. 데이터 링크 계층(Data Link Layer)

- 개요
  
  - 노드 대 노드(node to node) 간 물리적 매체로 패킷 데이터를 신뢰성 있게 전달
  - MAC 주소를 가지고 통신
  - 데이터 전송 단위 : Frame
  - 전송 주소 : MAC

- 기능
  
  - **프레임** 구성 : 네트워크 계층으로부터 받은 비트 스트림을 프레임 단위로 나눔
  
  - **물리주소 MAC(Medium Access Control)** 지정 : 
    
    - 네트워크 카드가 만들어질 때부터 맥 주소(MAC address)가 정해져 있다
    
    - 송신자와 수신자의 물리 주소를 헤더에 추가
  
  - **흐름 제어** : 수신자의 수신 데이터 전송률을 고려하여 데이터 전송하도록 제어
  
  - **오류 제어** : 손상 또는 손실된 프레임을 발견/재전송, 트레일러를 통해 이루어짐
  
  - **접근 제어** : 주어진 어느 한 순간에 하나의 장치만 동작하도록 제어

![image](https://user-images.githubusercontent.com/52997401/213852275-f1bc1369-28ae-4317-9647-6de07723d26e.png)

- 주요 프로토콜
  
  - ARP(Address Resolution Protocol)
    
    - 주소를 해석하기 위한 프로토콜
    
    - 논리적인 IP 주소를 물리적인 MAC 주소로 바꾼다.
    
    - 캐시를 통해 얻은 정보가 저장되고 보통 20분의 수명을 가진다.
  
  - RARP(Reserve Address Resolution Protocol)
    
    - 역 주소 프로토콜
    
    - 저장 장치가 없는 네트워크 단말기 등이 IP 주소를 얻기 위해 사용

- 예시
  
  - 이더넷

### 3.5.1. 데이터 링크 - 노드 대 노드(Hop-to-Hop)의 전달 책임

![image](https://user-images.githubusercontent.com/52997401/213853445-97dddcc8-fa26-4654-afc7-3499214bfe07.png)

### 3.5.2. 데이터 링크 계층의 전달 요소

#### 3.5.2.1. 물리주소의 데이터 전달  과정

- 물리주소 10인 노드는 물리주소 87 인 노드에 프레임을 보낸다..
  
  - Ex) 07:01:02:01:2C:4B

- 데이터 링크 수준에서 이 프레임은 헤더에 물리 주소들을 가지고 있다. 여기서는 오직 이 주소들만 필요하다.

- 헤더의 끝에는 이 수준에서 필요한 다른 정보가 있다. 트레일러에는 보통 오류 검출을 위한 추가 비트들이 포함되어 있다.

![image](https://user-images.githubusercontent.com/52997401/213855298-f9d612cc-f624-4686-ae5d-de4ac9c2d05a.png)

## 3.6. 네트워크 계층(Network Layer)

- 개요
  
  - 네트워크를 논리적으로 구분하고 연결하는 계층
  - 논리적 주소를 기반으로 패킷의 <mark>발신지-대-목적지</mark> 전달
  - 데이터 전송 단위 : Datagram(Packet)
  - 전송 주소 : IP

- 기능
  
  - 발신지-대-목적지 전달(packet)
  
  - 논리 주소지정(Logical addressing)
    
    - IP : 네트워크 관리자가 할당한 논리적인 주소
    - 상위 계층에서 받은 패킷에 발신지와 목적지의 논리 주소를 헤더에 추가
  
  - 라우팅(Routing)
    
    - 데이터(패킷)가 최종 목적지에 전달될 수 있도록 주소(IP)를 정하고, 경로(Route)를 지정하거나 교환 기능

![image](https://user-images.githubusercontent.com/52997401/213856959-9afb4e36-6c00-42ed-a627-2582e76786e3.png)

- 주요 프로토콜
  
  - ICMP(Internet Control Message Protocol)
    
    - 에러 발생 시 에러 발생 원인을 알려주거나 네트워크 상태를 진단해주는 기능
  
  - IGMP(Internet Group Management Protocol)
    
    - 호스트(컴퓨터)가 멀티캐스트 그룹 구성원을 인접한 라우터에게 알리는 프로토콜
  
  - IP (Internet Protocol)
    
    - 네트워크 기기에서 논리적 식별을 위한 주소
      
      - IPv4 : 약 40억 개의 주소
        
        - Ex) 123.321.234.232
      
      - IPv6 : 2의 128제곱의 개수를 가진 주소 
        
        - Ex) 21DA:00D3:0000:2F3B:02AA:00FF:FE28:9C5A

### 3.6.1. 네트워크 계층 - 발신지 대 목적지 전달

![image](https://user-images.githubusercontent.com/52997401/213858193-19f3d67f-a8ed-4286-8626-7417adf299b5.png)

### 3.6.2. 네트워크 계층의 전달 흐름

![image](https://user-images.githubusercontent.com/52997401/213858266-d1c43407-51bf-48a7-85e7-33530c1b7da2.png)

## 3.7. 전송 계층(Transport Layer)

- 개요
  
  - 전체 메시지를 전달 가능한 세그먼트 단위로 분할하고, 전체 메시지가 완전하게 바른 순서로 <mark>프로세스 대 프로세스로 전달됨을 보장</mark>
  
  - 이를 위해 데이터의 전송 방식을 결정하고 전송 속도를 조절하며 오류를 정정하여 신뢰성 있는 데이터를 전달
  
  - 데이터 전송 단위 : Segment
  
  - 전송 주소 : Port
  
  - *네트워크 층은 개별적인 패킷의 종단-대-종단(end-to-end) 전송을 담당*

![image](https://user-images.githubusercontent.com/52997401/213858477-2346300d-2b9c-4d8d-9da9-3850b0a9edce.png)

- 기능
  
  - 포트 주소 지정 (port addressing) : 포트 주소를 포함
    
    - 네트워크 계층은 각 패킷을 정확한 컴퓨터에, 전송 계층은 해당 컴퓨터의 정확한 프로세스(프로그램)에게 전달
  
  - 분할과 재조립 (Segmentation and reassembly)
    
    - 전달 가능한 세그먼트 단위로 나눔
    
    - 각 세그먼트는 <mark>순서 번호</mark>를 가지며 이를 통해 재조립 또는 패킷의 손실 여부 판단
  
  - 연결 제어  (Connection control)
    
    - 비 연결 및 연결 지향
  
  - 흐름 제어 (Flow control)
  
  - 오류 제어 (Error control)

- 프로토콜
  
  - TCP (Transmission Control Protocol)
    
    - 연결형 서비스로 가상 회선 방식을 제공
    
    - 신뢰성을 보장하며 3-way handshaking 과정을 통해 연결
    
    - 전이중(Full-Duplex), 점대점(Point to Point) 방식
  
  - UDP(User Datagram Protocol)
    
    - 비연결형 서비스로 데이터 그램 방식을 제공
    
    - 신뢰성이 낮다
    
    - TCP보다 속도가 빠르다
  
  - SCTP(Stream Control Transmission Protocol)
    
    - SCTP는 UDP와 TCP의 특성을 결합
    
    - UDP나 TCP와 유사하며 다중 연결을 지원한다.

### 3.7.1. 전송 층에서의 전달

#### 3.7.1.1. 메세지의 프로세스 대 프로세스 전달

![image](https://user-images.githubusercontent.com/52997401/213858808-b1c44d3a-5d14-4fa9-b717-348f7b4d1628.png)

#### 3.7.1.2. 전송 계층의 전달 예시

![image](https://user-images.githubusercontent.com/52997401/213859080-2069dc52-4af5-429b-a15c-c76c7733257b.png)

## 3.8. 세션 계층(Session layer)

- 개요
  
  - 응용 프로그램 간의 연결을 지원해주는 계층
  
  - 통신 시스템 사용자간의 연결을 유지 및 설정함 (API, Socket)
  
  - 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공
  
  - **동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex)의 통신**과 함께, 체크 포인팅과 유휴, 종료, 다시 시작 과정 등을 수행
  
  - TCP/IP 세션을 만들고 없애는 책임을 진다.

## 3.9. 표현 계층(Presentation layer)

- 개요
  
  - 데이터의 변환 작업을 하는 계층

- 응용 계층으로부터 전달 받거나 전송하는 데이터를 응용 계층에서 이해할 수 있도록 응용 프로그램에 맞춰 인코딩 및 디코딩 등 변환 이뤄짐. 파일 인코딩, 명령어를 포장, 압축, 암호화한다. (JPEG)

- 코드 간의 번역을 담당하여 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어 준다.

- MIME 인코딩이나 암호화 등의 동작이 이 계층에서 이루어진다.

## 3.10. 응용 계층 (Application Layer)

- 개요
  
  - 사용자가 네트워크에 접속할 수 있게 해 줌
  - 데이타 단위 : Data/Message

- 기능
  
  - 사용자 인터페이스 제공

- 서비스
  
  - 원격로그인, 파일액세스, 전송, 관리, 메일서비스(Mail services) Http www 웹 등등

![image](https://user-images.githubusercontent.com/52997401/213859129-4c7c51ff-927d-4edc-8f5b-21e1db513aa3.png)

- 프로토콜 및 프로그램
  
  - FTP (File Transfer Protocol)
  
  - Telnet
  
  - SMTP (Simple Mail Transfer Protocol)
  
  - DNS ( Domain Name System )
  
  - HTTP
  
  - DHCP
  
  - Ping
  
  - Tcpdump
  
  - Tracerouter

## 3.11. 각 계층과 프로토콜 비교

![image](https://user-images.githubusercontent.com/52997401/213859314-13a52a8f-1870-4729-99af-27baef34194d.png)

# 4. 추가 참고 자료

https://velog.io/@jehjong/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0-TCPIP-4%EA%B3%84%EC%B8%B5

[TCP/IP 프로토콜](https://underground2.tistory.com/5)

[https://github.com/carnival77/tech-interview/blob/master/contents/network.md#osi-7%EA%B3%84%EC%B8%B5](https://github.com/carnival77/tech-interview/blob/master/contents/network.md#osi-7%EA%B3%84%EC%B8%B5)
