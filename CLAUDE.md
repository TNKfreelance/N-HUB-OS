# N-HUB-OS — AI Knowledge Operating System

このファイルは N-HUB-OS プロジェクトの憲法(Constitution)。Claude Code は N-HUB-OS 配下で作業する際、必ずこの内容に従う。

## N-HUB-OS とは

N-HUB-OS は単一の skill でも単発のツールでもなく、**AI Knowledge Operating System** である。AIを管理するAIではなく、知識を管理するOS。AI(Claude Code / Gemini CLI / Codex CLI / Cursor / GitHub Copilot / OpenAI / Google Antigravity など)が入れ替わっても、蓄積した知識と判断基準は変わらずに使えることを目指す(詳細は [docs/00_constitution.md](docs/00_constitution.md))。現時点の実装は Claude Code に依存しており、他ツール対応は方針のみ([docs/70_cross_tool_extensibility.md](docs/70_cross_tool_extensibility.md))。

目的は「世界最先端のAI技術情報(Claude Code / MCP / AI Agent / Browser Automation / AI Video / AI Coding / AI SaaS / Immersive Web 等)を継続的に収集・検証・蓄積し、その知見から skill・MCP・記事・動画・自動化ワークフローなどの成果物を高品質かつ継続的に生み出す」こと。

中核モデル:

```
Intelligence Core
  Research Engine        海外一次情報の収集
  Verification Engine    再現性・信頼性の検証
  Knowledge Engine        検証済み知見の構造化
  Skill Engine            Claude Code Skill の生成・更新
  MCP Engine               MCP サーバーの選定・実装
  Automation Engine       ワークフロー自動化
  Writer Engine            記事・動画などのコンテンツ生成
  Publishing Engine        note/SNS/GitHub 等への配信
  Analytics Engine         成果・利用状況の分析

Second Brain
  Markdown / JSON / Knowledge Graph としてバージョン管理

Output
  Skill / MCP / Template / Article / Video / GitHub / Premium
```

ディレクトリ構成(確定、詳細は [docs/10_architecture.md](docs/10_architecture.md)):

```
N-HUB-OS/
  CLAUDE.md          このファイル(憲法)
  README.md          人間向けエントリーポイント
  docs/              構想の全容(00_constitution.md 〜 90_roadmap.md、番号帯の意味は下記)
  spec/              機械可読スキーマ(research note / verified knowledge / knowledge_graph.json)
  templates/         research_note.md / verified_knowledge.md 等
  bootstrap/         再現手順の入口(詳細は docs/50_bootstrap.md)
  skills/            実働する Claude Code Skill
  mcp/               MCPサーバーの選定・registry.md
  brain/             N-HUB-OS自身のSecond Brain(research/ verified/ knowledge_graph.json)
                     ※ N-Link の脳(~/.n-link)とは別物。混同しないこと
  self-evolution/    VERSION / CHANGELOG.md
  examples/          実例(蓄積され次第追加)
```

`docs/` の番号帯:

| 番号帯 | 意味 |
|---|---|
| 00-03 | Why(存在理由・ビジョン・原則・用語) |
| 10-12 | What(アーキテクチャ・Brain・ワークフロー) |
| 20-28 | 各Engine(Research/Verification/Knowledge/Skill/MCP/Automation/Writer/Publishing/Analytics) |
| 30 | How(開発規約) |
| 50 | Bootstrap(再現手順) |
| 60 | Self Evolution(改善サイクル) |
| 70 | Cross-Tool Extensibility(方針のみ) |
| 90 | Roadmap |

将来構築する Skill 群(優先順位は [docs/90_roadmap.md](docs/90_roadmap.md) を参照):
Research / Verification / Knowledge / SecondBrain / SkillBuilder / MCPBuilder / Writer / Automation / Publisher / Analytics

## 絶対ルール

1. **すべてのタスクは N-Link を通して行う。**
   N-Link は `n-link-brain` MCP として接続されている運用基盤(記憶・承認ガバナンス・品質ゲート)。実装作業に着手する前に必ず `brain_analyze_task` を呼び、副作用のあるアクション(ファイル削除・外部送信・課金・不可逆操作など)の前には必ず `brain_approval_check` を呼ぶ。タスク完了を宣言する前に `brain_evaluate_quality` の判定を経る。これを迂回して N-HUB-OS 内の作業を進めてはならない。

