---
title: "[논문리뷰] Evaluating Wi-Fi Performance for VR Streaming: A Study on Realistic HEVC Video Traffic"
summary: "VR 스트리밍을 위한 Wi-Fi 성능 평가 논문 리뷰 (arXiv 2026)"
excerpt: "VR 스트리밍을 위한 Wi-Fi 성능 평가 논문 리뷰 (arXiv 2026)"
date: 2026-07-07
last_modified_at: 2026-07-07

categories:
  - 논문리뷰

tags:
  - Virtual Reality
  - Wi-Fi
  - IEEE 802.11
  - Video Streaming
  - QoS

layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
mathjax: true

paper:
  title: "Evaluating Wi-Fi Performance for VR Streaming: A Study on Realistic HEVC Video Traffic"
  authors: "Ferran Maura, Francesc Wilhelmi, Boris Bellalta"
  affiliations: "Universitat Pompeu Fabra, Barcelona"
  links:
    - name: "Paper"
      url: "https://arxiv.org/abs/2601.16950"
    - name: "Github"
      url: ""
    - name: "Project"
      url: ""
---

{% include paper-info.html %}

<div class="paper-summary-box" markdown="1">

**한 줄 요약**  
이 논문은 실제 HEVC 인코딩 영상 트래픽을 802.11 시뮬레이션에 결합한 에뮬레이션 프레임워크를 개발하여, 다양한 코덱·네트워크 설정에서 Wi-Fi가 VR 스트리밍을 지원할 수 있는 용량을 분석하고, Intra-refresh(IR) 코딩이 지연 변동성을 줄여 QoS를 개선하며 CBR 100 Mbps 기준 최대 4명의 동시 사용자를 지원할 수 있음을 보인다.

</div>

<figure class="paper-figure paper-figure--wide">
  <img src="{{ '/assets/images/paper_review/vr-wifi/front.png' | relative_url }}" alt="VR Wi-Fi streaming framework overview">
</figure>

## Abstract / 요약

### 1. Original Abstract

<details markdown="1">
<summary><strong>Original Abstract 보기</strong></summary>

> Cloud-based Virtual Reality (VR) streaming presents significant challenges for 802.11 networks due to its high throughput and low latency requirements. When multiple VR users share a Wi-Fi network, the resulting uplink and downlink traffic can quickly saturate the channel. This paper investigates the capacity of 802.11 networks for supporting realistic VR streaming workloads across varying frame rates, bitrates, codec settings, and numbers of users. We develop an emulation framework that reproduces Air Light VR (ALVR) operation, where real HEVC video traffic is fed into an 802.11 simulation model. Our findings explore Wi-Fi's performance anomaly and demonstrate that Intra-refresh (IR) coding effectively reduces latency variability and improves QoS, supporting up to 4 concurrent VR users with Constant Bitrate (CBR) 100 Mbps before the channel is saturated.
</details>

### 2. 한국어 요약

클라우드 기반 VR 스트리밍은 높은 처리량과 낮은 지연을 동시에 요구하기 때문에 802.11 네트워크에 상당한 부담을 준다. 여러 VR 사용자가 하나의 Wi-Fi를 공유하면 상향/하향 트래픽이 빠르게 채널을 포화시킨다.

본 논문은 프레임률, 비트레이트, 코덱 설정, 사용자 수를 변화시키며 802.11 네트워크가 현실적인 VR 스트리밍 워크로드를 지원할 수 있는 용량을 조사한다. 이를 위해 실제 HEVC 영상 트래픽을 802.11 시뮬레이션 모델에 입력하는, ALVR 동작을 재현하는 에뮬레이션 프레임워크를 개발한다.

실험 결과, Wi-Fi 성능 이상(performance anomaly) 현상을 분석하고, Intra-refresh(IR) 코딩이 지연 변동성을 효과적으로 줄여 QoS를 개선하며, 채널 포화 이전까지 CBR 100 Mbps 기준 최대 4명의 동시 VR 사용자를 지원할 수 있음을 보인다.


## 서론

