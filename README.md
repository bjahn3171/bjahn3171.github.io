# bjahn3171.github.io

A personal GitHub Pages blog for paper reviews and research notes.

This site is built with Jekyll and the Minimal Mistakes theme.  
It is customized to organize paper review posts by research categories and tags.

## Site

- URL: https://bjahn3171.github.io
- Main purpose: Paper review archive
- Theme: Minimal Mistakes Jekyll theme

## Features

- Paper review posts
- Sidebar categories by research topic
- Tag-based post filtering
- Recent-first post archive
- Paper metadata box
- Table of contents for individual posts
- MathJax support for equations
- Custom figure layout for paper images

## Main Structure

```text
_posts/Paper Review/         # Paper review posts
_pages/                      # Archive and category pages
_includes/                   # Reusable HTML components
_sass/custom/                # Custom style modules
assets/images/paper_review/  # Paper figures
assets/css/main.scss         # Main stylesheet entry
```

## Important Files

| File | Role |
|---|---|
| `_config.yml` | Site and theme configuration |
| `_includes/paper-info.html` | Paper metadata box |
| `_includes/filterable-post-list.html` | Post list and tag filtering |
| `_includes/sidebar-custom.html` | Sidebar category menu |
| `_includes/page__taxonomy.html` | Post page tag display |
| `_sass/custom/_variables.scss` | Color variables |
| `_sass/custom/_base.scss` | Global font, layout, heading styles |
| `_sass/custom/_paper-post.scss` | Paper post components |
| `_sass/custom/_post-list.scss` | Archive/list page styles |
| `_sass/custom/_filter.scss` | Search and tag filter UI |

## Quick Usage

### Add a paper review

Create a new post under:

```text
_posts/Paper Review/YYYY-MM-DD-paper-title.md
```

Use this category:

```yaml
categories:
  - 논문리뷰
```

### Add a paper metadata box

In the post body:

```liquid
{% include paper-info.html %}
```

### Add an image

Store images under:

```text
assets/images/paper_review/paper-slug/
```

Insert image:

```html
<figure class="paper-figure paper-figure--wide">
  <img src="{{ '/assets/images/paper_review/paper-slug/overview.webp' | relative_url }}" alt="Overview">
</figure>
```

### Use LaTeX equations

Enable MathJax in the post front matter:

```yaml
mathjax: true
```

Inline equation:

```markdown
$\mathbf{x}_k = (x_k, y_k)^\top$
```

Display equation:

```markdown
$$
e_k = (\mathbf{x}_k, t_k, p_k)
$$
```

## Detailed Guides

- [Writing Guide](docs/writing-guide.md)
- [Style Guide](docs/style-guide.md)
- [Image Guide](docs/image-guide.md)
- [MathJax Guide](docs/mathjax-guide.md)

## License

This website is based on the Minimal Mistakes Jekyll theme.

Minimal Mistakes is licensed under the MIT License.

Original theme:

- Minimal Mistakes by Michael Rose and contributors
- https://github.com/mmistakes/minimal-mistakes

Custom paper-review structure and site modifications:

- Copyright (c) 2026 Byungjun Ahn