2. **N-Link 関連フォルダには一切触れない。**
   閲覧・編集・削除・移動のいずれも禁止。具体的には以下(および今後 `N-Link` / `n-link` を名前に含むことが確認された新規フォルダ)を対象とする:
   - `~/.n-link`(brain.db / identity.json — n-link-brain MCP の実データ)
   - `~/N-Link-Project`
   - `~/N-Link-Cockpit`
   - `~/N-Link-Cockpit-Electron`
   - `~/N-Link ♾️`
   - `~/N-link`
   - `~/n-link-brain.stale_bak_20260621`(旧バックアップ)
   N-HUB-OS からこれらの内容を読む必要がある場合も、直接ファイル操作はせず、必ず `n-link-brain` MCP のツール経由で行う。

3. **N-HUB-OS は N-Link の下位互換ではなく別プロジェクト。**
   N-Link がガバナンス・記憶・承認を担う「脳」であるのに対し、N-HUB-OS はその脳を使って知識収集・skill/コンテンツ生産を行う「作業場」。両者のコードベース・データストアを混在させない。

4. **段階的に構築する。**
   構想全体の仕様([docs/](docs/))はすでに完成しているが、実働する skill・MCP・自動化コードの実装は一度に行わない。個々のタスクごとに `brain_analyze_task` の指示に従い、必要な範囲から着手する。

## 詳細仕様

構想の全容・判断基準・アーキテクチャ・各Engineの仕様は [docs/](docs/) に 00〜90 の番号順で格納されている。新しいセッションで全体像を復元したい場合は、まずこのファイルを読み、次に `docs/00_constitution.md` から `docs/90_roadmap.md` まで番号順に読むこと。再現手順の詳細は [docs/50_bootstrap.md](docs/50_bootstrap.md)。

| 文書 | 内容 |
|---|---|
| [docs/00_constitution.md](docs/00_constitution.md) | 存在理由、N-Linkとの関係、非目標 |
| [docs/01_vision.md](docs/01_vision.md) | ゴール、対象領域、成果物種別 |
| [docs/02_principles.md](docs/02_principles.md) | 情報源優先順位、検証済み昇格条件、除外対象 |
| [docs/03_terminology.md](docs/03_terminology.md) | 用語集(ツール依存/非依存の区別を含む) |
| [docs/10_architecture.md](docs/10_architecture.md) | Intelligence Core全体図、ガバナンス層、モジュール境界 |
| [docs/11_brain.md](docs/11_brain.md) | Second Brain / Knowledge Graph 保存形式 |
| [docs/12_workflow.md](docs/12_workflow.md) | N-Link canonical pipelineに沿った標準タスクフロー |
| [docs/20_research_engine.md](docs/20_research_engine.md) | 収集対象・重複排除・保存形式 |
| [docs/21_verification_engine.md](docs/21_verification_engine.md) | 昇格条件・実績 |
| [docs/22_knowledge_engine.md](docs/22_knowledge_engine.md) | 関連性の分類・実績 |
| [docs/23_skill_engine.md](docs/23_skill_engine.md) | 各Skillの目的・入出力 |
| [docs/24_mcp_engine.md](docs/24_mcp_engine.md) | MCP導入基準・選定フロー |
| [docs/25_automation_engine.md](docs/25_automation_engine.md) | 自動化してよい/いけない範囲 |
| [docs/26_writer_engine.md](docs/26_writer_engine.md) | 未実装。コンテンツ生成の仕様 |
| [docs/27_publishing_engine.md](docs/27_publishing_engine.md) | 公開前チェックリスト・承認フロー |
| [docs/28_analytics_engine.md](docs/28_analytics_engine.md) | 未実装。利用実績分析の仕様 |
| [docs/30_development_rules.md](docs/30_development_rules.md) | 命名・ドキュメント形式・バージョニング規約 |
| [docs/50_bootstrap.md](docs/50_bootstrap.md) | 再現手順 |
| [docs/60_self_evolution.md](docs/60_self_evolution.md) | N-HUB-OS自身の改善サイクル・バージョニング |
| [docs/70_cross_tool_extensibility.md](docs/70_cross_tool_extensibility.md) | 他AIツール対応方針(未実装) |
| [docs/90_roadmap.md](docs/90_roadmap.md) | 現在地(バージョンは [self-evolution/VERSION](self-evolution/VERSION) 参照)と次のマイルストーン |

各 Engine / マイルストーンは個別タスクとして着手時に `brain_analyze_task` へ渡し、承認が必要な操作は `brain_approval_check` でゲートすること。