Extended Reality(XR)는 게임을 넘어 원격 협업, 가상 훈련·교육, 원격 의료, 산업 기계 원격 조작 등 다양한 분야로 확장되고 있는 핵심 기술이다. 그중 클라우드 VR 스트리밍은 강력한 원격 서버에서 콘텐츠를 렌더링·인코딩하여 성능이 낮은 단말(HMD)로 스트리밍하는 방식으로, 단말의 하드웨어 요구 사항을 크게 낮출 수 있다.

이 구조에서 서버는 영상·오디오를 인코딩하여 HMD로 전송하고, HMD는 사용자의 자세와 움직임을 추적하여 tracking 데이터를 서버로 되돌려 보낸다. 이 피드백을 바탕으로 새로운 프레임이 렌더링되어 다시 HMD로 전송된다. 종단 간 지연이 충분히 낮게 유지되기만 하면, HMD 자체 렌더링 성능을 넘어서는 고품질 그래픽을 구현할 수 있다.

유선 연결은 이러한 응용을 잘 지원하지만, 사용자의 이동성과 편의성 때문에 실무에서는 Wi-Fi(IEEE 802.11)가 선호된다. 그러나 실시간 VR 스트리밍의 엄격한 지연·신뢰성 요구를 Wi-Fi로 충족하기는 쉽지 않다. 그 이유는 다음과 같다.

- 802.11은 DCF를 통한 랜덤 채널 접근을 사용하므로 단말들이 매체 접근을 위해 경쟁해야 한다.
- 서버, AP, HMD(STA)가 상향/하향 전송을 조율하지 않아 경험 품질이 저하될 수 있다.
- 같은 채널을 사용하는 인접 네트워크의 간섭이 예측 불가능한 방해를 일으킬 수 있다.

본 논문의 핵심 novelty는 802.11 시뮬레이션 내부에 실제로 인코딩된 영상 전송을 사용한다는 점이다. 이를 통해 서로 다른 코덱 설정에서 발생하는 프레임 크기 분포를 정확히 재현할 수 있다. 주요 기여는 (1) 서버-HMD 간 하나 또는 다수의 VR 스트리밍 세션을 802.11 위에서 에뮬레이션하는 모듈형 프레임워크 개발, (2) 코덱 파라미터·네트워크 경쟁·PHY 조건이 QoS 지표에 미치는 영향을 통합적으로 분석한 것이다.


## 배경

### 1. 클라우드 VR 스트리밍 구조

VR 스트리밍에서 렌더링은 일반적으로 서버에서 수행되며, 서버는 영상·오디오·햅틱 데이터를 인코딩하여 HMD로 전송한다. HMD는 사용자의 자세를 지속적으로 추적하여 tracking 패킷을 서버로 전송하고, 서버는 이 피드백으로 사용자 위치를 갱신하여 다음 프레임을 렌더링한다.

대표적인 구현으로 ALVR(Air Light VR)과 WiVRn이 있다. ALVR은 MIT 라이선스의 VR 스트리밍 애플리케이션으로, SteamVR 서버와 HMD 클라이언트 사이의 무선 브리지 역할을 한다. 서버는 영상·오디오·햅틱 데이터를 전송하고 클라이언트는 tracking 정보와 통계를 되돌려 보낸다. ALVR은 이미지 경계의 해상도를 낮춰 인코딩 효율을 높이는 foveated rendering, 급격한 머리 움직임을 보상하는 reprojection 같은 VR 특화 기능도 지원한다.

### 2. 실시간 스트리밍을 위한 영상 코딩

서버-클라이언트 간 영상 트래픽은 raw RGB 대비 대역폭을 크게 줄이기 위해 압축된다. 다만 압축은 프레임마다 인코딩·디코딩 지연을 유발하여 종단 간 지연을 증가시킨다. H.264, HEVC 같은 최신 코덱은 프레임을 GoP(Group of Pictures) 단위로 인코딩하며, GoP는 I-frame(intra-coded)과 P-frame(predicted)으로 구성된다. 실시간 스트리밍에서는 미래 프레임을 필요로 하는 B-frame은 사용하지 않는다.

HEVC의 IR(Intra-refresh) 모드는 I-frame 코딩 단위를 여러 프레임에 걸쳐 점진적으로 주입하는 방식이다. 이는 프레임 손실 상황에서의 견고성을 높일 뿐 아니라, 프레임 크기 분포를 덜 변동적으로 만든다. 이 특성이 이후 실험에서 핵심 비교 축이 된다.

