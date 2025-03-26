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

## 📄 layouts/shortcodes/img.html

```go-html
{{ $matches := .Page.Resources.Match (printf "*%s" (.Get "src")) }}
{{ $src := index $matches 0 }}

{{ if not $src }}
  <p style="color:red;">⚠️ Could not find image '{{ .Get "src" }}'</p>
{{ else }}
  {{ .Page.Scratch.Set "usesLightbox" true }}
  {{ $caption := .Get "caption" }}
  {{ $alt := .Get "alt" | default "" }}
  {{ $tiny := $src.Resize "500x" }}
  {{ $small := $src.Resize "800x" }}
  {{ $medium := $src.Resize "1200x" }}

  <figure>
    <a href="{{ $src.RelPermalink }}" data-lightbox="gallery" {{ with $caption }}data-title="{{ . }}"{{ end }}>
      <img
        sizes="(min-width: 35em) 720px, 100vw"
        srcset='{{ $tiny.RelPermalink }} 500w, {{ $small.RelPermalink }} 800w, {{ $medium.RelPermalink }} 1200w'
        src="{{ $medium.RelPermalink }}"
        loading="lazy"
        alt="{{ $alt }}">
    </a>
    {{ with $caption }}<figcaption>{{ . }}</figcaption>{{ end }}
  </figure>
{{ end }}
```

---

## 📄 layouts/partials/lightbox.html

```html
<link href="https://cdn.jsdelivr.net/npm/lightbox2@2/dist/css/lightbox.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/lightbox2@2/dist/js/lightbox.min.js"></script>
```

---

## 📦 go.mod

```go
module github.com/kholmqvist/hugo-img-lightbox

go 1.18
```

---

## ✅ TODO / Improvements

- Add support for fallback to `/static/images/`
- Add param for `gallery` grouping
- Add dark/light toggle for Lightbox
- Support global captions from front matter

---

PRs welcome! 💜

