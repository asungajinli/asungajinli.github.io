---
layout: posts
title: "A Reinforcement Learning Framework for PQoS in a Teleoperated Driving Scenario"
categories: Mobility
permalink: /study/paper_review/mobility_001/
prev: paper_review
---
# RAN-AI

<a href ="https://github.com/signetlabdei/ns3-ran-ai" target="_blank" rel="noopener noreferrer"><img src="https://img.icons8.com/ios-glyphs/120/null/github.png" width="15" height="15" style="box-shadow:none;"></a> [**ns3-ran-ai**](https://github.com/signetlabdei/ns3-ran-ai){:target="_blank"}

Matteo Drago 외 연구진들은 RAN-AI라는 ns3환경에서 시뮬레이션 되는 새로운 엔티티를 개발하였다.

매우 동적인 V2X 시스템에서 QoS는 언제든 예기치 못하게 변경 또는 저하될 수 있다. 사람의 안전과 직결되는 교통수단에서 통신 장애는 치명적인 결과를 초래할 수 있다. 이를 위해 QoS를 사전에 예측하여 그에 따라 애플리케이션을 통제한다는 개념인 PQoS(Predictive Quality of Service)를 도입했다. 바로 RAN-AI는 V2X 네트워크를 위한 PQoS 메커니즘이다.

## 전체적인 RAN-AI의 동작 과정

1. 애플리케이션 통계를 가져오고, gNB와 최종 사용자로부터 RL(강화학습) 에이전트의 [입력]({{ page.url }}#pqos-입력)으로 사용가능한 RAN 측정값(full-stack)을 수집한다.
2. RL 에이전트는 측정값(입력)을 바탕으로 전체 성능을 최대화 하는 최적의 [대응]({{ page.url }}#pqos-대응)을 결정한다.
3. 최종 사용자에게 QoS 변동사항을 알리고, 에이전트의 결정을 바탕으로 대응책을 제시한다.

## PQoS **입력**

- Context 정보:<br>
    운영 시나리오, 도로의 요소, 네트워크 구축, 시간에 대한 통합 정보
- 사용자 궤적:<br>
    드라이빙 애플리케이션은 최종 사용자의 궤적을 네트워크에 제공할 수 있으며, RAN-AI는 사용자가 위치하게 될 gNB에 대한 데이터(e.g., cell load)를 습득할 수 있다.
- 교통 정보:<br>
    RAN-AI는 외부 제어 센터로부터 트래픽 상태를 수집하고 데이터를 바탕으로 트래픽 예측을 제공할 수 있다.
- 네트워크 메트릭:<br>
    RAN-AI는 PHY 및 MAC 계층(e.g., RSRP, RSRQ, SINR, PRBs utilization, MCS), RLC 및 PDCP 계층(e.g., 사용자간 데이터 트래픽 통계)에서 측정된 데이터들을 얻을 수 있다.
- 상위 계층 메트릭:<br>
    RAN-AI는 사용자의 애플리케이션을 통해 E2E(end-to-end) 성능(e.g., delay와 throughput의 평균, 표준편차, min, max)에 대해 알 수 있다.

## PQoS **대응**

RAN-AI는 PQoS 입력을 바탕으로 적절한 조치(e.g., 스케쥴링 결정 변경, propagation condition의 function에 따른 무선자원할당 적용, 네트워크 용량에 기반한 traffic request 변조, system numerology 수정을 통한 탄력적인 통신 채널 제공)를 취해야 한다.

또 다른 방법으로는 전송 전 애플리케이션 계층에서 생성되는 데이터의 크기를 줄이는 것이다.
<br><br>

# 시뮬레이션

RAN-AI 시뮬레이션 수행은 ns-3를 통해 이루어졌다. 이는 ns3-gym 프레임워크를 확장한 형태이다.

## 구조

<img class="modal img__medium" src="/_pages/study/paper_review/teasers/mobility_001.png" alt="<b>[Fig. 1]</b> O-RAN 호환 architecture 및 workflow <a href='#Reference'>[1]</a>."/>

- [SUMO(Simulation of Urban MObility)](https://eclipse.dev/sumo/){:target="_blank"}<br>
    시뮬레이션 차량들은 SUMO를 통해 생성된 실제 길을 따라 이동.
- [GEMV 2](https://vehicle2x.net/){:target="_blank"}<br>
    V2V, V2I 통시을 위한 지정학적 propagation model.<br>

## *Setup*

논문 참고

## GEMV

[Google 어스로 KML 지도 데이터 가져오기](https://support.google.com/earth/answer/7365595?hl=ko&co=GENIE.Platform%3DDesktop){:target="_blank"}




---
# <a name="Reference"></a>Reference

1. M. Drago, F. Mason, T. Zugno, M. Giordani, M. Boban and M. Zorzi, "Artificial Intelligence in Vehicular Wireless Networks: A Case Study Using ns-3", Workshop on ns-3 (WNS3), 2022.
2. M. Boban, J. Barros and O. K. Tonguz, "Geometry-Based Vehicle-to-Vehicle Channel Modeling for Large-Scale Simulation," in IEEE Transactions on Vehicular Technology, vol. 63, no. 9, pp. 4146-4164, Nov. 2014, doi: 10.1109/TVT.2014.2317803.
{:.post__reference}