### 3. 높은 QoE를 위한 요구 사항

HMD 화면은 눈과 매우 가깝기 때문에, VR 스트리밍은 높은 해상도와 비트레이트를 요구한다. 본 논문은 10~100 Mbps 범위의 비트레이트를 고려한다. 지연은 두 가지로 구분한다.

- **Motion-to-Photon(MTP) 지연**: 물리적 움직임과 HMD 상 시각적 갱신 사이의 지연. ITU-T는 360º VR 경험에서 MTP 지연이 50 ms 이하일 것을 권고한다.
- **네트워크 지연**: 클라우드 VR 게이밍처럼 강한 상호작용이 필요한 경우 RTT ≤ 20 ms가 요구된다.

ALVR에서는 하나의 VF(Video Frame)를 이루는 조각(fragment) 패킷이 하나라도 손실되면 전체 프레임이 손실된 것으로 간주된다. 일반적인 비트레이트에서 한 VF는 수십 개 패킷으로 구성되므로, 0.01%의 작은 손실 확률도 약 1% 수준의 FLR(Frame Loss Ratio)로 이어질 수 있다. 본 논문은 원활한 경험 기준으로 VF-RTT 33 ms 이하, 전송 프레임의 99% 이상 성공 수신, 즉 **FLR ≤ 1%** 및 **네트워크 지연 ≤ 33 ms**를 수용 가능한 QoE 임계값으로 채택한다.


## Method

본 논문의 핵심은 실제 인코딩된 영상 트래픽을 802.11 시뮬레이션에 결합한 에뮬레이션 프레임워크이다. 프레임워크는 Rust로 구현되었으며, 이산 사건 시뮬레이션을 위해 NexoSim 라이브러리를 사용한다. 서버, 클라이언트, STA, AP 각 구성 요소가 모듈로 분리되어 있고, 서버-클라이언트 블록은 네트워크 모델과 분리되어 802.11 장치들의 공유 채널 동작을 별도로 특성화한다.

### 1. VR 서버

SteamVR과 ALVR의 split rendering 역할은 설정 가능한 인코딩/디코딩 파이프라인으로 대체된다. 이 파이프라인은 4K 영상을 다양한 프레임률·비트레이트·트랜스코딩 파라미터로 처리할 수 있다.

- 오디오 패킷은 10 ms마다 쌍으로 전송되며, 내용은 비어 있고 합산 크기는 2000 바이트이다.
- 영상은 FFmpeg를 호출해 샘플 콘텐츠를 $T_{\text{CHUNK}}$초 단위의 인코딩 청크로 트랜스코딩하여 생성한다. 사용자 정의 설정(코덱 preset, 비트레이트, GoP 크기, IR)이 적용된다.
- 인코딩된 버퍼에서 단일 HEVC NAL 단위를 일정 FPS로 추출하여 패킷으로 조각화한 뒤, stream socket을 통해 버스트 전송한다.

청크 기반 인코딩은 ABR(Adaptive Bitrate) 알고리즘 통합을 용이하게 하고, 프레임 단위 인코딩 대비 계산 부하를 줄인다.

### 2. VR 클라이언트

클라이언트는 $3 \times \text{FPS}$의 비율로 단일 UL tracking 패킷을 주기적으로 전송한다. 영상 프레임의 모든 조각을 수신하면 ALVR receive socket이 원본 VF를 복원한다. 첫 조각을 받은 뒤 0.1초 이내에 프레임이 완전히 복원되지 않으면 폐기하고, 즉시 UL 패킷으로 프레임 손실 보고를 전송한다.

성공적으로 복원된 프레임은 용량 $B_{\text{DEC}}$의 jitter buffer에 저장된다. 이 버퍼는 네트워크 지연 변동을 완화하고 일정한 재생률을 유지한다. 시뮬레이션된 vsync 메커니즘이 일정 FPS로 프레임을 꺼내 디코딩하고 최종 RGB 출력을 표시한다.

### 3. Wi-Fi 네트워크

