# MathJax Guide

This document describes how to write LaTeX-style equations in posts.

## Enable MathJax

Add this to the post front matter:

```yaml
mathjax: true
```

Example:

```yaml
---
title: "[논문리뷰] Example Paper"
layout: single
author_profile: true
toc: true
toc_sticky: true
mathjax: true
---
```

## Inline Equation

Use `$...$`.

```markdown
$\mathbf{x}_k = (x_k, y_k)^\top$
```

Example:

```markdown
여기서 $\mathbf{x}_k = (x_k, y_k)^\top$는 이벤트가 발생한 픽셀 위치를 의미한다.
```

## Display Equation

Use `$$...$$`.

```markdown
$$
e_k = (\mathbf{x}_k, t_k, p_k)
$$
```

Example:

```markdown
하나의 이벤트는 다음과 같이 표현된다.

$$
e_k = (\mathbf{x}_k, t_k, p_k)
$$
```

## Common Syntax

```markdown
$\theta$

$\Delta t_k$

$p_k \in \{+1, -1\}$

$$
L(\mathbf{x}_k, t_k) - L(\mathbf{x}_k, t_k - \Delta t_k) = p_k \theta
$$
```

## Aligned Equations

```markdown
$$
\begin{aligned}
y &= g_a(x) \\
\hat{y} &= Q(y) \\
\hat{x} &= g_s(\hat{y})
\end{aligned}
$$
```

## Troubleshooting

If equations do not render:

1. Check that the post has `mathjax: true`.
2. Check that `_includes/head/custom.html` contains the MathJax script.
3. Wait for GitHub Pages rebuild.
4. Refresh the page with `Ctrl + F5`.
5. Use `$...$` for inline equations and `$$...$$` for display equations.
