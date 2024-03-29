---
layout: posts
title: "Bluetooth 세대별 특징"
permalink: /projects/bluetooth/generation/
prev: bluetooth
---

# Bluetooth 1

GFSK 변조 방식을 이용해 최대 1 Mbps, 실제로는 0.7 Mbps의 전송속도와 최대 10 m의 전파 범위를 지원한다.

# Bluetooth 2

Bluetooth 2.0은 2004년 3월에 발표되었다. 기존에 사용하던 GFSK 변좡식을 그대로 사용할 경우 1 Mbps의 전송속도를 유지하지만, Enhanced Data Rate(EDR)을 통해 최대 3 Mbps, 실제로는 2.1 Mbps의 속도가 지원된다.

EDR은 2 Mbps를 지원하는 π/4-DPSK와 3 Mbps를 지원하는 8-DPSK 변조 방식을 사용한다.

# Bluetooth 3

Bluetooth 3.0은 2009년 4월에 발표되었다. 이전 버전에 비해 8배 가량 향상된 24 Mbps의 속도를 제공한다. 그러나 이 속도는 사실 Wi-Fi 연결을 통해 전송되며 Bluetooth는 연결 설정 및 관리에만 사용된다.이를 High Speed(HS)라고 부르는데 HS가 포함되어 있지 않은 일반 모듈은 Bluetooth 2.0과 같이 3 Mbps이고, 3.0에서 표준화된 새로운 기능들(NFC 통합 기능, Enhanced Power Control 등) 정도만 제공한다.

# Bluetooth 4

BLE가 개발되면서부터 Bluetooth는 Bluetooth BR/EDR(Classic)과 Bluetooth LE로 나뉘게 된다. BR/EDR과 LE는 서로 다른 프로토콜 스택을 가지고 있기 때문에 서로 직접적인 통신이 불가능하다.

<div class="post__stage-container">
    <div class="post__stage">
        <img class="modal" src="/_pages/projects/bluetooth/images/generation/1.png" alt="<b>[Fig. 1]</b> Bluetooth 프로토콜 스택 <a href='#Reference'>[1]</a>."/>
    </div>
    <div class="post__stage">
        <img class="modal" src="/_pages/projects/bluetooth/images/generation/2.png" alt="<b>[Fig. 2]</b> Bluetooth 듀얼모드 <a href='#Reference'>[2]</a>."/>
    </div>
</div>

이에 [Fig. 1]과 같이 BR/EDR과 LE 스택을 모두 가지는 듀얼모드(Dual Mode)가 등장하게 된다.

- **BR/EDR** 통신만 가능한 그룹을 Bluetooth Classic
- **BR/EDR**과 **LE** 모두 가능한 그룹을 Dual Mode 또는 Smart Ready
- **LE**만 가능한 그룹은 Single Mode 또는 Smart 라고 부른다.

<img class="modal" src="/_pages/projects/bluetooth/images/generation/3.png" alt="<b>[Fig. 3]</b> Bluetooth Classic과 LE의 비교 <a href='#Reference'>[3]</a>."/>

BLE는 Advertise mode와 Connection mode 이렇게 2가지 모드를 통해 통신이 이루어진다. Advertise mode에서는 브로드캐스트 방식으로 데이터를 전송하며, Connection mode에서는 브로드캐스트 방식으로 전송된 데이터를 수신하는 디바이스와 1:1로 연결하여 데이터를 주고 받는다.

그래서 communication 토폴로지에는 P2P, broadcast, mesh 네트워킹이 있는데 기존의 BR/EDR에서는 P2P 방식의 통신 방법만 지원했다면 BLE에서는 broadcast와 mesh 방식이 추가되었다.

PHY 채널을 살펴보면 BR/EDR은 ISM 대역에 해당하는 2.402 ~ 2.480 GHz를 1 MHz 단위로 쪼개어 총 79개의 채널을 사용을 하였는데, BLE는 2 MHz 단위로 쪼개어 총 40개의 채널을 사용한다. 그 중 37, 38, 39 채널은 broadcast용 채널로 분류되어있다.

# Bluetooth 5

5 버전에서는 PHY layer에서 큰 변화가 있었다. 4 버전에서는 GFSK를 이용한 1 Mbps의 전송속도만 지원하였는데, 2 Mbps를 지원하는 'LE 2M', 전송거리 최대 4배를 지원하는 'LE 125K'와 'LE 500K'(합쳐서 'LE Coded')가 추가되었다. 전송 속도가 올라간 'LE 2M'은 간단하게 2LE, 전송거리가 증가한 'LE Coded'는 Bluetooth LE Long Range라 해서 BLR이라고 부르기도 한다.

