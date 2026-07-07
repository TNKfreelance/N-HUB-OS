# 23. Skill Engine

このドキュメントは各 skill の仕様(目的・入出力)を定義する。**実コード(SKILL.md)はここでは作らない。** 各 skill の実装は個別タスクとして、必要になった時点で N-Link canonical pipeline(`brain_analyze_task` -> ... -> `brain_evaluate_council`)でゲートしながら `skills/<name>/` に作成する([90_roadmap.md](90_roadmap.md) で優先順位を管理)。

## Skill 一覧

| Skill | 目的 | 入力 | 出力 |
|---|---|---|---|
| Research | [20_research_engine.md](20_research_engine.md) に従い一次情報を収集する | 収集対象カテゴリ/キーワード | `brain/research/*.md` |
| Verification | 収集物を裏取りし検証済みへ昇格判定する | `brain/research/*.md` | `brain/verified/*.md` または却下理由の追記 |
| Knowledge | 検証済み知識を Second Brain / Knowledge Graph に構造化する | `brain/verified/*.md` | `brain/knowledge_graph.json` の更新 |
| SecondBrain | brain/ 全体の整合性チェック・重複排除・アーカイブ運用 | `brain/` 配下全体 | 整合性レポート、`brain/archive/` への移動 |
| SkillBuilder | 新しい Claude Code Skill を設計・生成する | 知見 + 生産依頼 | `skills/<name>/SKILL.md` |
| MCPBuilder | 必要な MCP サーバーを選定・導入・薄いラッパーを作る | 知見 + 生産依頼 | `mcp/registry.md` の追記、必要なら `mcp-server-dev` skill 呼び出し |
| Writer | 検証済み知識から記事・台本などのコンテンツ原稿を作る | `brain/verified/*.md` + `templates/` | 原稿ファイル |
| Automation | 定型作業のワークフロー化(スケジュール実行含む) | 生産依頼 | 保存先は実装時に確定させる(現時点で先取りして仕様化しない) |
| Publisher | 承認済み成果物を外部チャネルへ公開する | 承認済み成果物 + `brain_approval_check` 結果 | 公開ログ(保存先は実装時に確定させる) |
| Analytics | 公開後の利用実績を分析し、収集優先順位にフィードバックする | 利用実績データ | `brain/verified/` への注記、`02_principles.md` の優先順位見直し提案 |

## 共通ルール

- 各 skill は生成後、Claude Code の正式な Skill 仕様(SKILL.md + frontmatter、`description` はトリガー精度重視で具体的に書く)に従う。独自フォーマットを発明しない。
- 各 skill の実装完了時は `skill-creator:skill-creator` または `plugin-dev:skill-development` skill を使って品質確認を行い、その後に N-Link の品質ゲートを通す。
- 副作用のある処理(外部送信・公開・課金)を伴う skill は、内部で必ず `brain_approval_check` を呼ぶ設計にする。

## 実装順序の目安

[90_roadmap.md](90_roadmap.md) に記載。一般には依存関係の少ない Research → Verification → Knowledge の順が自然だが、実際の着手順は都度のタスク依頼に従う。