Wi-Fi는 IEEE 802.11be(Wi-Fi 7)를 표현하는 이산 사건 시뮬레이터로 에뮬레이션된다. RTS/CTS 메커니즘을 포함한 DCF를 구현하며, 802.11be MCS 테이블에 따라 수신 전력 기반 다중 전송률, 재전송, 단일 사용자 MIMO, A-MPDU를 통한 패킷 집성을 지원한다. (단, MLO 같은 고급 기능은 아직 포함되지 않음)

수신 전력은 [13]의 TMB 실내 경로 손실 모델로 계산하여 사용자별 MCS를 선택한다. RSSI가 −46 dBm를 초과하면 최고 전송률인 $\text{MCS}_{13}$이 선택된다. OFDMA 같은 기능은 포함하지 않으며, A-MPDU 내 각 데이터 패킷은 10%의 오류 확률을 가져 MAC 계층 재전송으로 이어진다.


## Experiments / Analysis

### 1. Experimental Setup

| 항목 | 내용 |
|---|---|
| Task | Wi-Fi 상 VR 스트리밍 QoS 평가 |
| Codec | HEVC (FFmpeg, *fast* preset) |
| 영상 샘플 | *BigBuckBunny* (평균 12.006 Mbps), *snow* (평균 86.627 Mbps), 3840×2160 @ 60 FPS |
| 코덱 비교 축 | IR vs GoP size 30 / 90 |
| Metric | VF-RTT, Channel Utilization(CU), FLR, VMAF |
| 주요 파라미터 | 5 GHz, 80 MHz, 20 dBm, A-MPDU 최대 64 packets, $T_{\text{CHUNK}}$ 1.5 s, $B_{\text{DEC}}$ 2 frames |

고FPS 샘플 없이 높은 프레임률을 재현하기 위해, 시뮬레이션 FPS와 원본 FPS의 비율에 비례하여 FFmpeg 인코딩 비트레이트를 스케일링한다. 평가 지표는 다음과 같다.

- **VF-RTT**: 서버가 완전한 VF를 전송하고 대응하는 UL 통계 패킷을 수신하기까지의 시간. 애플리케이션이 체감하는 네트워크 지연을 반영한다.
- **CU**: 전송·충돌에 소요된 시간과 전체 시뮬레이션 시간의 비율.
- **FLR**: 클라이언트가 완전히 수신하지 못한 VF의 비율.
- **VMAF**: 디코딩된 RGB 프레임을 고비트레이트(100 Mbps) 기준과 비교한 0~100의 perceptual quality 점수.

### 2. Main Results

**(A) GoP 크기·IR·비트레이트의 영향 (단일 HMD, AP로부터 1.5 m, 90 FPS)**

- IR은 GoP 대비 프레임 크기와 VF-RTT 변동성을 크게 줄이지만, 중복성 증가로 인해 VMAF는 약간 낮아진다.
- 더 큰 GoP는 I-frame 빈도를 낮춰 변동성을 줄이고 압축 효율을 높여, 동일 비트레이트에서 VMAF를 소폭 향상시킨다.
- VMAF는 높은 비트레이트에서 이득이 감소한다. 60 Mbps만으로도 모든 코덱 설정에서 양호한 perceptual quality(VMAF ≈ 90)를 달성한다.
- 흥미롭게도, 80 Mbps IR 스트림은 40 Mbps GoP 스트림과 유사한 VF-RTT 분산과 VMAF 범위를 보인다.
- **권고**: 지연 안정성을 위해 낮은 비트레이트의 GoP보다는 **높은 비트레이트의 IR**을 우선하는 것이 바람직하다.

**(B) VR 사용자 수 증가의 영향 (*snow*, CBR 100 Mbps, 1.5 m)**

- FLR은 사용자 3명까지는 1% 미만으로 유지된다.
- 사용자 4~5명에서 VF-RTT 변동성이 급격히 증가하며(중앙값 약 20 ms, 50 ms), FLR이 1%를 초과한다.
- 따라서 **4명**이 100 Mbps CBR 스트림 기준 QoS를 유지할 수 있는 한계 사용자 수이다.
- IR은 일관되게 더 낮은 VF-RTT 분산을 보이지만, 채널 포화는 코덱·FPS 선택과 무관하게 4명 지점에서 발생한다.
- 높은 FPS는 전송 빈도가 늘어 CU를 증가시키며, 5~6명에서는 네트워크 혼잡으로 인해 오히려 더 큰 A-MPDU 전송이 발생해 CU가 감소하기 시작한다.

