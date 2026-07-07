---
title: Gemini CLIはすでにMCPに対応している — Claude Code以外のツールとの接点
category: AI Agent
source_ids: [gemini-cli-mcp-support]
draft_date: 2026-07-07
status: draft
---

# Gemini CLIはすでにMCPに対応している — Claude Code以外のツールとの接点

## リード文

Googleが公式に提供するオープンソースの端末型AIエージェント「Gemini CLI」は、すでにMCP(Model Context Protocol)に対応している。これはClaude Code以外のツールへの拡張性を考える上で見過ごせない事実だ。

## 本文

Gemini CLI(`google-gemini/gemini-cli`)はApache License 2.0で公開されている、Googleの公式オープンソースプロジェクトだ。ReAct(推論+実行)ループを内蔵し、READMEには「MCP (Model Context Protocol) support for custom integrations」と明記されている。ローカル・リモート両方のMCPサーバーに接続できる。2026年7月時点でスター数は10.6万、直近リリースは6月25日と非常に活発に開発が続いている。

これがなぜ重要かというと、多くのAI Knowledge Operating Systemの構想は「特定のAIツールに縛られない」ことを掲げつつ、実際にはガバナンス層(記憶・承認・品質ゲート)を特定ツール用のプラグイン形式で実装せざるを得ないケースが多い。もしそのガバナンス層がMCPという標準プロトコルの上に作られていれば、少なくとも「MCPに対応しているツールであれば理論上は繋がる」という土台ができる。GeminiCLIがMCPに対応しているという事実は、その土台の一部がすでに存在することを意味する。

ただし、これはあくまで「プロトコルレベルで繋がる可能性がある」という話であり、Claude Code固有の概念(Skill仕様など)をGemini CLI側がどう解釈するかはまったく別の課題だ。実際に検証されたわけではないので、過度な期待は禁物である。

## 参考(根拠となった検証済み知識)

- [brain/verified/gemini-cli-mcp-support.md](../brain/verified/gemini-cli-mcp-support.md)
