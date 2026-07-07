# 03. Terminology

N-HUB-OS は将来的に Claude Code 以外の AI ツール(Gemini CLI, Codex CLI, Cursor, GitHub Copilot, OpenAI, Google Antigravity など、[70_cross_tool_extensibility.md](70_cross_tool_extensibility.md) 参照)からも読まれることを想定する。ツールが変わっても同じ理解に到達できるよう、ここで用語を固定する。

| 用語 | 意味 | ツール依存性 |
|---|---|---|
| N-HUB-OS | この構想全体。AI Knowledge Operating System。 | ツール非依存 |
| Engine | N-HUB-OSの機能単位(Research/Verification/Knowledge/Skill/MCP/Automation/Writer/Publishing/Analytics)。「何をするか」を定義する概念。 | ツール非依存 |
| Skill | Engineをそのツール上で実行可能な形にした実装。現状は Claude Code の Skill 仕様(`SKILL.md`)で実装されている。 | **Claude Code固有**(他ツールでは異なる実装形式になる) |
| Brain / Second Brain | `brain/` 配下に保存される知識ストア(`research/` 未検証、`verified/` 検証済み、`knowledge_graph.json`)。 | ツール非依存(単なるファイル群) |
| Knowledge Graph | 検証済み知識間の関連(`related`/`supersedes`/`depends_on`)を記録する軽量グラフ。 | ツール非依存 |
| Verified / Unverified | `brain/research/` は未検証、`brain/verified/` は独立2ソース以上または再現確認済みの知識。判断基準は [02_principles.md](02_principles.md)。 | ツール非依存 |
| N-Link | このリポジトリとは別に稼働する運用基盤(記憶・承認ガバナンス・品質ゲート)。`n-link-brain` という MCP として提供される。 | **Claude Code(またはMCP対応ツール)固有** |
| MCP | Model Context Protocol。外部ツール・データソースとAIを繋ぐ標準プロトコル。 | ツール横断で意味を持つが、実装呼び出し方法はツール依存 |
| Bootstrap | 新環境でN-HUB-OSを再現する手順。[50_bootstrap.md](50_bootstrap.md)。 | ツール非依存(手順自体は) |
| Golden Ticket | N-Linkが用いる10項目品質判定の名称。N-HUB-OS自体の用語ではなくN-Link側の概念。 | **N-Link固有** |

## 命名規則

- ドキュメント: `docs/<番号>_<英語スネークケース>.md`
- Skill: `skills/<engine-name>/SKILL.md`(現状Claude Code形式。他ツール対応時は`skills/<engine-name>/<tool>/`のような分岐を検討する。[70_cross_tool_extensibility.md](70_cross_tool_extensibility.md)参照)
- Brain内の検証済みファイル: `brain/verified/<slug>.md`(スラッグ = ファイル名 = knowledge_graph.jsonのノードid)
