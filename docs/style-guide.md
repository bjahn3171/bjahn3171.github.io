# Style Guide

This document describes where to edit styles.

## Custom Style Location

Custom styles are stored under:

```text
_sass/custom/
```

Main files:

```text
_sass/custom/_variables.scss
_sass/custom/_base.scss
_sass/custom/_sidebar.scss
_sass/custom/_paper-post.scss
_sass/custom/_post-list.scss
_sass/custom/_filter.scss
```

The main stylesheet entry is:

```text
assets/css/main.scss
```

## Color Variables

Edit:

```text
_sass/custom/_variables.scss
```

Main variables:

```scss
--bj-accent: #2f7f8f;
--bj-accent-dark: #1f5f6c;
--bj-text: #4f565c;
--bj-muted: #70777d;
--bj-light-muted: #9aa1a8;
--bj-border: #e7eaee;
--bj-bg-soft: #f7f9fa;
```

Usage:

| Variable | Role |
|---|---|
| `--bj-accent` | Main accent color |
| `--bj-accent-dark` | Hover color |
| `--bj-text` | Main body text |
| `--bj-muted` | Muted text |
| `--bj-light-muted` | Count or secondary text |
| `--bj-border` | Border color |
| `--bj-bg-soft` | Soft background color |

## Body Font Size

Edit:

```text
_sass/custom/_base.scss
```

```scss
.page__content {
  font-size: 0.76rem;
  line-height: 1.6;
}
```

## Post Title Font Size

Edit:

```text
_sass/custom/_base.scss
```

```scss
.page__title {
  font-size: 1.25rem;
  line-height: 1.35;
}
```

## Heading Font Size

Edit:

```text
_sass/custom/_base.scss
```

```scss
.layout--single .page__content h2 {
  font-size: 1.2rem;
}

.layout--single .page__content h3 {
  font-size: 0.98rem;
}

.layout--single .page__content h4 {
  font-size: 0.9rem;
}
```

Markdown heading mapping:

```text
##  -> h2
### -> h3
#### -> h4
```

## Post List Style

Edit:

```text
_sass/custom/_post-list.scss
```

Important selectors:

```scss
.paper-list-title
.paper-list-date
.paper-list-summary
.paper-list-tags
.paper-list-tag
```

Example:

```scss
.paper-list-title {
  font-size: 1.25rem;
}

.paper-list-summary {
  font-size: 0.82rem;
  margin: 0.25rem 0 0.35rem 0;
}

.paper-list-tag {
  padding: 0.25rem 0.58rem;
  font-size: 0.65rem;
}
```

## Tag Row Spacing

Edit:

```text
_sass/custom/_post-list.scss
```

```scss
.paper-list-tags {
  gap: 0.42rem;
}
```

`gap` controls the spacing between the tag label and tag pills.

## Sidebar Style

Edit:

```text
_sass/custom/_sidebar.scss
```

Important selectors:

```scss
.author__name
.author__bio
.author__urls-wrapper
.paper-sidebar
.paper-sidebar__item
.paper-sidebar__children
```

## Layout Width

Edit:

```text
_sass/custom/_base.scss
```

```scss
@media (min-width: 1024px) {
  .masthead__inner-wrap,
  #main {
    max-width: 1560px !important;
  }

  .layout--single .page {
    padding-right: 200px !important;
  }

  .layout--single .sidebar__right {
    width: 200px !important;
    margin-right: -200px !important;
  }
}
