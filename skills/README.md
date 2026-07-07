# Skills

N-HUB-OS が生産する Claude Code Skill の置き場。仕様は [docs/23_skill_engine.md](../docs/23_skill_engine.md) を参照。各 skill は個別タスクとして N-Link canonical pipeline を通してから `skills/<skill-name>/SKILL.md` の形で追加する(段階的構築、[docs/90_roadmap.md](../docs/90_roadmap.md) 参照)。

## 実装済み

- [research/SKILL.md](research/SKILL.md) — 海外一次情報の収集(docs/23_skill_engine.md の Research 行に対応)
- [verification/SKILL.md](verification/SKILL.md) — 未検証ノートの裏取り・brain/verified/ への昇格判断(docs/23_skill_engine.md の Verification 行に対応)
- [knowledge/SKILL.md](knowledge/SKILL.md) — 検証済みエントリ間の関連性の精査とknowledge_graph.json/related_idsの同期(docs/23_skill_engine.md の Knowledge 行に対応)
- [skillbuilder/SKILL.md](skillbuilder/SKILL.md) — 新しいN-HUB-OS skillの規約(命名・セクション構成・N-Linkブラックリスト)を定義し、既存skillの規約準拠をチェックする(docs/23_skill_engine.md の SkillBuilder 行に対応)
- [secondbrain/SKILL.md](secondbrain/SKILL.md) — brain/全体(research/verified/knowledge_graph.json)の横断整合性チェックとアーカイブ運用(docs/23_skill_engine.md の SecondBrain 行に対応)
- [mcpbuilder/SKILL.md](mcpbuilder/SKILL.md) — MCPサーバーの4基準評価とmcp/registry.mdへの記録(docs/23_skill_engine.md の MCPBuilder 行に対応)
- [writer/SKILL.md](writer/SKILL.md) — 検証済み知識から記事下書きを作成(docs/23_skill_engine.md の Writer 行に対応)
- [automation/SKILL.md](automation/SKILL.md) — 低リスクな定型タスクのワークフロー定義(docs/23_skill_engine.md の Automation 行に対応)
- [publisher/SKILL.md](publisher/SKILL.md) — 公開前チェックリストとオーナー承認ゲート(docs/23_skill_engine.md の Publisher 行に対応)
- [analytics/SKILL.md](analytics/SKILL.md) — 公開実績の分析とフィードバック(docs/23_skill_engine.md の Analytics 行に対応)

## 未実装

なし。10の想定skillすべて実装済み(2026-07-07)。今後は実運用しながら各skillを改善していくフェーズ。
