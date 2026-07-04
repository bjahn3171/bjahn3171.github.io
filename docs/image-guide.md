# Image Guide

This document describes how to add paper figures.

## Image Location

Store paper figures under:

```text
assets/images/paper_review/
```

Recommended structure:

```text
assets/images/paper_review/
└── paper-slug/
    ├── front.png
    ├── overview.webp
    └── pipeline.webp
```

Example:

```text
assets/images/paper_review/mc-emvs/front.png
```

## Insert Image

Use this in a post:

```html
<figure class="paper-figure paper-figure--wide">
  <img src="{{ '/assets/images/paper_review/mc-emvs/front.png' | relative_url }}" alt="MC-EMVS overview">
</figure>
```

## Insert Image with Caption

```html
<figure class="paper-figure paper-figure--wide">
  <img src="{{ '/assets/images/paper_review/mc-emvs/front.png' | relative_url }}" alt="MC-EMVS overview">
  <figcaption>Figure 1. Overview of MC-EMVS.</figcaption>
</figure>
```

## Figure Size Classes

Available classes:

```html
paper-figure--wide
paper-figure--medium
paper-figure--small
```

Example:

```html
<figure class="paper-figure paper-figure--medium">
  <img src="{{ '/assets/images/paper_review/paper-slug/overview.webp' | relative_url }}" alt="Overview">
</figure>
```

## Recommended Format

Use WebP for blog images.

Recommended size:

```text
width: 1200px ~ 1600px
quality: 80 ~ 90
```

## PDF Figure Extraction Workflow

For high-quality figures, do not use low-resolution screenshots.

Use `pdftoppm` to render a PDF page as a high-resolution PNG.

Example:

```bash
pdftoppm -png -r 400 -f 3 -l 3 paper.pdf page
```

For a single-page poster PDF:

```bash
pdftoppm -png -r 400 -singlefile paper.pdf poster
```

This generates:

```text
poster.png
```

Then crop the figure area manually.

## Convert PNG to WebP

Use ImageMagick:

```bash
magick cropped.png -resize 1400x -quality 90 overview.webp
```

If the file is still too large:

```bash
magick cropped.png -resize 1200x -quality 80 overview.webp
```

## Recommended Upload

Upload only the final compressed image:

```text
assets/images/paper_review/paper-slug/overview.webp
```

Do not upload huge intermediate PNG files.
