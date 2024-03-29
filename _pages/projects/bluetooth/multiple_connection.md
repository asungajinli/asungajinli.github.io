---
layout: posts
title: "Bluetooth 다중 연결"
permalink: /projects/bluetooth/multiple_connection/
prev: bluetooth
---

Bluetooth 기기 여러 대를 동시에 연결할 수 있을까? Bluetooth를 일상생활에서 항상 활용하는 여러분들도 아마 매번 헷갈려하는 문제일 것이다. 여러 대를 동시에 연결한다는 것은 point-to-point, 즉 일대일 연결을 말하는 것이다. Broadcast 방식의 단방향 전송은 해당하지 않는다.

Blueooth 제품을 만들기 앞서 다중 연결 여부를 고려하는 것은 중요하다. 다중 연결이 필요할 경우 고려해야 할 상황과 방안을 알아보도록 하자.

# Coexistence And Collocation

우선 그러기 위해서는 Bluetooth의 다중 분할 방식에 대해 알아볼 필요가 있다. 상세한 내용은 Bluetooth Core Specification<sup><a href='#Reference'>[1]</a></sup>의 285 페이지(또는 섹션 7)을 참고하기 바란다.

Bluetooth는 알다시피 2.4 GHz의 ISM 대역을 사용하기 때문에 같은 대역을 사용하는 무선 장치들과의 간섭을 피하는 것이 중요하다. 이를 위해 크게 FDD와 TDD 다중 분할 방식을 사용한다. Isolation이 충분할 경우 FDD 방식을 채택하고, isolation이 부족하거나 공유 안테나의 경우 TDD 방식을 사용한다.

| Feature                        | Version | Introduced Description                                          |
|--------------------------------|---------|-----------------------------------------------------------------|
| Adaptive Frequency Hopping    | 1.2     | Allows devices to reduce the number of channels used in a piconet in order to avoid interferers |
| HCI Set Host Channel Classification | 1.2     | Allows a Host to inform the local Bluetooth Controller of the channels that are occupied by a collocated technology |
| Enhanced SCO (eSCO)           | 1.2     | Added retransmissions to SCO for the purpose of combating interference |
| MWS Coexistence Signaling (CSA3) | 1.2     | Provides a standardized interface between collocated radios for communicating information necessary to enable some coexistence techniques |
| Piconet Clock Adjust          | 4.1     | Allows a Bluetooth device to align the piconet clock with an external technology, e.g. Long Term Evolution (LTE) |
| Train Nudging                 | 4.1     | Provides a mechanism to improve the success rate of page and inquiry when the slots to receive the respective responses are periodically not available |
| Generalized Interlaced Scanning | 4.1     | Provides a mechanism to improve the success rate of page scan and inquiry scan when some slots are periodically not available for scanning |
| Slot Availability Mask        | 5.0     | Provides a mechanism for two Bluetooth devices to indicate to each other the availability of their time slots |
{:.posts__caption alt="<b>[Table. 1]</b> Interference mitigation features <a href='#Reference'>[1]</a>."}

위 [Table. 1]은 Core Specification에 나와있는 기능을 그대로 가져와 본 것이다. 여기에 있는 기능들을 다 다루지는 않고 Bluetooth 다중 연결을 위한 몇가지만 알아보겠다.

## Adaptive Frequency Hopping

Frequency Hopping는 Bluetooth 장치가 간섭을 일으키지 않게 하기 위한 가장 기본적인 기능이다. 그 중 Adaptive Frequency Hopping(AFH)는 'Adaptive(적응형)' 말그대로 상황에 따라 능동적으로 채널을 사용하겠다는 것이다.




# Bluetooth Mesh

Bluetooth는 LE를 기반으로 하는 Mesh 네트워크를 지원한다. Mesh는 다대다 통신이 가능한 구조로 주로 스마트홈이나 스마트빌딩 등 IoT 환경에서 주로 사용된다. 이미 Zigbee, WiFi, Thread 등 Mesh 네트워크를 구축하기위한 여러 프로토콜이 있지만, Bluetooth Mesh가 가지는 장점이 존재한다.

우선 Mesh 네트워크의 데이터 전달방식에 대해 알아볼 필요가 있다. **Routing** 방식과 **Flooding** 방식이 있는데, Zigbee와 Thread가 Routing 방식을 사용하고, Bluetooth는 Flooding 방식을 사용한다. Routing은 말그대로 각 네트워크 노드가 라우팅 테이블을 가지고 있고, 이를 기반으로 해당 주소로 데이터를 보낸다. Flooding은 노드에 데이터가 들어오면 주변 노드로 broadcast하여 데이터를 전달한다. Flooding이 직역하면 '홍수'라는 말에서 알 수 있듯 데이터가 홍수처럼 퍼져나간다고 생각할 수 있다.

