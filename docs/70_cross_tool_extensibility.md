# 70. Cross-Tool Extensibility(方針文書)

**状態: 方針のみ。実装は行っていない**(2026-07-07時点、オーナーの明示的な判断による)。

## 考え方

N-HUB-OS は「AIを管理するAI」ではなく「知識を管理するOS」である([00_constitution.md](00_constitution.md))。AI(Claude Code, Gemini CLI, Codex CLI, Cursor, GitHub Copilot, OpenAI, Google Antigravity など)は入れ替わっても、`docs/`・`brain/` に蓄積された知識と判断基準は変わらずに使えることを目指す。

## 現状の依存関係(正直な棚卸し)

現在の実装は Claude Code に強く依存している:

- `skills/*/SKILL.md` は Claude Code の Skill 仕様そのもの
- N-Link(記憶・承認ガバナンス・品質ゲート)は `n-link-brain` という Claude Code 用 MCP として実装されている
- Bootstrap手順([50_bootstrap.md](50_bootstrap.md))はClaude Codeでの起動を前提にしている

したがって、他ツールへの対応は**将来の設計目標であり、現時点で動作するものではない**。

## 追加の実データ(2026-07-07)

Research skillの実運用で、Gemini CLI(Google公式のオープンソース端末型AIエージェント)がすでにMCPサーバー(ローカル・リモート両方)に対応していることを確認した([brain/verified/gemini-cli-mcp-support.md](../brain/verified/gemini-cli-mcp-support.md))。N-LinkがMCPベースで実装されていることを踏まえると、これは将来Gemini CLIからもN-Linkに接続できる可能性を示す好材料ではある。ただし、Gemini CLIがClaude CodeのSkill仕様(SKILL.md)をどう扱うかは別問題で、実際の対応検証はまだ行っていない(先取りして設計しない、原則は変わらず)。

## 将来の対応方針(案、未実装)

- `docs/` と `brain/` はツール非依存(プレーンなMarkdown/JSON)のため、そのまま他ツールからも読める。
- `skills/` はツールごとに実装形式が異なる(例: Cursorのrules、GitHub Copilotのinstructions等)。将来的には `skills/<engine>/<tool>/` のようにツール別のアダプタを追加する形を検討する(現時点では未設計)。
- N-Linkのようなガバナンス層をツール非依存にするか、各ツールごとに軽量な代替を用意するかは、実際に2つ目のツールへ対応する際に判断する(先取りして設計しない、[00_constitution.md](00_constitution.md) 原則3)。

## ロードマップとの関係

この文書は [90_roadmap.md](90_roadmap.md) の将来項目であり、実装タスクとして着手する場合は他のEngineと同様にN-Link canonical pipelineを通す。
