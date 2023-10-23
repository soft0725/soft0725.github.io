---
title: 자율주행에 필요한 기능들과 약어
date: '2023-10-23 12:16:00 +0900'
categories: [Autonomous Driving]
tags: [Autonomous Driving]
image: 
    path: /assets/img/autonomous_driving/autonomous_sdriving_functions.png
---


***

| 기능                    | 약어  | 설명                                       |
|------------------------|-------|------------------------------------------|
| 크루즈                    | CC : Cruise Control | 크루즈 컨트롤 시스템                       |
|                       | SCC : Smart Cruise Control   | 스마트 크루즈 컨트롤 시스템                 |
|                       | ASCC : Adaptive (Advanced) Cruise Control | 어댑티브 크루즈 컨트롤                    |
| | | 
|         차선             | LDWS : Lane Departure Warning System  | 차선 이탈 경보 시스템                      |
|                       | LKAS : Lane Keeping Assist System | 차선 유지 지원 시스템                      |
| | |         
|        추돌 방지               | FCW : Forward Collision Warning  | 전방 추돌 경보 시스템                      |
|                       | AEB : Autonomous Emergency Brake  | 자동 긴급 제동 시스템                      |
|| | 
| 사각지대 방지            | BCW : Blind-spot Collision Warning | 후측방 경보 시스템  |
|             | LCA : Lane Change Assist | 차선 변경 어시스트 시스템  |
| | | |
|      주차       | RCCW : Rear Cross-Traffic Collision Warning | 후방 교차 교통 충돌 경고  |
| | RCCA : Rear Cross-Traffic Collision-Avoidance Assist |후방 충돌 보조 시스템|
|                      | SPAS : Smart Parking Assist System  | 주차 조향 보조 시스템                     |
|                       | RSPA : Remote Smart Parking Assist | 원격 스마트 주차 보조                     |
|                       | RCTA : Rear Cross Traffic Alert | 후방 교차 교통 경보 |
| | |                  


## 크루즈 컨트롤 (CC)
자동차가 일정한 속도를 유지하며 달리는 것이다. 
고속도로에서는 일정한 속도를 유지하며 달리기 때문에 좋은 기능이다.
하지만 일반 국도나 정체가 심한 도로에서는 많이 멈춰야 하기 때문에 단점도 존재한다. 

## 스마트 크루즈 컨트롤(SCC)
크루즈 컨트롤에서 업그레이드 된 버전으로 앞 차와 간격을 유지하며 달리게 된다. 
또한 앞쪽에 레이더가 장착되면서 사람, 자동차 등등 많은 것들을 인식하여 위험할 경우 브레이크를 작동해 차를 멈추게 한다.

## 어댑티브 크루즈 컨트롤 (ASCC)
스마트 크루즈 컨트롤은 전방 충돌 방지 보조 시스템으로 브레이크가 작동되면 멈춘다.
하지만 어댑티브 크루즈 컨트롤은 멈췄다가 다시 앞으로 가는 기능까지 더해졌다.


또한 내비게이션 기반으로 돌아가는 크루즈 컨트롤도 있다.
이것의 자세한 설명은 생략하도록 하겠지만 대충 알아보자면 내비게이션 기반으로 감속 구간에서는 
감속을 하고 주행속도가 n km/h 이상인 곳에서는 가속을 하는 시스템이다.

출처 : [크루즈 컨트롤 종류와 설명](https://m.post.naver.com/viewer/postView.naver?volumeNo=33508906&memberNo=35796412)

<br>


## 차선 이탈 경보 시스템 (LDWS)
차선을 인식하여 차량이 차선을 넘는지 넘지 않는지를 판단하는 기술이다. 
기본적으로 시스템이 작동하는 조건은 `60 km/h 이상, 방향 지시등 X` 일때 작동한다.

- 원리
	- 소실점을 이용하여 소실점이 차량의 중심과 일치 할 때는 정상 주행으로 판단
	- 소실점이 차량의 중심과 다르다면 차선 이탈로 경보 이벤트 발생 

## 차선 유지 보조 시스템 (LKAS)
LDWS보다 업그레이드 된 기능으로 차선 이탈 경보만이 아니라 스티어링휠(MDPS)을 제어하여 운전자가 차선을 유지할 수 있도록 보조하여 준다.

방향 지시등 또는 양쪽 차선이 인식되지 않는 경우 시스템이 작동하지 않는다.

출처 : [엠에스리](https://m.blog.naver.com/lagrange0115/220990235341)

<br>


## 후측방 경보 시스템 (BCW) & 차선 변경 어시스트 시스템 (LCA)
- BCW
	- 차량 뒷범퍼에 있는 센서를 통해 사각지대에 있는 자동차의 여부를 알려준다.
- LCA
	- 차량 후방에서 고속 접근 차량에 대해 경보를 하는 시스템이다.
	- 약 4.5초 뒤에 충돌할 것이 예상될 때 경보가 작동한다.

출처 : [엠에스리](https://m.post.naver.com/viewer/postView.naver?volumeNo=30244005&memberNo=28844427)
영상 설명 : [Blind-spot Collision Warning (BCW) on Hyundai](https://www.youtube.com/watch?v=BcHcfhn5_gg)



## 후방 교차 교통 충돌 경고 (RCCW) & 후방 충돌 보조 시스템 (RCCA)
- RCCW 또는 (RCTA 라고도 부름)
	- 측면에서 접근하는 차량을 감지하였을 때 작동된다. 
- RCCA 
	- RCCW에서 충돌 위험이 감지 되면 RCCA가 브레이크를 작동하여 차량을 멈춘다.

차량이 8 km/h ~ 36 km/h의 속도로 이동할 때 감지하여 제동한다. 

출처 : [카수리](https://post.naver.com/viewer/postView.naver?volumeNo=27892134&memberNo=30632401)

<br>

## 주차 조향 보조 시스템 (SPAS)
차체 사방의 센서로 주차 공간을 탐색하고 차량이 자동으로 스티어링 휠을 조작하여 차량을 주차하는 시스템 
운전자는 기어와 브레이크만 조작하면 된다.

출처 : [개미뚠뚠](https://m.blog.naver.com/papawolf8/220801686376)
영상 설명 : [르노코리아자동차](https://www.youtube.com/watch?v=OAYqjk2phwc)

## 원격 스마트 주차 보조 (RSPA)
사용자가 차량에 탑승하지 않고 키로 차량을 제어하는 기술 
대표적인 기술로는 
- 스마트 주차 
- 원격 스마트 주차 
- 스마트 출차 

출처 : [엠에스리](https://blog.naver.com/PostView.naver?blogId=lagrange0115&logNo=222650687242)


<br>
자율주행에 들어가는 기능들에 대한 설명과 약어는 이정도로만 정리하고 다음부터는 한 기능들 마다 구현을 해보거나 자세하게 정리하도록 하겠다. 


