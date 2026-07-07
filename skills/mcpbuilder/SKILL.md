---
name: n-hub-mcpbuilder
description: Evaluates candidate MCP servers against N-HUB-OS's 4 adoption criteria (necessity, reliability, permissions, N-Link non-conflict), records the decision in mcp/registry.md, and delegates actual new-server implementation to the mcp-server-dev:build-mcp-server skill when no existing MCP satisfies the need. Use this whenever the user asks to evaluate, add, register, or "導入して"/"検討して" an MCP server for N-HUB-OS, or explicitly says "N-HUB-OS MCPBuilder". Do not use this to actually write new MCP server code (that is mcp-server-dev:build-mcp-server's job) and do not use this to toggle which MCP profiles are active in a session (that is the connector-switcher skill's job).
---

# N-HUB-OS MCPBuilder Skill

## 目的

N-HUB-OSが必要とするMCPサーバーを選定し、`mcp/registry.md` に記録する。正本は `docs/24_mcp_engine.md`(導入基準・選定フロー)。実際に新規MCPサーバーを自前実装する必要がある場合は、このskillが直接コードを書くのではなく `mcp-server-dev:build-mcp-server` skillに委譲する。

## 導入基準(docs/24_mcp_engine.mdより)

1. **必要性** — 既存のskill・組み込みツール(WebSearch/WebFetch等)でカバーできないか
2. **信頼性** — 公式提供か、メンテナンスされているか
3. **権限** — 認証情報の取り扱い、アクセス範囲が最小限か
4. **N-Linkとの非衝突** — `n-link-brain` を無効化・上書きする設定を行わない

4つすべてを満たすもののみ `mcp/registry.md` に「導入済み」として記録する。1つでも満たさない場合は「検討中」または「却下」として理由とともに記録する(却下も記録として残す。存在しなかったことにしない)。

## 手順

1. 候補となるMCPサーバーを特定する(ユーザー指定、またはEngineの実需要から)。
2. 上記4基準を順に評価する。既存の組み込みツール(WebSearch/WebFetch等)で代替できる場合は「不要」と判断し、新規導入しない。
3. 4基準を満たす場合、`mcp/registry.md` に一行追加する(状態: 導入済み/検討中/却下)。
4. 自前実装が必要と判断した場合は、このskill自身は実装せず `mcp-server-dev:build-mcp-server` skillの利用をユーザーに提案する。
5. 実際に接続・動作確認ができた場合のみ「導入済み」とする。机上の評価だけで「導入済み」と書かない。

## 出力フォーマット

`mcp/registry.md` への追記行:

```markdown
| <MCP名> | <用途> | 導入済み/検討中/却下 | <4基準の評価根拠を簡潔に> |
```

## 守るべき制約

- 書き込み先は `mcp/registry.md` のみ。実際のMCPサーバーコードは書かない(`mcp-server-dev:build-mcp-server` に委譲)。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
- `n-link-brain` を無効化・上書きするような推奨は行わない(常に候補から除外)。
- MCPプロファイルの実際のON/OFF切り替えは行わない(`connector-switcher` skillの範囲)。
- 実際に接続確認していないものを「導入済み」と書かない(却下・検討中は正直に記録する)。