<img class="modal img__small" src="/_pages/projects/bluetooth/images/multiple_connection/1.webp" alt="<b>[Fig. 1]</b> BLE meshnets with managed flooding and routing <a href='#Reference'>[2]</a>."/>

받은 데이터를 계속해서 broadcast하게 되면, 데이터 수가 너무 많아질 뿐더러 영원히 사라지지 않는것이 아닐까 하는 생각이 들 수 있다. 이를 방지하기 위한 여러가지 기능이 있지만, 대표적인 것이 data cache와 Time To Live(TTL)이다. 각 노드는 이미 보낸 데이터를 cache하고 있어서 cached 데이터와 동일한 데이터가 들어올 시에는 전송시키지 않는다. TTL은 쉽게 말해 데이터에 수명을 부여하는 방식이다. 홉을 지나갈 때마다 TTL을 1씩 감소시키고, TTL이 0이 되면 해당 데이터는 폐기한다.

Routing 기반 Mesh 네트워크를 사용하기 위해서는 네트워크 장치에 routing table을 저장하기 위한 충분한 RAM 확보가 필요하고 노드의 추가, 삭제 시 라우팅 테이블 변경으로 인한 낮은 안정성과 유지관리가 어렵다는 단점이 있다. 그러나 Flooding 방식에 비해 홉 수에 의한 영향을 덜받는다. 또 기본적으로 data rate이나 latency 성능이 더 좋다.

Silicon Labs에서 Zigbee, Thread, BLE Mesh를 비교한 자료<sup><a href='#Reference'>[3]</a></sup>가 있는데, 참고하면 좋을 것 같다.

<table class="posts__caption" alt="<b>[Table. 2]</b> Thread, Zigbee, Bluetooth Mesh의 비교.">
    <thead>
        <tr>
            <th>Thread</th>
            <th>Zigbee</th>
            <th>Bluetooth</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <ul>
                    <li>라우팅 방식</li>
                    <li>IPv6 기반</li>
                    <li>라우터 수가 제한되어 있으며 라우터 당 최대 511개의 장치에 연결 가능</li>
                    <li>따라서 대규모 네트워크보다는 고밀도 메시 넷이 적합</li>
                    <li>유사 기술에 비해 높은 데이터 전송률</li>
                    <li>로컬 시스템에 적합하며 장거리 데이터 전송용으로는 적합하지 않음</li>
                </ul>
            </td>
            <td>
                <ul>
                    <li>라우팅 방식</li>
                    <li>낮은 데이터 속도 (최대 250 Kbps)</li>
                    <li>다양한 주파수 및 전력 범위 지원으로 다양한 전송 거리 지원</li>
                    <li>BLE를 포함한 다양한 트랜시버와 함께 작동 가능</li>
                    <li>스마트폰과 같이 Zigbee 송수신기가 없는 장치를 네트워크에 추가하려면 게이트웨이를 사용해야 함</li>
                </ul>
            </td>
            <td>
                <ul>
                    <li>플러딩 방식</li>
                    <li>다중 노드 네트워크에서 관리형 플러딩을 사용할 경우 많은 노이즈, 오버헤드가 발생</li>
                    <li>이를 줄이기 위해 필터링 알고리즘을 개발하거나 고유 식별자가 있는 가상 주소 사용</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>


---

# <a name="Reference"></a>Reference

1. Woolley, Martin (7 February 2023). "[Bluetooth® Core Specification Version 5.4](https://www.bluetooth.org/DocMan/handlers/DownloadDoc.ashx?doc_id=556599){:target="_blank"}" (PDF). bluetooth.com. Retrieved 19 February 2024.
2. Andrey Solovev, Anna Petrova, "Bluetooth Mesh: Technology Overview, Examples, Alternatives, and First-Hand Experience," <i>Integra Sources Blog</i>, 2019. [Online]. Available: [https://www.integrasources.com/blog/bluetooth-mesh-network-tutorial/](https://www.integrasources.com/blog/bluetooth-mesh-network-tutorial/){:target="_blank"}. [Accessed: 10- Feb- 2024].
3. "Benchmarking Bluetooth Mesh, Thread, and Zigbee Network Performance," <i>Silicon Labs</i>, [Online]. Available: [https://www.silabs.com/wireless/multiprotocol/mesh-performance](https://www.silabs.com/wireless/multiprotocol/mesh-performance){:target="_blank"}. [Accessed: 20- Feb- 2024].
{:.post__reference}