<table class="posts__caption" alt="<b>[Table. 1]</b> BLE PHY Layer.">
  <thead>
    <tr>
        <th>PHY</th>
        <th>LE 1M</th>
        <th colspan="2">LE Coded (BLR)</th>
        <th>LE 2M (2LE)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td>Modulation</td>
        <td>1 Ms/s<br>GFSK</td>
        <td>1 Ms/s<br>GFSK</td>
        <td>1 Ms/s<br>GFSK</td>
        <td>2 Ms/s<br>GFSK</td>
    </tr>
    <tr>
        <td>Data Rate</td>
        <td>1 Mbit/s</td>
        <td>500 Kbit/s</td>
        <td>125 Kbit/s</td>
        <td>2 Mbit/s</td>
    </tr>
    <tr>
        <td>Error Detection</td>
        <td>CRC</td>
        <td>CRC</td>
        <td>CRC</td>
        <td>CRC</td>
    </tr>
    <tr>
        <td>Error Correction</td>
        <td>NONE</td>
        <td>FEC</td>
        <td>FEC</td>
        <td>NONE</td>
    </tr>
    <tr>
        <td>Range Multiplier</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>0.8</td>
    </tr>
    <tr>
        <td>Coded System<br>(Access Header)</td>
        <td>Uncoded</td>
        <td>S=8</td>
        <td>S=8</td>
        <td>Uncoded</td>
    </tr>
    <tr>
        <td>Coded System<br>(Payload)</td>
        <td>Uncoded</td>
        <td>S=2</td>
        <td>S=8</td>
        <td>Uncoded</td>
    </tr>
    <tr>
        <td>Bluetooth 5 Requirement</td>
        <td>Mandatory</td>
        <td>Optional</td>
        <td>Optional</td>
        <td>Optional</td>
    </tr>
  </tbody>
</table>

BLR의 경우에는, 블루투스 코어 사양은 0.1%의 BER을 한계로 정하였고, 중요한 점은 **전력 사용량을 증가시키지 않고 최대 허용 BER을 달성**한다는 것이다. 이를 위해 BLR에서는 Forward Error Correcting(FEC)를 수행한다. FEC 인코딩에는 S=2, S=8 두가지 옵션이 있으며 패턴 매퍼를 거쳐 1비트를 각각 2, 8심볼로 변환한다. 범위는 대략 각각 2, 4배로 증가하고, 대신 전송해야 하는 심볼 수가 늘어나 Application Layer의 전체 data rate은 감소하며 통신 시간이 길어져 평균 소비 전력이 증가한다.

2LE는 Modulation을 향상시켜 2배의 전송 속도를 달성했다. 그만큼 전송 시간이 줄어들어 배터리 향상과 주파수 효율성이 좋아지는 등의 효과를 볼 수 있다. 전송 속도 2배라고 되어있지만, 실제로 속도가 2배가 된다고 보기는 어렵고, 대역폭이 2배가 되어서 패킷 자체의 전송에 걸리는 시간이 반으로 줄어드는 것은 맞지만 오버헤드, 그러니까 패킷 사이의 간격은 그대로이기 때문에 전체 속도가 2배가 되지는 않는다.

PHY Update는 Host에서 PHY 변경 요청이 있을 경우 Link Layer에서 변경 요청 및 업데이트가 이루어진다. Central(Master) 뿐만 아니라 Peripheral(Slave)에서도 PHY Update를 시도할 수 있지만, 최종 결정권은 Master에게 있다.

그 밖에 오디오가 지원되기 시작했고 **Extended Advertising**이 도입되어 별도의 연결 과정 없이 정보를 전달하는 방법이 개선되었다. 기존의 37, 38, 39 채널 외에 나머지 37개의 채널을 보조 advertising 채널로 사용한다.



---

# <a name="Reference"></a>Reference

1. <a href='https://makersweb.net/embedded/14289' target='_blank'>MakersWeb</a>
2. <a href='https://community.silabs.com/s/share/a5U1M000000knyFUAQ/a-short-history-of-the-bluetooth-ble-standard-ble-beacons-and-gatt?language=en_US' target='_blank'>Silicon Labs</a>
3. <a href='https://www.bluetooth.com/learn-about-bluetooth/tech-overview/' target='_blank'>Bluetooth SIG</a>
{:.post__reference}