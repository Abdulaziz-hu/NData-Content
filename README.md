# NData-Content

Public content repository for the [N(DATA)](https://github.com/Abdulaziz-hu/NData) website.

This repo stores all Markdown content (blog posts, news articles, update notes) and the product data JSON. The main NData site fetches everything live from here via the GitHub raw API.

---

## Repository Structure

```
root/
├── content/
│   ├── blog/
│   │   ├── en/
│   │   │   └── yyyy/mm/dd/slug.md
│   │   └── ar/
│   │       └── yyyy/mm/dd/slug.md
│   ├── news/
│   │   ├── en/
│   │   │   └── yyyy/mm/dd/slug.md
│   │   └── ar/
│   │       └── yyyy/mm/dd/slug.md
│   └── updates/
│       ├── en/
│       │   └── yyyy/mm/dd/slug.md
│       └── ar/
│           └── yyyy/mm/dd/slug.md
└── data/
    └── data.json
```

---

## Writing a Post

Create a `.md` file in the correct language and section folder using the date path.

**Example:** `content/blog/en/2026/06/01/my-new-post.md`

### Frontmatter

Every file must start with a YAML frontmatter block:

```markdown
---
title: My Post Title
date: 2026-06-01
author: Your Name
category: blog          # blog | news | update
slug: my-new-post
lang: en                # en | ar
tags: tag1, tag2
version: 1.12.0         # optional, for update posts
---

Your content here...
```

### Supported Markdown

- Headings: `#`, `##`, `###`, etc.
- **Bold**, *italic*, ***bold italic***
- `inline code` and fenced code blocks (` ``` `)
- Unordered lists (`-`) and ordered lists (`1.`)
- Blockquotes (`>`)
- Links `[text](url)`
- Horizontal rules (`---`)

---

## Product Data (`data/data.json`)

The `data.json` file is fetched directly by the N(DATA) web interface and API explorer. It is a flat JSON array of product objects.

### Product Schema

```json
{
  "id": "phn-000001",
  "name": "Product Name",
  "brand": "Brand",
  "category": "smartphones",
  "description": "Short description.",
  "price": 999,
  "date_added": "2026-01-01",
  "images": ["https://..."],
  "specs": {
    "display": "6.1-inch OLED",
    "processor": "Snapdragon 8 Gen 3",
    "ram": "8GB",
    "storage": "256GB"
  },
  "diy": [
    {
      "type": "guide",
      "title": "Screen Replacement",
      "url": "https://ifixit.com/..."
    }
  ]
}
```

### Categories

| Value | Label |
|---|---|
| `smartphones` | Phones |
| `laptops` | Laptops |
| `wearables` | Audio/Wear |
| `components` | Components |
| `tablets` | Tablets |
| `cameras` | Cameras |
| `gaming` | Gaming |
| `monitors` | Monitors |
| `networking` | Networking |

---

## How Content is Fetched

The N(DATA) site fetches content at runtime using the GitHub Contents API:

```
GET https://api.github.com/repos/Abdulaziz-hu/NData-Content/contents/content/{section}/{lang}
```

It then fetches each `.md` file raw:

```
GET https://raw.githubusercontent.com/Abdulaziz-hu/NData-Content/main/content/{section}/{lang}/{yyyy}/{mm}/{dd}/{slug}.md
```

No build step required. Push a new `.md` file and it appears on the site within seconds.

---

## Contributing

1. Fork this repo
2. Add or edit content files following the structure above
3. Open a pull request

For bugs or suggestions related to the main website, see the [NData repo](https://github.com/Abdulaziz-hu/NData).

---

## License

MIT — see [LICENSE](https://github.com/Abdulaziz-hu/NData/blob/main/LICENSE) in the main NData repository.
