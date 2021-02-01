#### OSI 7계층이란?
- 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것  

#### OSI 7계층을 나눈 이유는?
- 통신이 일어나는 과정을 단계별로 파악할 수 있기 때문  
- 전체 흐름에 대한 쉬운 이해 및 문제 발생시 원인 파악의 수월함 때문 (모듈화의 장점)  

#### 1계층 - 물리 계층 (Physical Layer)
- 전기적, 기계적인 특성을 이용해서 통신 케이블로 데이터를 전송  
- 통신 단위는 비트 (0 또는 1)  
- 단순 데이터 전송 역할  
- 통신 케이블, 허브 등  

#### 2계층 - 데이터 링크 계층 (DataLink Layer)
- 맥주소를 가지고 물리계층에서 받은 정보를 전달  
- 에러검출 / 통신 채널 공유 (재전송 / 흐름제어)  
- 브릿지, 스위치  
- NIC (Network Interface Card)  
- 관련 Protocol: MAC Protocol (예시: CSMA/CD), ARP (Address Resolution Protocol)  

#### 3계층 - 네트워크 계층 (Network Layer)
- 라우팅: IP 주소를 활용하여 데이터를 목적지까지 전달하는 기능  
- 라우팅, 흐름제어, 세그먼테이션, 오류제어 등  
- 관련 Protocol: IP Protocol, DHCP, ICMP  

*ICMP: Host 또는 router에서 사용자 메시지가 아닌 네트워크 상태를 전달하기 위해 사용하는 프로토콜  

#### 4계층 - 전송 계층 (Transport Layer)
- 프로세스 간 통신  
- 통신 활성화  
- 패킷 생성(Assembly/Sequencing/Deassembly/Error detection/Request repeat/Flow control) 및 전송  
- 관련 Protocol: TCP, UDP

#### 5계층 - 세션 계층 (Session Layer)

#### 6계층 - 표현 계층 (Presentation Layer)

#### 7계층 - 응용 계층 (Application Layer)

https://shlee0882.tistory.com/m/110
