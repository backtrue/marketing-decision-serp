---
name: marketing-decision-serp
description: 行銷決策用的 SERP 前 30 結果構成分析流程。Use when the user asks to analyze keyword search results, SERP composition, competitor/content/channel result types, brand domain presence, or decide SEO, Google Ads, media, blogger, video, ecommerce-channel, or content actions from search results. Always collect brand domain rules before analysis and output a Google Sheets-ready decision table.
---

# Marketing Decision SERP

Use this skill to turn a keyword's top SERP results into a marketing decision table, not a generic SEO report.

## Non-Negotiable Intake

Before running any SERP analysis, ask for and confirm:

1. Target keyword(s).
2. Market and language, defaulting to Taiwan / Traditional Chinese only when the user has already implied Taiwan.
3. Brand domain(s), including whether subdomains count as owned.
4. Competitor domains, if known. If not provided, classify competitor-owned sites by evidence from the SERP and mark uncertain cases as `需人工確認`.

Do not start classification before brand domain rules are known.

Owned-domain rules:

- A listed brand root domain and its listed subdomains are `自有`.
- Subdomains only count as owned when included by the user's rule.
- Ecommerce marketplace pages, retailer pages, shopping-search pages, and brand stores on channels are not `自有`; classify them as `電商通路`.
- Social/video profiles are not `自有` unless the user explicitly says to treat specific official accounts as owned media.

## Required Data Sources

Use live data sources only. Prefer:

1. Ubersuggest MCP `serp_analysis` for top SERP results.
2. Ubersuggest MCP keyword/domain tools for supporting metrics when needed.
3. Public search or another SERP provider only as a cross-check or fallback, and state the source clearly.

Every conclusion must cite the source name and URL when possible. For MCP-only results, cite the MCP provider page and state the tool used.

## Two-Layer Classification

Always separate these two columns:

- `SERP 版位`: what the search page slot is.
- `結果類型`: what the result represents for marketing decisions.

### SERP 版位

Use the provider's SERP type when available:

- `organic`
- `knowledge_graph`
- `people_also_ask`
- `video`
- `short_videos`
- `images`
- `related_searches`
- `local_pack`
- `paid`
- `other`

### 結果類型

Use this fixed list:

- `自有`
- `競品官網首頁`
- `競品官網分類頁`
- `競品官網商品頁`
- `競品官網內容`
- `部落客內容`
- `媒體內容`
- `第三方內容`
- `新聞`
- `影片`
- `電商通路`
- `需人工確認`

## Classification Rules

Classify from URL, domain, title, snippet, and page context. Open pages when the SERP title/URL is insufficient.

Use `自有` when:

- The result domain matches the confirmed brand domain rule.

Use competitor official-site classes when:

- The domain appears to be a brand/product official site, not a marketplace, media site, blog network, association, encyclopedia, or social platform.
- Homepage: root/homepage URL, brand homepage title, or minimal path.
- Category page: collection, category, product-listing, sale-page-category, brand product family, or page listing multiple products.
- Product page: URL/title targets one product SKU, package, item, or purchasable product detail.
- Content: blog/article/guide/FAQ/knowledge/report/resource content hosted on a competitor official domain.

Use `電商通路` when:

- The result is on a marketplace, retailer, shopping channel, search results page, marketplace product page, or channel brand store.
- Examples include momo, PChome, ETMall, Shopee, Rakuten, Yahoo Shopping, Amazon, or similar retailers.

Use `媒體內容` when:

- The domain is an editorial publication, news/media brand, magazine, or professional editorial content site.
- If the page is a news article, use `新聞` instead.

Use `部落客內容` when:

- The site is an individual blog, creator site, review blog, affiliate blog, personal site, or non-editorial content creator site.

Use `第三方內容` when:

- The site is informational but not media, blogger, ecommerce, video, competitor, or owned.
- Examples: Wikipedia, encyclopedia, association, institute, government, academic, public database, Q&A, general reference.

Use `影片` when:

- The SERP result itself is a video, short video, YouTube page, Facebook video, TikTok, Instagram Reel, or video feature.

Use `需人工確認` when:

- Domain ownership is unclear.
- The site could be either competitor or third party.
- The URL/title/snippet cannot support a confident classification.
- A page fails to load or blocks inspection.

Never force a classification without evidence.

## Decision Rules

After classifying, convert the SERP composition into marketing decisions.

Use these rules:

| 場景狀況 | 目標策略 |
|---|---|
| 完全沒有自有結果 | 先看自然結果占比什麼結果多，作為優先順序 |
| 有自有結果 | 安排預算增加流量、提高排名，並加強 SEO 工作 |
| 通路多 | 優先安排通路上架、通路商品頁優化、通路廣告資源採買 |
| 部落客內容多 | 盡快合作部落客，以搜尋結果中的內容型態為優先 |
| 媒體內容多 | 盡快合作媒體，以搜尋結果中的內容型態為優先 |
| 部落客內容多或媒體內容多 | 安排 Google Ads 指定版位廣告投放 |
| 有影片 | 規劃 YouTube / Shorts / creator video budget |
| 有影片 | 安排 Google Ads 指定版位廣告投放 |
| 競品官網內容多 | 品牌信任度提升計劃 |
| 競品官網內容多 | 利用 Google Ads 自訂區隔方式投遞競品瀏覽客戶 |

If multiple scenes apply, order recommendations by:

1. Whether owned assets are absent or weak.
2. Which result type dominates top 10.
3. Which result type dominates top 30.
4. Which actions can capture existing SERP demand fastest.
5. Which actions build durable owned visibility.

## Google Sheets Output

Output a Google Sheets-ready table. Prefer TSV in a fenced `tsv` block when the user will paste into Sheets. If Google Sheets tooling is available and the user asks to create or update a Sheet, create/update the Sheet directly.

Required columns:

- `查詢日期`
- `關鍵字`
- `市場`
- `語言`
- `排名`
- `SERP 版位`
- `結果類型`
- `是否自有`
- `是否疑似競品`
- `網域`
- `URL`
- `標題`
- `判斷依據`
- `建議行動`
- `優先級`
- `需人工確認`
- `資料來源`

Also output three summary tables:

1. `前10類型占比`
2. `前30類型占比`
3. `行銷決策摘要`

`行銷決策摘要` columns:

- `場景狀況`
- `觀察證據`
- `目標策略`
- `優先級`
- `執行備註`

## Acceptance Criteria

The work is complete only when:

- Brand domain rules were confirmed before analysis.
- Top 30 SERP results were collected from a named live source.
- `SERP 版位` and `結果類型` are separate.
- Every owned-domain result is checked against the user's domain rules.
- Ecommerce channel pages are not counted as owned unless the user explicitly overrides the rule.
- Uncertain classifications are marked `需人工確認`, not guessed.
- Top 10 and top 30 composition summaries are included.
- The final output includes a marketing decision summary, not just a ranking table.
- The output is Google Sheets-ready.
- Sources and source limitations are stated.
