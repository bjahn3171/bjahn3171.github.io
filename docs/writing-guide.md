# Writing Guide

This document describes how to write paper review posts.

## Post Location

Paper review posts are stored under:

```text
_posts/Paper Review/
```

Filename format:

```text
YYYY-MM-DD-paper-title.md
```

Example:

```text
_posts/Paper Review/2026-07-04-end-to-end-image-compression.md
```

## Required Category

Every paper review post should use:

```yaml
categories:
  - 논문리뷰
```

This category is used for sidebar counts and paper review archive pages.

## Recommended Tags

Use tags consistently because they are used for filtering.

Example:

```yaml
tags:
  - Video Coding
  - Image Compression
  - DeepLearning
  - ICLR
```

Recommended topic tags:

```text
Computer Vision
3D Vision
Video Coding
Event Camera
Gaussian Splatting
Image Compression
NLP
Diffusion
LLM
```

Recommended venue tags:

```text
CVPR
ICCV
ECCV
ICLR
ICML
NeurIPS
SIGGRAPH
DCC
PCS
TIP
TCSVT
```

## Common Front Matter

```yaml
---
title: "[논문리뷰] Paper Title"
summary: "Paper Title review (Venue Year)"
excerpt: "Paper Title review (Venue Year)"
date: YYYY-MM-DD
last_modified_at: YYYY-MM-DD

categories:
  - 논문리뷰

tags:
  - Research Topic
  - Conference

layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
mathjax: true

paper:
  title: "Paper Title"
  venue: "ICLR"
  year: "2024"
  date: "Publication Date"
  authors: "Author1, Author2"
  affiliations: "Affiliation1 | Affiliation2"
  links:
    - name: "Paper"
      url: ""
    - name: "Github"
      url: ""
    - name: "Project"
      url: ""
---
```

## Paper Metadata Box

To render the paper metadata box, add this near the top of the post body:

```liquid
{% include paper-info.html %}
```

The metadata itself is written in the front matter:

```yaml
paper:
  title: "Paper Title"
  venue: "ICLR"
  year: "2024"
  date: "Publication Date"
  authors: "Author1, Author2"
  affiliations: "Affiliation1 | Affiliation2"
  links:
    - name: "Paper"
      url: ""
    - name: "Github"
      url: ""
    - name: "Project"
      url: ""
```

## Compact Post Template

```markdown
{% include paper-info.html %}

## 한 줄 요약

<div class="paper-summary-box" markdown="1">

**TL;DR.**  
This paper ...

</div>

---

## Abstract / 요약

### 1. Original Abstract

<details markdown="1">
<summary><strong>Original Abstract 보기</strong></summary>

> Original abstract here.

</details>

### 2. 한국어 요약

Korean summary here.

---

## 서론 / 배경

Background and context.

---

## 핵심 아이디어

Main idea.

---

## Method

Method description.

---

## Experiments / Analysis

Experimental setup and results.

---

## Discussion

Strengths and limitations.

---

## Takeaway

Main takeaway.

---

## 용어 정리

| Term | Meaning |
|---|---|
|  |  |
```
EOF
