# N-HUB-OS

AIを管理するAIではなく、**知識を管理するOS**。AI(Claude Code, Gemini CLI, Codex CLI, Cursor, GitHub Copilot, OpenAI, Google Antigravity など)は入れ替わっても、蓄積した知識と判断基準は変わらずに使えることを目指す構想([docs/00_constitution.md](docs/00_constitution.md))。

現時点の実装は Claude Code 上で動作し、`n-link-brain`(N-Link)MCP をガバナンス層として利用する。他ツールへの対応は方針のみ([docs/70_cross_tool_extensibility.md](docs/70_cross_tool_extensibility.md))。

## まず読むもの

1. [CLAUDE.md](CLAUDE.md) — 絶対ルール(N-Link経由でのタスク実行・N-Link不可侵)
2. [docs/](docs/) — 構想の全容。`00_constitution.md` から番号順に読む
3. [docs/50_bootstrap.md](docs/50_bootstrap.md) — 新環境での再現手順
4. [docs/90_roadmap.md](docs/90_roadmap.md) — 現在地と次のマイルストーン

## ディレクトリ構成

```
N-HUB-OS/
  CLAUDE.md        絶対ルール
  docs/            構想全容(00 Why -> 10s What -> 20s 各Engine -> 30s+ How/運用)
  spec/            機械可読スキーマ(research note / verified knowledge / knowledge_graph.json)
  templates/       再利用可能なテンプレート
  bootstrap/       再現手順(詳細はdocs/50_bootstrap.mdに集約、ここは短い入口)
  skills/          実働するClaude Code Skill
  mcp/             MCPサーバーの選定・registry
  brain/           Second Brain(research/ verified/ knowledge_graph.json)
  self-evolution/  VERSION・CHANGELOG.md
  examples/        実例(蓄積され次第追加)
```

## 現在地

[docs/90_roadmap.md](docs/90_roadmap.md) と [self-evolution/CHANGELOG.md](self-evolution/CHANGELOG.md) を参照。
