---
name: n-hub-research
description: Collects foreign-language (non-Japanese) primary-source information on Claude Code, MCP (Model Context Protocol), AI Agents, Browser Automation (Playwright/Puppeteer/Browser Use), AI Workflow tools (n8n/LangGraph/CrewAI/AutoGen), AI Video Generation, AI Coding tools, AI SaaS, and Immersive Web (Three.js/WebGPU/React Three Fiber), then saves each finding as an unverified research note under N-HUB-OS/brain/research/. Use this whenever the user asks to research, collect, survey, check for updates on, or "keep an eye on" these AI/dev topics, or explicitly says "N-HUB-OS Research" / "N-HUB-OSでリサーチして" / "海外の最新情報を集めて". Do not use for topics outside this list, for general one-off web lookups the user can answer directly, or for verifying/promoting already-collected notes to brain/verified/ (that is the separate Verification skill).
---

# N-HUB-OS Research Skill

## 目的

海外一次情報を収集し、`N-HUB-OS/brain/research/` に未検証の調査ノートとして保存する。判断基準の詳細は N-HUB-OS リポジトリの `docs/20_research_engine.md`(収集仕様)と `docs/02_principles.md`(情報源優先順位・除外基準)にある。このスキルはそれらの要点を実行可能な手順に落とし込んだものであり、矛盾が生じた場合は Specification 側を正とする。

## 収集対象カテゴリ

Claude Code / MCP / AI Agent / Browser Automation / AI Workflow(n8n, LangGraph, CrewAI, AutoGen)/ AI Video Generation / AI Coding / AI SaaS / Immersive Web(Three.js, WebGPU, React Three Fiber)

日本語の情報源は対象外(海外一次情報を優先する方針)。日本語での要約・執筆は収集後の別工程(Writer skill)の仕事なので、このスキルの中ではやらない。

## 情報源の優先順位

1. GitHub
2. Reddit
3. Hacker News
4. X(旧Twitter)
5. YouTube
6. Product Hunt
7. Medium / Dev.to
8. 公式ブログ・公式ドキュメント

上位のソースで確認できる情報を優先して探す。`WebSearch` / `WebFetch` を使う(専用クローラーは作らない — 過剰実装を避けるという N-HUB-OS の方針)。GitHub に関しては GitHub 検索・トレンドページを直接見るのが早い。

## 除外する情報

以下に該当するものは収集・保存しない:

- 公式発表前の噂・未確定情報
- 再現性や裏取りができない誇大広告のみの投稿
- 著作権的にグレーな無断転載・全文コピー
- 個人情報を含むもの

除外理由がはっきりしないグレーな場合は、無理に保存せず一言で理由を添えてスキップしてよい。

## 手順

1. ユーザーの依頼からカテゴリ・キーワードを特定する。
2. 上記の優先順位に従って `WebSearch` / `WebFetch` で情報を探す。
3. 見つけた候補ごとに、まず重複チェックを行う:
   - `N-HUB-OS/brain/research/` 内の既存ファイルを検索し、同一 URL または非常に似たタイトルのエントリがないか確認する。
   - 既存エントリが見つかった場合は新規ファイルを作らず、そのファイルの `## Updates` セクションに日付付きで追記する。
4. 新規の場合は、`N-HUB-OS/templates/research_note.md` のフォーマットに従って `N-HUB-OS/brain/research/<YYYY-MM-DD>_<source>_<slug>.md` を作成する(`source` は github/reddit/hackernews/x/youtube/producthunt/medium/devto/official のいずれか、`slug` は英数字とハイフンの短いタイトル)。
5. 収集結果をユーザーに簡潔に報告する(何件収集したか、どのソースから、保存先のファイル名)。

## 出力フォーマット

`N-HUB-OS/templates/research_note.md` をそのまま使う:

```markdown
---
source: github|reddit|hackernews|x|youtube|producthunt|medium|devto|official
source_url: <元URL>
collected_date: <YYYY-MM-DD>
category: <収集対象カテゴリから1つ以上>
status: unverified
---

# <タイトル>

## 要約

## 元情報からの引用・根拠

## 再現性メモ(実際に試した場合のみ)
```

## 守るべき制約

- 保存先は `N-HUB-OS/brain/research/` のみ。それ以外のディレクトリ、特に N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
- 検証済み(`brain/verified/`)への昇格はこのスキルの範囲外。未検証のまま `status: unverified` で保存する。
- 大量の自動巡回・常時ポーリングは行わない。呼ばれたときにその場で収集するタスク駆動型の動作とする。
