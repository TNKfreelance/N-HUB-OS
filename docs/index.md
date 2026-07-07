# N-HUB-OS

> AIを管理するAIではない。
> 知識を管理するOSである。
>
> AIが変わっても、知識は変わらない。
>
> 知識を資産に変える。
> 検証を標準化する。
> 成果物を自動生成する。
> 知識を継続的に進化させる。

[GitHubリポジトリ](https://github.com/TNKfreelance/N-HUB-OS)

## 構成原理: Why → What → How → Implementation

構想は4段階で組み立てる。**Why**(存在理由・ビジョン・原則)が先にあり、それを**What**(アーキテクチャ・Brain・ワークフロー)が形にし、**How**(開発規約・再現手順・進化サイクル)が運用方法を定め、最後に**Implementation**(実働するskill・MCP・成果物)として実装される。逆順には作らない。

```
Why  (00-03)  存在理由・ビジョン・原則・用語
  ↓
What (10-12)  アーキテクチャ・Brain・ワークフロー
  ↓
How  (30-70)  開発規約・再現手順・進化サイクル・拡張性方針
  ↓
Implementation  実際に稼働する10のskill([23. Skill Engine](23_skill_engine)参照)
```

## N-HUB-OS ↓ 使えるツール

N-HUB-OSはAIツールに依存しない構想として設計されている。現在の実装はClaude Codeに強く依存しているが([70. Cross-Tool Extensibility](70_cross_tool_extensibility)参照)、将来的には以下のようなツールから同じ`docs/`・`brain/`を読める設計を目指す:

Claude Code / Gemini CLI / Codex CLI / Cursor / GitHub Copilot / OpenAI / Google Antigravity

## Why

- [00. Constitution](00_constitution)
- [01. Vision](01_vision)
- [02. Principles](02_principles)
- [03. Terminology](03_terminology)

## What

- [10. Architecture](10_architecture)
- [11. Brain (Second Brain & Knowledge Graph)](11_brain)
- [12. Workflow](12_workflow)

## Engines(Implementationの単位)

- [20. Research Engine](20_research_engine)
- [21. Verification Engine](21_verification_engine)
- [22. Knowledge Engine](22_knowledge_engine)
- [23. Skill Engine](23_skill_engine)
- [24. MCP Engine](24_mcp_engine)
- [25. Automation Engine](25_automation_engine)
- [26. Writer Engine](26_writer_engine)
- [27. Publishing Engine](27_publishing_engine)
- [28. Analytics Engine](28_analytics_engine)

## How

- [30. Development Rules](30_development_rules)
- [50. Bootstrap](50_bootstrap)
- [60. Self Evolution](60_self_evolution)
- [70. Cross-Tool Extensibility](70_cross_tool_extensibility)

## Roadmap

- [90. Roadmap](90_roadmap)
