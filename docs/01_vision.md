# 01. Vision

## ゴール

N-HUB-OS は、以下のループを継続的に回すシステムになる。

```
海外一次情報の収集 → 検証 → 知識化(Second Brain)
      → skill / MCP / 記事 / 動画 / 自動化ワークフローの生成
      → 公開・共有 → 利用実績の分析 → 次の収集対象へフィードバック
```

## 対象領域(収集・生産の重点分野)

構想書(N-HUB.txt)で列挙された重点分野をそのまま採用する:

- Claude Code / MCP(Model Context Protocol)/ AI Agent
- Browser Automation(Playwright, Puppeteer, Browser Use)
- AI Workflow(n8n, LangGraph, CrewAI, AutoGen)
- AI Video Generation
- AI Coding
- AI SaaS
- Immersive Web(Three.js, WebGPU, React Three Fiber)

## 生産する成果物の種類

| 種別 | 説明 | 保存先 |
|---|---|---|
| Skill | Claude Code Skill | `skills/` |
| MCP | MCP サーバーの導入・薄いラッパー | `mcp/` |
| Template | 再利用可能なテンプレート | `templates/` |
| Article | 記事・note 用原稿 | `brain/verified/` 由来、保存先は実装時に確定 |
| Video | 動画企画・台本・成果物メタ情報 | 個別プロジェクトフォルダ(実体はローカル別途管理) |
| Workflow | 自動化ワークフロー定義 | 保存先は実装時に確定(未実装) |

## 「できあがった状態」の定義(このドキュメント群における MVP)

このリポジトリを `git clone` し、Claude Code で開けば、[CLAUDE.md](../CLAUDE.md) と `docs/` を読むだけで以下が誰の手にも(どのモデル・どのホストでも)再現できること:

1. N-HUB-OS が何のためのプロジェクトかを誤解なく理解できる
2. 何が絶対ルールで、何が未実装(意図的に段階構築中)かを区別できる
3. 次に何を実装すべきかの優先順位([90_roadmap.md](90_roadmap.md))を迷わず判断できる

skill・MCP・engine の実コードそのものは MVP の対象外とし、各実装は個別タスクとして N-Link の canonical pipeline(`brain_analyze_task` → `brain_deploy_plan` → `brain_alignment_meeting` → 実装 → `brain_evaluate_council`)でゲートしながら段階的に積み上げる。
