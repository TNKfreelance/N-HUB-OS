# Changelog

形式は [Keep a Changelog](https://keepachangelog.com/) に準拠。バージョニング方針は [docs/60_self_evolution.md](../docs/60_self_evolution.md)。

**注記(2026-07-07)**: v1.0.0でリポジトリ全体を N-HUB → N-HUB-OS へリネーム・再構成した際、v0.1.0〜v0.6.0のエントリ内のパス表記(`Specification/` → `docs/`、`Skills/` → `skills/` 等)は現在の実際の場所を指すように機械的に更新した。各バージョン時点で実際に存在したファイル名・大文字小文字とは異なる場合があるが、内容(何を作ったか)自体は変更していない。

## [1.4.0] - 2026-07-07

### Added
- brain/research/2026-07-07_github_claude-code-recent-releases.md — Claude Codeの直近リリース(v2.1.196〜v2.1.202)を実際にGitHub Releasesから収集(MCP以外の新しい対象領域への実運用拡大)
- brain/verified/claude-code-2026-q3-updates.md — 独立4ソース(GitHub Releases・anthropic.com/news・platform.claude.com/docs・ai-tldr.dev)で裏取りできた2項目(Sonnet 5デフォルト化・バックグラウンドサブエージェント標準化)のみを検証済みへ昇格
- articles/claude-code-2026-q3-updates.md — 上記の検証済み知識から記事下書きを作成(未検証の因果関係の主張は「推測」と明記し断定しなかった)

### Verified
- 収集した6項目のうち、独立裏取りできたのは2項目のみだったため、research note には「部分昇格」であることを明記し、残り4項目(組織デフォルトモデル・AskUserQuestion挙動変更・スタック形式slash-skill・動的ワークフローサイズ)はGitHub単独ソースのまま未検証で残した(過剰な断定を避けた)
- SecondBrainの整合性チェックを実データ(research 3件・verified 3件・graph node3/edge1)に対して実行。ノード/ファイルの1:1対応・昇格リンクとも問題なし

## [1.3.0] - 2026-07-07

### Changed(破壊的変更)
- リポジトリ https://github.com/TNKfreelance/N-HUB-OS を **プライベート → パブリック** に変更した。理由: GitHub Pagesはプライベートリポジトリでは無料プランで利用できないという実際のプラットフォーム制約に当たったため(APIで実際に`422: Your current plan does not support GitHub Pages`を確認)、オーナーに選択肢を提示した上で「公開に切り替えてPagesを有効化」という明示判断を得た。`brain/`の実データはMCPに関する技術情報のみで機密情報・個人情報は含まれないことを事前にスキャンで確認済み(v1.2.0のPublisher機能テストで実施したgrepスキャン参照)

### Added
- `docs/_config.yml`、`docs/index.md` — GitHub Pages(Jekyll)用の設定とホームページ
- GitHub Pagesを実際に有効化: https://tnkfreelance.github.io/N-HUB-OS/ (source: main branch /docs)

### Verified
- 実際にAPIでPagesを有効化し、ビルドステータスが`built`になったことを確認。さらにトップページと個別ドキュメントページ(00_constitution)の両方を実際にWebFetchで取得し、正しくHTMLとしてレンダリングされていること(404でも生Markdownでもないこと)を確認した

## [1.2.0] - 2026-07-07

### Added
- skills/writer/SKILL.md、templates/article.md、articles/(新規ディレクトリ) — 検証済み知識から記事下書きを作成するskill([docs/23_skill_engine.md](../docs/23_skill_engine.md) の Writer 行に対応)
- skills/automation/SKILL.md、automation/(新規ディレクトリ) — 低リスクな定型タスクのワークフロー定義skill(Automation 行に対応)
- skills/publisher/SKILL.md — 公開前チェックリストとオーナー承認ゲート(Publisher 行に対応)
- skills/analytics/SKILL.md — 公開実績の分析(Analytics 行に対応)

### Verified
- Writer: 実際に2件の検証済み知識から記事下書き `articles/mcp-2026-latest-updates.md` を作成。`brain/verified/` にない新規の主張は追加しなかった
- Automation: 実際にSecondBrain整合性チェックのワークフロー定義 `automation/secondbrain-integrity-check.md` を作成。ステータスは`defined`のまま、実際のスケジュール有効化はオーナー承認待ちとして意図的に見送った
- Publisher: 公開前チェックリストをN-HUB-OSリポジトリ全体(GitHub公開予定)に対して実際に適用。引用元明記・機密情報/シークレットの不在(grepスキャン実施)・裏取り根拠の3点を確認
- Analytics: `articles/publish_log.md` の存在を実際に確認したところ公開実績がまだ無かったため、「分析対象なし」と正直に報告(架空のデータを作成しなかった)
- これにより`docs/23_skill_engine.md`に定義された10skill(Research/Verification/Knowledge/SkillBuilder/SecondBrain/MCPBuilder/Writer/Automation/Publisher/Analytics)すべての実装・実地テスト・独立監査が完了

## [1.1.0] - 2026-07-07

### Added
- skills/mcpbuilder/SKILL.md — MCPサーバーを4基準(必要性・信頼性・権限・N-Link非衝突)で評価し`mcp/registry.md`に記録するskill([docs/23_skill_engine.md](../docs/23_skill_engine.md) の MCPBuilder 行に対応)

### Verified
- 実地機能テストとして、実在の`github/github-mcp-server`(GitHub公式)を4基準で評価。信頼性・権限・N-Link非衝突は問題ないが、必要性基準(Research skillの現需要は既存のWebSearch/WebFetchで足りる)を満たさないため「却下」と判断し、理由とともに`mcp/registry.md`へ記録。導入すること自体を目的化せず、過剰実装回避の原則を実地で適用した

## [1.0.0] - 2026-07-07

### Changed(破壊的変更)
- リポジトリ全体を `N-HUB/` → `N-HUB-OS/` へリネーム。ユーザー提示の3案を統合した構造に再編:
  - `Specification/` → `docs/`(00-03 Why, 10-12 What, 20-28 各Engine, 30 How, 50 Bootstrap, 60 Self Evolution, 70 Cross-Tool Extensibility, 90 Roadmap の番号帯に再編)
  - `Skills/ MCP/ Brain/ Templates/ Bootstrap/ SelfEvolution/` → 小文字の `skills/ mcp/ brain/ templates/ bootstrap/ self-evolution/`(中身は無変更、実データ・監査履歴も保持)
  - 空スキャフォールドだった `Workflow/ Automation/ Platform/ Documentation/` を削除し、内容を `docs/` とルート `README.md` に統合(実データの損失なし)
- 新規追加: ルート `README.md`(人間向けエントリーポイント)、`spec/`(機械可読スキーマ3点)、`examples/`(空、将来用)
- 新規ドキュメント: `docs/03_terminology.md`、`docs/21_verification_engine.md`、`docs/22_knowledge_engine.md`、`docs/26_writer_engine.md`(未実装エンジンの仕様)、`docs/28_analytics_engine.md`(未実装エンジンの仕様)、`docs/30_development_rules.md`、`docs/70_cross_tool_extensibility.md`(Claude Code以外のツールへの拡張性は方針文書のみ、実装なし)

## [0.6.0] - 2026-07-07

### Added
- skills/secondbrain/SKILL.md — `brain/`全体(research/verified/knowledge_graph.json)を横断する整合性チェックとアーカイブ運用を担うskill([docs/23_skill_engine.md](../docs/23_skill_engine.md) の SecondBrain 行に対応)

### Verified
- 実地機能テストとして、現在の実データ(research 2件・verified 2件・graph node2/edge1)に対し6項目の整合性チェック(昇格リンク切れ・ノード欠落・孤立エッジ・未検証放置・重複見落とし・アーカイブ候補)を実行。全項目で問題なし、アーカイブ操作も発生せず

## [0.5.0] - 2026-07-07

### Added
- skills/skillbuilder/SKILL.md — N-HUB-OS skillの規約(命名・セクション構成・frontmatter・N-Linkブラックリスト)を定義し、新規skill作成と既存skillの規約チェックを担うskill([docs/23_skill_engine.md](../docs/23_skill_engine.md) の SkillBuilder 行に対応)。汎用の `skill-creator:skill-creator` は置き換えず、フルeval/ベンチマークループが必要な場合はそちらに委譲する設計

### Verified
- 実地機能テストとして、Research/Verification/Knowledgeの3skillに対しSkillBuilderの規約チェックリストを実行。N-Linkブラックリストの文言・命名規則(`n-hub-<engine>`)・セクション順序(目的→ドメイン固有→手順→出力フォーマット→守るべき制約)のドリフトはゼロ件

## [0.4.0] - 2026-07-07

### Added
- skills/knowledge/SKILL.md — 検証済みエントリ同士の関連性を精査し `knowledge_graph.json` と `related_ids` を同期させるskill([docs/23_skill_engine.md](../docs/23_skill_engine.md) の Knowledge 行に対応)

### Changed
- brain/verified/mcp-2026-07-28-stateless-spec.md, mcp-registry-live-service.md — 既存の`related`エッジ(Verification skillが昇格時に追加)の分類を実際に本文を読んで再確認し正しいと判断、両ファイルの`related_ids`をエッジと同期。version 1→2、`## 変更履歴`に追記。`knowledge_graph.json`自体は変更なし(既存分類が正しかったため)

## [0.3.0] - 2026-07-07

### Added
- skills/verification/SKILL.md — 未検証ノートを裏取りし `brain/verified/` へ昇格させるskill([docs/23_skill_engine.md](../docs/23_skill_engine.md) の Verification 行に対応)
- brain/verified/mcp-2026-07-28-stateless-spec.md — 独立3ソース(公式ブログ・WorkOS・mcp.directory)の一致により昇格した検証済み知識
- brain/verified/mcp-registry-live-service.md — レジストリAPIへの実アクセス(再現確認)により昇格した検証済み知識
- brain/knowledge_graph.json にノード2件・エッジ1件を追加

### Changed
- 対応する2件のresearchノートを `status: promoted` に更新し、`## Verification` セクションで昇格先を記録

## [0.2.0] - 2026-07-07

### Added
- skills/research/SKILL.md — 最初の実働 skill。海外一次情報の収集を行う([docs/23_skill_engine.md](../docs/23_skill_engine.md) の Research 行、[docs/20_research_engine.md](../docs/20_research_engine.md) に対応)
- skill-creator のガイドラインに沿って作成。タスクが低リスク・仕様が明確(N-HUB-OS独自仕様書に厳密に従うのみ)なため、フルの eval/ベンチマークループは今回省略し、独立監査官1名によるレビューで代替した

## [0.1.0] - 2026-07-06

### Added
- N-HUB-OS/CLAUDE.md(絶対ルール: N-Link経由でのタスク実行、N-Linkフォルダ不可侵)
- docs/00〜12(全13ドキュメント: Philosophy, Vision, Principles, Architecture, Workflow, Research, Knowledge, Skills, MCP, Automation, Publishing, Evolution, Roadmap)
- トップレベルスキャフォールド: bootstrap/, skills/, mcp/, brain/, Workflow/, Automation/, templates/, Platform/, Documentation/, self-evolution/
- bootstrap/README.md(再現手順)
