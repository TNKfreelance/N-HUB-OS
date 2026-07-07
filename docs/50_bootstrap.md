# 50. Bootstrap — 再現手順

新しい環境で N-HUB-OS を確実に再現するための手順。前提: Claude Code(または将来対応する他のAIツール、[70_cross_tool_extensibility.md](70_cross_tool_extensibility.md) 参照)が利用可能で、`n-link-brain`(N-Link)MCP が接続済みであること。N-HUB-OS は N-Link に依存するが、N-Link 自体のセットアップはこのドキュメントの範囲外([CLAUDE.md](../CLAUDE.md) 絶対ルール2により N-HUB-OS から N-Link のセットアップに手を出さない)。

## 手順

1. **リポジトリを取得する**
   ```
   git clone <N-HUB-OS のリポジトリURL> N-HUB-OS
   cd N-HUB-OS
   ```
   (まだ GitHub 化していない場合は、このディレクトリをそのままコピーする)

2. **Claude Code を起動する**
   `N-HUB-OS/` をカレントディレクトリとして Claude Code を開く。

3. **CLAUDE.md を読ませる**
   Claude Code は起動時に自動的に [../CLAUDE.md](../CLAUDE.md) を読み込む。これにより次が確定する:
   - N-HUB-OS とは何か
   - すべてのタスクは N-Link 経由で行うこと
   - N-Link 関連フォルダには一切触れないこと

4. **docs/ を 00 から順に読ませる**
   構想の全体像・判断基準・アーキテクチャ・各 Engine の仕様は [../docs/](../docs/) に番号順(00番台=Why、10番台=What/構造、20番台=各Engine、30番台以降=開発規約・再現手順・進化・ロードマップ)で格納されている。新しいセッションで全体像を把握させたい場合は「docs を 00 から順に読んで」と指示すれば、実装コードなしで構想全体を復元できる。

5. **現在地とロードマップを確認する**
   [90_roadmap.md](90_roadmap.md) を見て、何が実装済みで何が未実装かを確認する。

6. **次のタスクに着手する**
   ロードマップの優先順位に従い、着手するタスクごとに N-Link canonical pipeline([12_workflow.md](12_workflow.md))を通す。`brain_analyze_task` から必ず始める。

## 再現性の検証チェックリスト

- [ ] `CLAUDE.md` が存在し、絶対ルール1・2が明記されている
- [ ] `docs/00_constitution.md` 〜 `docs/90_roadmap.md` が全て揃っている
- [ ] トップレベルディレクトリ(`skills/ mcp/ brain/ templates/ bootstrap/ spec/ examples/ self-evolution/`)が存在する
- [ ] `self-evolution/VERSION` が読み取れる
- [ ] N-Link 関連フォルダ(`~/.n-link` 等)への参照が「読むな」という文脈以外に存在しない

## このリポジトリに含まれないもの

- N-Link 本体(`n-link-brain` MCP・`~/.n-link` の記憶データ)。これは環境側に別途セットアップされている前提。
- 未実装の Engine の実コード(意図的に段階構築、[90_roadmap.md](90_roadmap.md) 参照)。
- Claude Code 以外のツール向けの実際のアダプタ実装([70_cross_tool_extensibility.md](70_cross_tool_extensibility.md) は方針文書のみ)。
