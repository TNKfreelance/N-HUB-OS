# 20. Research Engine

## 収集対象カテゴリ

構想書に基づき、以下を収集対象カテゴリとする(優先順位は [02_principles.md](02_principles.md) のソース優先順位とは別軸):

- Claude Code / MCP Servers / AI Agent
- Browser Automation(Playwright, Puppeteer, Browser Use)
- AI Workflow(n8n, LangGraph, CrewAI, AutoGen)
- AI Video Generation / AI Coding / AI SaaS
- Immersive Web(Three.js, WebGPU, React Three Fiber, Shaders)
- GitHub Trending / Awesome Lists / Claude Skills

## 除外対象

[02_principles.md](02_principles.md) の「除外対象」をそのまま適用する(未確定情報・再現性のない誇大広告・無断転載・個人情報を含むもの)。

## 重複排除

- 収集前に `brain/research/` 内の既存ファイルを URL・タイトルで検索し、同一ソースの再収集を避ける。
- 類似タイトル・同一 URL のエントリは新規ファイルを作らず、既存ファイルの `updates` セクションに追記する。

## 保存形式

`brain/research/<YYYY-MM-DD>_<source>_<slug>.md`

```markdown
---
source: github|reddit|hackernews|x|youtube|producthunt|medium|devto|official
source_url: <元URL>
collected_date: <YYYY-MM-DD>
category: <01_vision.md の対象領域から1つ以上>
status: unverified
---

# <タイトル>

## 要約

## 元情報からの引用・根拠

## 再現性メモ(実際に試した場合のみ)
```

## 更新方法

新しい情報が既存エントリを更新・否定する場合は、元ファイルを上書きせず `## Updates` セクションに日付付きで追記する(履歴を失わない)。

## API 連携

利用可能な場合は `WebSearch` / `WebFetch` および GitHub API 等の既存ツールを使う。専用のクローラー・常駐スクレイパーは現時点では実装しない(過剰実装回避、[00_constitution.md](00_constitution.md) 原則3)。必要になった時点で個別タスクとして N-Link canonical pipeline でゲートしながら追加する。
