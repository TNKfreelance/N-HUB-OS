# MCP Registry

導入済み・検討中の MCP サーバーの一覧。詳細な選定基準は [24_mcp_engine.md](../docs/24_mcp_engine.md)。

| MCP名 | 用途 | 状態 | 備考 |
|---|---|---|---|
| n-link-brain | N-HUB-OS全体のガバナンス・記憶・品質ゲート | 導入済み(常時ON、core) | N-Link本体。N-HUB-OSから無効化しない |
| github/github-mcp-server | GitHubリポジトリの閲覧・Issue/PR管理・コード検索 | 却下(2026-07-07時点) | 必要性: Research skillの現在の需要(GitHub上の情報収集)は既存の`WebSearch`/`WebFetch`で足りており、専用MCP導入の必要性基準を満たさない([docs/00_constitution.md](../docs/00_constitution.md)原則3、過剰実装回避)。信頼性: 公式(`github/github-mcp-server`)で問題なし。権限: Issue/PR作成・コード変更等の書き込み系スコープを含みうるため、将来Publishing Engine等で実際にGitHub操作が必要になった時点で改めて評価する。N-Link非衝突: 問題なし。 |
