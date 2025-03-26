# hugo-img-lightbox

A plug-and-play Hugo module for responsive images, captions, and Lightbox2 support via shortcode.

---

## 📦 Features

- `{{< img >}}` shortcode with responsive sizes (500w, 800w, 1200w)
- Lazy loading `<img>`
- Optional `<figure>` + `<figcaption>` from `caption` param
- Automatic Lightbox2 support
- Lightbox assets only load when shortcode is used

---

## 📁 Directory Structure

```
hugo-img-lightbox/
├── layouts/
│   ├── shortcodes/
│   │   └── img.html
│   └── partials/
│       └── lightbox.html
├── README.md
└── go.mod
```

---

## 🚀 Installation

1. Add this to your site's `config.toml`:

```toml
[module]
[[module.imports]]
path = "github.com/kholmqvist/hugo-img-lightbox"
```

2. In your site's layout (`baseof.html` or similar), add:

```go-html
{{ if .Scratch.Get "usesLightbox" }}
  {{ partial "lightbox.html" . }}
{{ end }}
```

3. In your content files:

```markdown
{{< img src="image.png" alt="Alt text" caption="Alt text" >}}
```

---
