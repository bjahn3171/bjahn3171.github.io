{% include paper-info.html %}

## 0. 한 줄 요약

<div class="paper-summary-box" markdown="1">

**TL;DR.**  
이 논문은 CNN 기반 비선형 변환, 양자화, 복원 변환을 하나의 rate–distortion 목적함수로 end-to-end 최적화하여 기존 JPEG/JPEG 2000보다 우수한 압축 성능을 얻는 학습 기반 이미지 압축 방법을 제안한다.

</div>

---

## 1. Abstract / 요약

### 1.1 Original Abstract

<details markdown="1">
<summary><strong>Original Abstract 보기</strong></summary>

> We describe an image compression method, consisting of a nonlinear analysis
transformation, a uniform quantizer, and a nonlinear synthesis transformation.
The transforms are constructed in three successive stages of convolutional linear
filters and nonlinear activation functions. Unlike most convolutional neural networks,
the joint nonlinearity is chosen to implement a form of local gain control,
inspired by those used to model biological neurons. Using a variant of stochastic
gradient descent, we jointly optimize the entire model for rate–distortion performance
over a database of training images, introducing a continuous proxy for the
discontinuous loss function arising from the quantizer. Under certain conditions,
the relaxed loss function may be interpreted as the log likelihood of a generative
model, as implemented by a variational autoencoder. Unlike these models,
however, the compression model must operate at any given point along the rate–
distortion curve, as specified by a trade-off parameter. Across an independent
set of test images, we find that the optimized method generally exhibits better
rate–distortion performance than the standard JPEG and JPEG 2000 compression
methods. More importantly, we observe a dramatic improvement in visual quality
for all images at all bit rates, which is supported by objective quality estimates
using MS-SSIM.

</details>

### 1.2 한국어 요약

이 논문은 CNN 기반의 비선형 분석 변환, 균일 양자화, 비선형 합성 변환으로 구성된 학습 기반 이미지 압축 모델을 제안한다.  
양자화는 미분 불가능하기 때문에 직접적인 gradient 기반 학습이 어렵지만, 논문에서는 이를 연속적인 근사 손실 함수로 대체하여 전체 압축 모델을 rate–distortion 기준으로 end-to-end 최적화한다.

또한 일반적인 CNN 활성화 함수 대신, 생물학적 시각 모델에서 영감을 받은 local gain control 형태의 GDN 비선형성을 사용한다. 실험 결과, 제안 방법은 JPEG 및 JPEG 2000보다 우수한 rate–distortion 성능을 보였고, 특히 낮은 비트레이트에서 시각적 품질이 크게 개선되었다.

### 1.3 핵심 요약

- **핵심 문제:** 양자화가 포함된 이미지 압축 과정을 어떻게 end-to-end로 학습할 수 있는가?
- **핵심 방법:** 분석 변환, 양자화, 합성 변환을 rate–distortion objective로 공동 최적화한다.
- **핵심 결과:** JPEG, JPEG 2000보다 좋은 압축 성능과 시각적 품질을 보였다.

---

## 2. 서론 / 배경

기존 이미지 압축 방식은 transform, quantization, entropy coding과 같은 구성 요소를 사람이 설계한 규칙에 의존해 왔다. JPEG나 JPEG 2000 역시 각각 DCT, wavelet transform과 같은 hand-crafted 변환을 기반으로 한다.

이 논문은 이러한 전통적인 압축 파이프라인을 학습 가능한 모델로 대체하려는 흐름에 있다. 즉, 이미지를 latent representation으로 변환하고, 이를 양자화한 뒤 다시 복원하는 전체 과정을 하나의 rate–distortion 최적화 문제로 다룬다.

이 논문에서 중요한 점은 단순히 neural network를 압축에 적용했다는 것이 아니라, **양자화로 인해 학습이 어려운 손실 압축 문제를 연속적인 proxy objective로 완화하여 end-to-end 학습 가능하게 만들었다는 점**이다.

---

## 3. 핵심 아이디어

이 논문의 핵심 아이디어는 다음과 같다.

> 이미지 압축을 분석 변환, 양자화, 합성 변환으로 구성된 학습 가능한 비선형 autoencoder 구조로 보고, 전체 모델을 rate–distortion 관점에서 직접 최적화한다.

기존 방식은 대체로 다음과 같다.

```text
Image
→ hand-crafted transform
→ quantization
→ entropy coding
→ reconstruction
