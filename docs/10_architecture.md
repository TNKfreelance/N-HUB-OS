# 10. Architecture

## 全体図

```
                          N-HUB-OS
        ---------------------------------------------
                     Intelligence Core
        ---------------------------------------------
          Research Engine        -> brain/research/
          Verification Engine    -> brain/verified/
          Knowledge Engine       -> brain/verified/ + knowledge_graph.json
          Skill Engine           -> skills/
          MCP Engine             -> mcp/
          Automation Engine      -> 保存先は実装時に確定(未実装)
          Writer Engine          -> templates/ 経由で Article/Video 原稿を生成(未実装)
          Publishing Engine      -> 公開チャネルへ(保存先は実装時に確定)
          Analytics Engine       -> 利用実績を brain/verified/ にフィードバック
        ---------------------------------------------
                    Second Brain (このリポジトリ自体)
          brain/research/   未検証の収集物(Markdown, front-matter付き)
          brain/verified/   検証済み知識(Markdown, front-matter付き)
          brain/knowledge_graph.json  知識間の関連(軽量グラフ)
        ---------------------------------------------
                        Output
          Skill / MCP / Template / Article / Video / Workflow
        ---------------------------------------------
```

## ガバナンス層(外部依存)

N-HUB-OS は自前のガバナンス層を持たず、すべて `n-link-brain` MCP に委譲する。

```
N-HUB-OS の各 Engine が何かを実装・実行する
        |
        v
n-link-brain MCP (N-Link)
  brain_analyze_task    -> 何を作るべきかの意図解析
  brain_approval_check  -> 副作用のある操作の承認ゲート
  brain_deploy_plan /
  brain_alignment_meeting -> 規模の大きいタスクの設計合意(user_gate)
  brain_evaluate_quality /
  brain_evaluate_council -> 品質ゲート(Golden Ticket)
  brain_record_success /
  brain_remember         -> 学習・記憶
```

N-Link 側のデータ(`~/.n-link`, `N-Link-Project` 等)には N-HUB-OS から直接アクセスしない。すべて MCP ツール呼び出し経由。

## モジュール境界

- 各 Engine は独立したディレクトリに 1 対 1 対応させ、循環依存を作らない(Research → Verification → Knowledge は一方向のパイプライン)。
- Skill Engine が生成する成果物(`skills/*`)は Claude Code の Skill 仕様(SKILL.md + frontmatter)にそのまま従う。独自フォーマットを発明しない。
- MCP Engine は既存 MCP サーバーの選定・薄い設定を扱う。新規 MCP サーバーの自前実装が必要な場合のみ `mcp-server-dev:build-mcp-server` skill に委譲する。

## インターフェース契約

- Engine 間のデータ受け渡しは Markdown(front-matter 付き)または JSON に限定する(バイナリ・独自DBを増やさない)。
- すべてのファイルは相対パスで相互参照可能にし、`git clone` だけで解決できること([50_bootstrap.md](50_bootstrap.md) 参照)。
