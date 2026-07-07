---
title: MCP 2026-07-28仕様はプロトコルをステートレス化し認可を強化する
category: MCP
source_urls:
  - https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/
  - https://workos.com/blog/mcp-2026-spec-agent-authentication
  - https://mcp.directory/blog/mcp-2026-07-28-release-candidate
verified_date: 2026-07-07
confidence: high
version: 2
related_ids:
  - mcp-registry-live-service
---

# MCP 2026-07-28仕様はプロトコルをステートレス化し認可を強化する

## 結論(何が分かったか)

Model Context Protocol の2026-07-28仕様(現在RC、最終公開は2026年7月28日予定)は、`initialize`ハンドシェイクと`Mcp-Session-Id`によるセッション管理をプロトコルレベルから撤廃し、任意のサーバーインスタンスがどのリクエストも処理できる完全ステートレスな設計になる。あわせて OAuth 2.0 Protected Resource Metadata の実装必須化、Resource Indicators によるトークンの宛先サーバー限定など、認可まわりが大幅に強化される。

## 根拠(複数ソースの裏取り内容)

- **公式ブログ**(一次ソース): ステートレス化・拡張機能フレームワーク・認可強化・運用性改善(`Mcp-Method`/`Mcp-Name`ヘッダー等)・非推奨ポリシーを発表。RCロックは2026-05-21、最終公開は2026-07-28。
- **WorkOS社ブログ**(独立した2次ソース): 「`initialize`/`initialized`ハンドシェイクが廃止された」「`Mcp-Session-Id`ヘッダーが廃止された」「どのサーバーインスタンスでもリクエストを処理できる」ことを実例付きで確認。認可面では「MCPクライアントはResource Indicatorsの実装が必須になり、別サーバー宛のトークンを別サーバーで悪用できなくする」ことも明記。
- **mcp.directory**(独立した3次ソース): 同じくハンドシェイク・セッションID廃止、`_meta`オブジェクトへのプロトコルバージョン/クライアント情報の内包、2026-07-28の最終公開日を確認。

3つの独立したソース(公式・WorkOS・mcp.directory)が同一の技術的変更点を一致して報告しており、[docs/02_principles.md](../../docs/02_principles.md)の「独立2ソース以上」の昇格条件を満たす。

## 実用上の示唆(何に使えるか、どの Skill/成果物に繋がるか)

- N-HUB-OSが将来 MCP Engine / MCPBuilder skill を実装する際、2026-07-28以降にリリースされる新仕様のMCPサーバーはステートレス設計(ロードバランサ配下でのスケール)を前提にできる。
- 認可周りの変更(Resource Indicators必須化)は、N-HUB-OSがMCPサーバーを自作する場合のセキュリティ設計に直接影響する([docs/24_mcp_engine.md](../../docs/24_mcp_engine.md)の導入基準に反映を検討)。

## 変更履歴
- v1 2026-07-07 初版(brain/research/2026-07-07_official_mcp-2026-07-28-release-candidate.md より昇格)
- v2 2026-07-07 Knowledge skillによりknowledge_graph.jsonの既存related edge(mcp-registry-live-service)をrelated_idsに同期。話題は同じMCPエコシステムだが、プロトコル仕様と発見サービスという別々の関心事のため"related"のまま(supersedes/depends_onではない)。
