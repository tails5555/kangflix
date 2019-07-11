---
layout: post
title: "운영체제 기초 개념"
date: 2019-07-07 15:00:00 +09:00
image: "/assets/img/category/ct_os.png"
category: 'os'
tags:
- OS
- Background
description: 운영체제를 공부하기 이전에 알아두면 좋은 개념들을 정리합니다.
introduction: 운영체제를 공부하기 이전에 알아두면 좋은 개념들을 정리합니다.
---

## Operation System

운영체제(Operation System) 는 사용자가 하드웨어를 이용하여 소프트웨어를 실행할 수 있게 도와주는 오작교 같은 소프트웨어 입니다.

**특성**

- 시스템의 효율성을 향상 합니다.
- 사용자에게 편리한 User Interface 를 제공합니다.
- 하드웨어와 소프트웨어에서 사용 된 자원들을 관리합니다.

## Processor & Register

**Processor** 

- 컴퓨터의 모든 장치를 제어하고 명령을 실행하는 장치입니다.
- 운영체제와 가장 밀접한 관계를 가지고 있습니다.
- CPU(Central Processing Unit) 라고 합니다.

**Register**

- 프로세서에 위치한 고속 메모리 입니다.
- 프로세서가 기억해야 할 데이터를 임시 저장하는 포스트 잇과 같은 역할을 합니다.
- 컴퓨터 구조에 따라 종류가 다양합니다.
- 제일 큰 분류는 사용자의 정보 변경 여부에 따라 나뉩니다.

## Memory

메모리(Memory) 는 컴퓨터의 기억장치 입니다.

메모리의 종류는 다음과 같고, 아래로 내려갈수록 용량이 많아지고, 속도는 느려집니다.

물론 4번에서 1번까지 올라오면서, 휘발성은 점차 커집니다.

1. 레지스터 메모리 : 프로세서가 바로 사용할 수 있는 공간.
2. 캐시 메모리 : 프로세서와 메인 메모리의 속도 차이를 줄이는 고속 버퍼(Buffer).
3. 메인 메모리(주 기억 장치, RAM) : 프로그램 실행 시, 필요한 자원들을 적재해야 작동 가능한 공간.
4. 보조 기억장치 : 대용량의 자기 디스크. 프로그램, 각종 문서, 이미지, 동영상 등이 저장되어 있는 공간.

## System Bus

- 하드웨어를 물리적으로 연결하여 데이터를 주고 받는 경로입니다.
- 컴퓨터 안에 다양한 신호를 시스템 버스로 전달합니다.
- 기능에 따라 데이터 버스, 주소 버스, 제어 버스 3가지로 나뉩니다.

## Operation

명령어(Operations) 는 컴퓨터 시스템을 동작하기 위해 데이터를 가공하는 기계어 입니다.

명령어는 크게 연산 부호, 피 연산자 2 분류로 나뉩니다.

**연산 부호** 

프로세스가 실행할 동작인 연산을 지정합니다.

**피 연산자** 

연산할 데이터의 주소를 저장합니다. 데이터는 레지스터 혹은 메모리에 위치 합니다.

피 연산자의 위치를 명시하는 방법은 직접 주소, 간접 주소 2 가지로 나뉩니다.

## Operation Mechanism

![Operation_Cycle]({{ site.baseurl }}/assets/img/post/os/operation_cycle.png){: width="100%"}

명령어의 실행 과정은 크게 4가지로 나뉩니다.

**인출 사이클**

메모리에서 명령어를 읽은 후 명령어 레지스터(IR) 에 저장합니다.

명령어 실행 이후 프로그램 카운터(PC) 에 1를 더합니다.

**실행 사이클**

인출 명령어를 해독한 후 결과에 따라 제어 신호를 발생하여 명령어를 실행합니다.

**간접 사이클**

명령어를 수행하기 이전 실제 데이터가 저장된 주 기억 장치(RAM) 의 유효 주소를 한 번 더 읽습니다.

**인터럽트 사이클**

실행 사이클 완료 이후, 인터럽트 요구를 검사 합니다.

다음 명령어 인출 이후 인터럽트가 있으면 프로그램의 주소를 특정 장소에 저장하고 중단된 프로그램 시점으로 복귀합니다.

## Interupt

인터럽트(Interrupt) 는 입출력 장치나 프로그램에서 프로세스로 보내는 하드웨어 신호입니다.

인터럽트 신호를 받은 프로그램은 실행 중단 이후 다른 프로그램을 실행합니다.

물론 단일 프로세서 안에서도 인터럽트를 사용할 수 있습니다.

인터럽트는 사용자의 영향이 아니라 운영체제의 영향이 크기 때문에 자동으로 조치하는 편입니다.

인터럽트가 이러지는 사례는 다음과 같습니다.

- 예상하지 못 한 입력.
- 정전 및 자연 재해 발생.
- 컴퓨터 시스템의 긴급 요청.
- 명령어를 잘 못 실행함.
- 입출력 완료를 시스템에 적당하게 처리하기 위함.