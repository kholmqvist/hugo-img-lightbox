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

## 🚀 Installation (Hugo Modules)

> You must have [Go](https://go.dev/doc/install) installed and available in your terminal.

### 1. Initialize Hugo Modules in your project (if not already)

```bash
hugo mod init github.com/your/project
```

### 2. Add this to your site's `config.toml`:

```toml
[module]
[[module.imports]]
path = "github.com/kholmqivst/hugo-img-lightbox"
```

### 3. Pull the module:

```bash
hugo mod get github.com/kholmqivst/hugo-img-lightbox
```

### 4. Add the Lightbox partial in your layout (`baseof.html` or similar):

```go-html
{{ if .Scratch.Get "usesLightbox" }}
  {{ partial "lightbox.html" . }}
{{ end }}
```

### 5. Use the shortcode in your content files:

```markdown
{{< img src="image.png" alt="Alt text" caption="Alt text" >}}
```

✅ Images must be inside the same page bundle as `index.md` (i.e., next to your content file).

---
