---
source: github
source_url: https://github.com/modelcontextprotocol/registry
collected_date: 2026-07-07
category: MCP
status: promoted
---

# MCP Registry — MCPサーバーの公式コミュニティレジストリ

## 要約

`modelcontextprotocol/registry` は、MCPサーバーを発見・公開するためのコミュニティ主導のレジストリサービス(いわば「MCPサーバーのアプリストア」)。Anthropic/MCP公式が管理する公式プロジェクトで、専任のワーキンググループ(コーディネーター4名)が運営している。

- スター数 7,000+、フォーク 893、リリース34回(最新 v1.7.9)
- 2025年9月にプレビュー公開、2025年10月にAPIが「freeze (v0.1)」となり互換性が保証された
- 現在もプレビュー段階で、正式版(GA)は今後の予定。プレビュー中は破壊的変更やデータリセットが起こりうると明記されている

## 元情報からの引用・根拠

- 出典: [GitHub - modelcontextprotocol/registry](https://github.com/modelcontextprotocol/registry)
- リポジトリ説明文: "A community driven registry service for Model Context Protocol (MCP) servers."

## 再現性メモ(実際に試した場合のみ)

2026-07-07: `https://registry.modelcontextprotocol.io/v0/servers?limit=3` に実際にアクセスし、`name`/`description`/`version`/`remotes`/`repository`/`_meta`を含む実在サーバーのJSONが返ることを確認。書類上の構想ではなく実運用中のAPIであることを再現確認できた。

## Verification

- 2026-07-07: 上記の実アクセスによる再現確認により昇格条件(手元での再現確認)を満たしたため、[brain/verified/mcp-registry-live-service.md](../verified/mcp-registry-live-service.md) へ昇格。
