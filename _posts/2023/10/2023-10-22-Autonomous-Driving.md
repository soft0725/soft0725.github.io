---
title: 자율주행 기초
date: '2023-10-22 22:12:00 +0900'
categories: [Autonomous Driving]
tags: [Autonomous Driving]
image: 
    path: /assets/img/autonomous_driving/autonomous_sdriving.png
---

자율주행은 사람의 개입없이 스스로 주행하는 것을 말한다.

### 자율주행의 단계는 4단계로 구분 가능

- level 0
	- 운전자가 수동으로 작동하는 단계
- level 1
    - 운전자의 편의를 위한 특정 자동화 기능들이 추가
    - 크루즈 컨트롤, 차선 이탈 등등..
- level 2
    - ADAS가 복합적으로 차량 제어
- level 3
    - 운전자의 도움없이 교통 신호와 도로 흐름을 인식해서 주행
    - 위험한 상황이나 특수 상황에서는 운전자 개입 필요
- level 4
    - 차량이 스스로 안전한 주행이 가능한 수준에 도달한 단계
    - 대표적으로 테슬라가 있다.
- level 5
    - 영화에 나오는 차량이라고 생각하면 된다.

출처 : `Tech Issue - 자율주행 기술의 성장 단계와 3가지 적용 사례_자율주행 기술의 현재 그리고 미래`


### 자율주행 보조 시스템의 종류

- ADAS
    - 차선이탈 경고 (LDW)
    - 차선유지보조 (LKA)
    - 보행자충돌경고 (PCW)
    - 자동비상제동 (AEB)
    - 지능형조명제어 (ALC)

- 인, 케빈 모니터링 카메라 **동승자를 위주로**
    
- 후방 카메라
    
- AroundView Monitoring (AVM)
    - 하늘에서 차량을 내려다 보는듯한 화면을 보여줌
    - 앞, 뒤, 옆을 재구성해서 보여줌

- Drive Monitoring System (DMS) **운전자를 위주로**
    - 졸음 경보
    - 전방 미주시
    - 하품(피로)
    - 휴대폰
    - 흡연

위 기술들을 사용하려면 컴퓨터 비전이라는 것을 알아야함


### 컴퓨터 비전 (Computer Vision)

기계가 이미지를 자동으로 인식하고 정확하고 효율적으로 설명하는 데 사용하는 기술

**가장 많이 쓰이는 기술**

- Face Recognition
    - Apple의 Face ID와 같다고 생각하면 된다.
- Image Classification
    
- Object Detection
    
- Emotion Detection
    
- Object Tracking
    
- Video Analytics
    - 비디오에 위 기술을 사용하여 더 많은 정보를 분석
- Segmentation
    - 각 픽셀이 어디에 속하는지 더 자세하게 알려줌


### 차량과 컴퓨터 비전

차량에서 컴퓨터 비전은 어디에서 쓰일까?

차량에 달려있는 카메라로 주변에 사람, 차량 등등을 인식한다.

- 이때 컴퓨터 비전 기술을 사용함

대표적으로 사용 되는 것

- Face Recognition
- Object Detection
- Segmentation


<br>

다음 글에서는 차선이탈 경고 (LDW) 이런 것 처럼 기능들에 대해서 알아보겠다.