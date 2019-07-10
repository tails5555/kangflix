---
layout: post
title: "OSI 7계층"
date: 2019-07-10 14:00:00 +09:00
image: "/kangflix/assets/img/category/ct_network.png"
category: 'network'
tags:
- Network
- OSI
description: OSI 7계층이 무엇인지 알아봅니다.
introduction: OSI 7계층이 무엇인지 알아봅니다.
---

## OSI Model

![OSI_IMAGE]({{ site.baseurl }}/assets/img/post/network/osi_structure.png){: width="100%"}

OSI 모델은 국제표준화기구(ISO) 에서 개발한 네트워크 계층 모델 입니다.

컴퓨터 네트워크에서 사용하는 프로토콜 디자인과 통신을 계층으로 나눈 것입니다.

OSI 모델의 계층은 7 가지로 구분되어 있습니다. 그리고 각 계층은 **L** 로 간추려서 작성합니다.

(예를 들어 전송 계층은 L4, 응용 계층은 L7 와 같이.)

상대방 간 네트워크가 생성되면 발신 측은 L7 (응용 계층) 에서 L1 계층 (물리 계층) 으로 내려갑니다.

이 과정을 Multiplexing(다중화) 라 하고, Header 가 추가 됩니다.

반대로 수신 측은 L1 계층 에서 L7 계층으로 올라갑니다.

이를 Demultiplexing(역다중화) 라 하고, 순수 Data 만 추출하게 됩니다.

참고로 다중화 과정이 이뤄지면서 Header 가 많아지면 이것들도 Data 가 되어 차기 계층에선 이 값들을 수정할 수 없습니다.

## Physical Layer

- 물리 계층. (L1)
- 네트워크에 참여하는 장치(디바이스) 들을 연결하기 위해 하드웨어의 세부 사항을 정의한 것.
- 통신 채널로 전송되는 디지털 데이터를 디바이스에 맞게 변조 시키는 역할.
- 단위는 신호(Signal), 대표적인 장치는 허브(Hub).

## Data Link Layer

- 데이터 링크 계층. (L2)
- Peer To Peer (P2P) 통신 간 신뢰성 있는 전송을 보장하기 위한 계층.
- CRC 기반 오류, 흐름 제어를 이행해야 함.
- 물리 계층 간의 오류를 찾고, 네트워크 개체에게 데이터를 전달.
- 단위는 프레임(Frame), 대표적인 장치는 L2 Switch 가 있음.
- 주요 프로토콜은 Ethernet, HDLC, LLC 등이 있음.

## Network Layer

- 네트워크 계층. (L3)
- 여러 네트워크 노드(Node) 들을 거치면서 최적의 경로를 찾는 역할을 함.
- 전송 계층에서 필요한 서비스 품질(Quality of Service, QoS) 를 위한 자원 제공.
- 이 계층의 주요 임무는 라우팅, 패킷 포워딩, 인터네트워킹, 세그먼테이션 등이 있음.
- 단위는 패킷(Packet), 대표적인 장치는 Router 가 있음.
- 주요 프로토콜은 IP, ARP, RIP, OSPF, IGRP 등이 있음.

## Transport Layer

- 전송 계층. (L4)
- 양 끝단(End-to-End) 의 사용자들이 신뢰 있는 데이터를 주고 받을 수 있도록 지원.
- 시퀀스 넘버를 기준으로 오류를 제어. (대표적으로 Go-Back-N, Selective-Repeat ARQ.)
- 상태 개념이 있고 (Stateful), 연결 기반 (Connection Oriented) 프로토콜이 존재함.
- 단위는 세그먼트(Segment), 대표적인 장치는 L4 Switch 가 있음.
- 주요 프로토콜은 TCP, UDP 가 있음.

## Session Layer

- 세션 계층. (L5)
- 양 끝단 응용 프로세스가 통신을 관리하는 방법을 제공.
- 동시 송수신(Duplex), 반이중(Half-Duplex), 전이중(Full-Duplex) 방식을 확인.
- 통신하는 사용자들을 동기화하고 오류 복구 명령들을 주로 다룸.
- 단위는 메시지(Message).

## Presentaion Layer

- 표현 계층. (L6)
- 코드 간의 번역을 담당하여 사용자 시스템에서 데이터 형식상 차이를 해결함.
- 데이터 전송을 위한 암호화와 복호화를 진행함.
- ASCII, UTF-8 등 인코딩을 하는 것이 여기서 이뤄짐.
- 멀티미디어 파일(이미지, 소리, 동영상) 등의 인코딩도 여기서 이뤄짐.
- 단위는 메시지(Message).

## Application Layer

- 응용 계층. (L7)
- 응용 프로그램과 직접 관계를 맺어 서비스를 수행하는 계층.
- 단위는 메시지(Message).
- 주요 프로토콜은 HTTP, HTTPS, POP3, SMTP, FTP, Telnet, SSL 등이 있음.

> ## TCP/IP 4 Layer
> 
> TCP/IP 는 인터넷에서 주로 사용하는 프로토콜의 조합입니다.
> 
> 인터넷 네트워크의 시점에서 더 용이하게 다룰 수 있도록 OSI 7 계층을 4 단계로 최소화한 개념입니다.
> 
> 인터넷 모델 이라고도 부릅니다. 이들의 구성은 다음과 같습니다.
> 
> - 응용 계층 : OSI 응용 계층(L7), 표현 계층(L6), 세션 계층(L5)
> - 전송 계층 : OSI 전송 계층(L4)
> - 인터넷 계층 : 네트워크 계층(L3)
> - 네트워크 인터페이스 계층 : 데이터 링크 계층(L2), 물리 계층(L1)
  