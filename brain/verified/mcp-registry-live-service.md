---
title: MCP公式レジストリは実際に稼働しているサーバー発見サービスである
category: MCP
source_urls:
  - https://github.com/modelcontextprotocol/registry
  - https://registry.modelcontextprotocol.io/v0/servers?limit=3
verified_date: 2026-07-07
confidence: high
version: 2
related_ids:
  - mcp-2026-07-28-stateless-spec
---

# MCP公式レジストリは実際に稼働しているサーバー発見サービスである

## 結論(何が分かったか)

`modelcontextprotocol/registry` はAnthropic/MCP公式が運営するMCPサーバーの発見用レジストリで、単なる構想やドキュメントではなく実際に稼働中のREST APIサービスである。2025年9月にプレビュー公開、2025年10月にAPIがfreeze(v0.1)され、現在もプレビュー段階。

## 根拠(複数ソースの裏取り内容)

- **GitHubリポジトリ**(一次ソース): スター7,000+、フォーク893、リリース34回。公式ワーキンググループ(コーディネーター4名)が管理。
- **実際にAPIへアクセスして再現確認**(手元での再現): `https://registry.modelcontextprotocol.io/v0/servers?limit=3` に実際にアクセスしたところ、`name`・`description`・`version`・`remotes`・`repository`・`_meta`(公開/更新/有効化日時)を含む実在のMCPサーバーのJSONデータ(例: inference.sh, tandem/docs-mcp)が返ってきた。ページネーションカーソルも機能しており、書類上の構想ではなく実運用中のサービスであることを直接確認できた。

「独立した2ソース以上」または「実際に再現確認できた」という[docs/02_principles.md](../../docs/02_principles.md)の昇格条件のうち、後者(手元での再現確認)を満たす。

## 実用上の示唆(何に使えるか、どの Skill/成果物に繋がるか)

- N-HUB-OSのMCP Engine / MCPBuilder skillがMCPサーバーを選定する際、`registry.modelcontextprotocol.io/v0/servers`のAPIを実際に検索用途で使える([docs/24_mcp_engine.md](../../docs/24_mcp_engine.md)のMCP選定フローに組み込み候補)。
- プレビュー段階(破壊的変更の可能性あり)という点は、本番導入前に再確認すべき注意点として記録しておく。

## 変更履歴
- v1 2026-07-07 初版(brain/research/2026-07-07_github_mcp-registry.md より昇格)
- v2 2026-07-07 Knowledge skillによりknowledge_graph.jsonの既存related edge(mcp-2026-07-28-stateless-spec)をrelated_idsに同期。プロトコル仕様とレジストリサービスは別々の関心事のため"related"のまま(supersedes/depends_onではない)。
