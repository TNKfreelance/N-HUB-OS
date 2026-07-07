---
title: Gemini CLIはGoogle公式のオープンソース端末型AIエージェントで、MCPに対応している
category: AI Agent
source_urls:
  - https://github.com/google-gemini/gemini-cli
  - https://docs.cloud.google.com/gemini/docs/codeassist/gemini-cli
verified_date: 2026-07-07
confidence: high
version: 1
related_ids: [mcp-2026-07-28-stateless-spec]
---

# Gemini CLIはGoogle公式のオープンソース端末型AIエージェントで、MCPに対応している

## 結論(何が分かったか)

Googleは`gemini-cli`という公式のオープンソース(Apache 2.0)端末型AIエージェントを提供しており、ReActループを内蔵し、ローカル・リモート両方のMCPサーバーに対応している。2026年7月時点でスター数10.6万・非常に活発な開発が続いている実運用中のツールである。

## 根拠(複数ソースの裏取り内容)

- **GitHubリポジトリ**(一次ソース、`google-gemini/gemini-cli`): READMEに「MCP (Model Context Protocol) support for custom integrations」と明記。Apache License 2.0、スター10.6万、直近リリースv0.49.0(2026-06-25)を確認。
- **Google Cloud公式ドキュメント**(独立した2次ソース、`docs.cloud.google.com`): オープンソースであること、「ローカル・リモートのMCPサーバー」に対応していることを独立に確認。

2つの独立した公式ソースが一致しており、[docs/02_principles.md](../../docs/02_principles.md)の昇格条件を満たす。

## 実用上の示唆(何に使えるか、どの Skill/成果物に繋がるか)

- N-HUB-OSの[docs/70_cross_tool_extensibility.md](../../docs/70_cross_tool_extensibility.md)は「Claude Code以外への対応は未設計」としているが、Gemini CLIがすでにMCPに対応していることは、将来N-HUB-OSがN-Link(MCPベース)経由でGemini CLIからも動作できる可能性を示す好材料である。ただし、Gemini CLIがClaude CodeのSkill仕様(SKILL.md)を認識できるかどうかは別問題であり、実際の対応は別タスクとして検証が必要。

## 変更履歴
- v1 2026-07-07 初版(brain/research/2026-07-07_github_gemini-cli-mcp-support.md より昇格)
