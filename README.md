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
│       └── lightbox-footer.html
│       └── lightbox-head.html
├── static/
│   ├── css/
│   │   └── lightbox.min.css
│   ├── images/
│   │   └── close.png
│   │   └── loading.gif
│   │   └── next.png
│   │   └── prev.png
│   └── js/
│       └── lightbox-plus-jquery.min.js
├── README.md
├── go.mod
└── theme.toml

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

### 4. Add the Lightbox partials in your layout (`baseof.html` or similar):

```go-html
<!-- place this inside your <head></head> tags -->
{{ if .Scratch.Get "usesLightbox" }}
  {{ partial "lightbox-head.html" . }}
{{ end }}

<!-- place this before your closing </body> tag -->
{{ if .Scratch.Get "usesLightbox" }}
  {{ partial "lightbox-footer.html" . }}
{{ end }}
```

### 5. Use the shortcode in your content files:

```markdown
{{< img src="image.png" alt="Alt text" caption="Alt text" >}}
```

✅ Images must be inside the same page bundle as `index.md` (i.e., next to your content file).

### 6. (Optional) Use python to convert all existing markdown images to use the img shortcode

Here’s a clean Python 3 script that will:
	1.	Recursively search all .md files in your content/ folder
	2.	Find all ![alt](src) Markdown image links
	3.	Replace them with your img shortcode

🐍 Python script: convert_markdown_images.py

```python
import re
from pathlib import Path

# Regex pattern: ![alt text](image/path.jpg)
pattern = re.compile(r'!\[([^\]]*?)\]\(([^)]+?)\)')

# Replacement: {{< img src="image.jpg" alt="Alt text" caption="Alt text" >}}
def replace_match(match):
    alt = match.group(1).strip()
    src = match.group(2).strip()
    return f'{{{{< img src="{src}" alt="{alt}" caption="{alt}" >}}}}'

# Path to your Hugo content directory
content_dir = Path("content")

for file in content_dir.rglob("*.md"):
    text = file.read_text(encoding='utf-8')
    new_text = pattern.sub(replace_match, text)

    if text != new_text:
        print(f"Updated: {file}")
        file.write_text(new_text, encoding='utf-8')
```

The script should be placed in your Hugo site folder.

```bash
python3 convert_markdown_images.py
```