**(C) AP-HMD 거리 및 이질적 MCS의 영향 (두 사용자)**

- 전송률은 거리에 따른 MCS에 의존한다. 낮은 MCS 사용자는 더 많은 airtime을 소비하여 다른 사용자의 큐잉 지연을 크게 증가시킨다 — 이것이 **Wi-Fi 성능 이상(performance anomaly)** 현상이다.
- User #2가 AP에서 멀어지면, 유리한 위치에 있는 User #1의 지연 QoS까지 함께 저하된다.
- 이 현상은 코덱·FPS 선택과 무관하며, User #1이 11 m에 있는 경우에는 모든 설정에서 33 ms 임계값을 초과할 정도로 지연 저하가 심화된다.

### 3. Additional Observations

핵심 관찰은 성능 저하가 **개별 사용자에 국한되지 않는다**는 점이다. 한 사용자의 열악한 채널 조건(먼 거리, 낮은 MCS)이 큐잉 지연을 통해 전체 네트워크의 다른 사용자에게까지 전파된다. 이는 실제 다중 사용자 VR 배치에서 최악 조건 사용자가 전체 QoS의 병목이 될 수 있음을 시사한다.


## 6. Discussion

### 1. 장점

1. 실제 HEVC 인코딩 트래픽을 802.11 시뮬레이션에 결합하여, 코덱 설정에 따른 프레임 크기 분포를 현실적으로 재현한다.
2. 네트워크 지표(VF-RTT, CU, FLR)와 코덱 지표(VMAF)를 하나의 프레임워크에서 통합 분석한다.
3. IR vs GoP, 비트레이트, 사용자 수, 거리라는 다차원 요인의 상호작용을 정량적으로 제시한다.
4. "높은 비트레이트 IR 우선", "4명 동시 사용자 한계" 같은 실무적으로 활용 가능한 권고를 도출한다.

### 2. 한계 및 의문점

1. MLO(Multi-Link Operation), Multi-AP coordination, OFDMA 등 Wi-Fi 7의 핵심 고급 기능이 아직 포함되지 않았다.
2. Bitrate Manager(ABR) 블록은 향후 과제로 남겨두고 CBR을 가정하므로, 실제 적응형 스트리밍 동작은 평가되지 않았다.
3. 결과는 특정 영상 샘플(*BigBuckBunny*, *snow*) 및 시뮬레이션 모델에 기반하므로, 다양한 실제 콘텐츠와 실제 무선 환경으로의 일반화는 추가 검증이 필요하다.
4. 인접 네트워크 간섭(OBSS)은 서론에서 문제로 언급되었으나 본 실험의 핵심 변수로는 다루어지지 않는다.


## 용어 정리

| 용어 | 의미 |
|---|---|
| ALVR (Air Light VR) | SteamVR 서버와 HMD 사이의 무선 브리지 역할을 하는 MIT 라이선스 VR 스트리밍 앱 |
| HEVC | H.265 고효율 영상 코딩 표준 |
| GoP (Group of Pictures) | I-frame과 P-frame으로 구성된 인코딩 프레임 그룹 단위 |
| IR (Intra-refresh) | I-frame 코딩 단위를 여러 프레임에 걸쳐 점진 주입하는 모드로, 프레임 크기 변동을 줄임 |
| VF-RTT | Video Frame Round-Trip Time, 애플리케이션 체감 네트워크 지연 지표 |
| FLR (Frame Loss Ratio) | 완전히 수신되지 못한 VF의 비율 |
| CU (Channel Utilization) | 전송·충돌에 소요된 시간 대비 전체 시간의 비율 |
| VMAF | Netflix의 perceptual quality 지표 (0~100) |
| MTP 지연 | Motion-to-Photon, 움직임과 화면 갱신 사이 지연 |
| Wi-Fi 성능 이상 | 낮은 MCS 사용자가 airtime을 독점하여 전체 처리량을 저하시키는 현상 |
| MCS | Modulation and Coding Scheme, 수신 전력에 따라 결정되는 전송률 |
| A-MPDU | Aggregate MAC Protocol Data Unit, 다수 패킷을 집성하는 프레임 |
