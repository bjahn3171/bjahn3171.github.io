---
title: "[논문리뷰] END-TO-END OPTIMIZED IMAGE COMPRESSION"
summary: "End-to-End Optimized Image Compression 논문 리뷰 (ICLR 2017)"
excerpt: "End-to-End Optimized Image Compression 논문 리뷰 (ICLR 2017)"
date: 2026-07-04
last_modified_at: 2026-07-04

categories:
  - 논문리뷰

tags:
  - Video Coding
  - Image Compression
  - DeepLearning
  - ICLR

layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false

paper:
  title: "END-TO-END OPTIMIZED IMAGE COMPRESSION"
  venue: "ICLR"
  year: "2017"
  date: "24 Feb 2017"
  authors: "Johannes Ballé, Valero Laparra, Eero P. Simoncelli"
  affiliations: "Google | New York University"
  links:
    - name: "Paper"
      url: "https://arxiv.org/abs/1611.01704"
    - name: "Github"
      url: ""
    - name: "Project"
      url: ""
---

{% include paper-info.html %}

## 0. 한 줄 요약

<div class="paper-summary-box" markdown="1">

**TL;DR.**  
이 논문은 neural image compression을 end-to-end로 최적화하여 기존 hand-crafted image codec과 경쟁하는 학습 기반 압축 방법을 제안한다.

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

이 논문은 CNN 기반의 비선형 변환과 GDN 비선형성을 사용해 이미지 압축 모델을 end-to-end로 학습하는 방법을 제안한다. 
양자화 때문에 직접 학습이 어려운 문제는 연속적인 근사 손실 함수로 해결하고, rate–distortion 기준으로 전체 모델을 최적화한다. 
실험 결과, 제안 방법은 JPEG 및 JPEG 2000보다 우수한 압축 성능을 보였으며, 특히 낮은 비트레이트에서도 시각적 품질이 크게 향상되었다.

---

## 2. 문제의식

기존 이미지 압축 방식은 transform, quantization, entropy coding 등을 사람이 설계한 규칙에 의존한다. 이 논문은 전체 압축 과정을 rate-distortion 관점에서 직접 최적화하려는 문제의식에서 출발한다.
