# Marketing Decision SERP Skill

行銷決策用的 SERP 前 30 結果構成分析 skill。

它不是一般 SEO 排名報表，而是把搜尋結果拆成「SERP 版位」與「結果類型」，再轉成行銷決策，例如 SEO、Google Ads、通路、媒體、部落客、影片與品牌信任度工作。

## 主要用途

- 分析指定關鍵字的 SERP 前 30。
- 檢查品牌 domain 是否出現。
- 區分自有、競品、媒體、部落客、第三方、影片、電商通路。
- 產出 Google Sheets-ready 表格。
- 根據搜尋結果構成給出行銷策略優先順序。

## 安裝

將本 repo 放到 Codex skill 目錄，例如：

```text
~/.codex/skills/marketing-decision-serp/
```

或放到專案層：

```text
<project>/.codex/skills/marketing-decision-serp/
```

目錄內需要包含 `SKILL.md`。

## 使用方式

在 Codex 中要求：

```text
使用 marketing-decision-serp 分析「牛樟芝」台灣前 30 SERP，品牌 domain 是 bcl.com.tw，blog.bcl.com.tw 也算自有，輸出 Google Sheets 版。
```

Skill 會要求先確認品牌 domain，再開始分析。
