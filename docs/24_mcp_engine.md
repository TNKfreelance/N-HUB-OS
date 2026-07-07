# 24. MCP Engine

## MCP サーバー導入基準

新しい MCP サーバーを N-HUB-OS に組み込む前に、以下を確認する:

1. **必要性** — 既存の skill・組み込みツール(WebSearch/WebFetch 等)でカバーできないか
2. **信頼性** — 公式提供か、メンテナンスされているか
3. **権限** — 認証情報の取り扱い、アクセス範囲が最小限か
4. **N-Link との非衝突** — `n-link-brain` を無効化・上書きする設定を行わない(`recommended_mcps` で core は常に候補から除外される)

## 選定フロー

```
brain_recommend_mcps(task) で N-Link にプロファイル/候補を判断させる(決定のみ)
        |
        v
実際の ON/OFF 切り替えは connector-switcher skill が dry-run + ユーザー確認の上で実行する
(N-HUB-OS / N-Link 自身は MCP を勝手に切り替えない)
```

## レジストリ

`mcp/registry.md` に、導入済み・検討中の MCP サーバーを一覧管理する。

```markdown
| MCP名 | 用途 | 状態 | 備考 |
|---|---|---|---|
```

## 自前 MCP サーバーの実装が必要な場合

既存 MCP で要件を満たせない場合のみ、`mcp-server-dev:build-mcp-server` skill に委譲して新規実装を検討する。実装は個別タスクとして N-Link canonical pipeline でゲートする。
