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

> 여기에 abstract 원문 또는 필요한 부분을 넣는다.

</details>

### 1.2 한국어 요약

이 논문은 nonlinear analysis transform, quantization, nonlinear synthesis transform으로 구성된 학습 기반 이미지 압축 구조를 제안한다.

---

## 2. 문제의식

기존 이미지 압축 방식은 transform, quantization, entropy coding 등을 사람이 설계한 규칙에 의존한다. 이 논문은 전체 압축 과정을 rate-distortion 관점에서 직접 최적화하려는 문제의식에서 출발한다.
