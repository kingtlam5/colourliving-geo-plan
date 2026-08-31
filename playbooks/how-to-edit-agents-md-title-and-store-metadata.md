# 已上線的 agents.md：改標題同 Store metadata

Live 三條 URL 已用你份 `templates/agents.md.liquid`。而家開頭係 `# COLOURLIVING`，Read-only 底下得一行 sitemap。下面兩舊 **可選、對 GEO 幾乎零影響**；想同 Shopify 預設發現句對齊就改。

**只改已經存在的 `agents.md.liquid`。** 唔好再開 `llms.txt.liquid`。改一份，`/agents.md`、`/llms.txt`、`/llms-full.txt` 一齊變。

---

## 1. 標題加 `Agent Instructions —`

Edit code → **Templates** → `agents.md.liquid` → 檔案 **第一行**。

而家：

```markdown
# COLOURLIVING
```

（若你用咗 Liquid，可能已經係 `# {{ agents.store_name }}`。）

改成：

```liquid
# Agent Instructions — {{ agents.store_name }}
```

`store_name` 會出 COLOURLIVING。Save。

無痕開 https://colourliving.shop/agents.md ，第一行應係：

`# Agent Instructions — COLOURLIVING`

---

## 2. 加 Store metadata（canonical `/agents.md`）

同一檔，搵 **Read-only browsing** 最尾嗰行 sitemap。而家大概係：

```markdown
- Search: `GET /search?q={query}&type=product`
- Sitemap: https://colourliving.shop/sitemap.xml

## Policies
```

**刪**「Sitemap: https://…」嗰一粒 bullet，改成：

```liquid
- Search: `GET /search?q={query}&type=product`

### Store metadata

- Sitemap: `GET /sitemap.xml` ({{ agents.sitemap_url }})
- Canonical agent document: `/agents.md`. `/llms.txt` and `/llms-full.txt` mirror this file.

## Policies
```

Save。三條 URL 都會見到 `### Store metadata`。Agent 跟路徑 `/agents.md`，唔靠呢句先識讀站；加咗只係講清楚邊份係正本。

**UCP 排喺品牌後面唔使搬。** Discovery／MCP 已喺檔案下半。唔好為對齊 Shopify 預設把 Commerce Protocol 剪去第二節。

---

## 核對

無痕（唔帶 `preview_theme_id`）：

- https://colourliving.shop/agents.md
- https://colourliving.shop/llms.txt

`Ctrl+F`：`Agent Instructions`、`Canonical agent document`、`333 Lockhart`、`/.well-known/ucp` 都要有。

完整最新稿（可整份覆蓋）：[agents-md-liquid.md](agents-md-liquid.md)。
