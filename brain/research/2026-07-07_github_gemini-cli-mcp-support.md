---
source: github
source_url: https://github.com/google-gemini/gemini-cli
collected_date: 2026-07-07
category: AI Agent
status: promoted
---

# Gemini CLIはGoogle公式のオープンソース端末型AIエージェントで、MCPに対応している

## 要約

`google-gemini/gemini-cli` は、Googleが公式に提供するオープンソース(Apache License 2.0)の端末型AIエージェント。ReAct(推論+実行)ループを内蔵し、ローカル・リモート両方のMCP(Model Context Protocol)サーバーに対応している。2026年7月7日時点でスター数10.6万、フォーク1.42万、リリース539回、直近リリースはv0.49.0(2026-06-25)と非常に活発に開発が続いている。

## 元情報からの引用・根拠

- 出典: [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)(一次ソース、公式リポジトリ)。README上で「🔌 Extensible: MCP (Model Context Protocol) support for custom integrations」と明記され、MCPサーバー設定の詳細ガイドも用意されている。

## 再現性メモ(実際に試した場合のみ)

未実施(リポジトリ・READMEの内容確認のみ)。

## Verification

- 2026-07-07: Google Cloud公式ドキュメント(`docs.cloud.google.com/gemini/docs/codeassist/gemini-cli`、独立2次ソース)で、オープンソースであることとMCPサーバー対応(ローカル・リモート)を独立に確認できたため、[brain/verified/gemini-cli-mcp-support.md](../verified/gemini-cli-mcp-support.md) へ昇格。
