# 90. Roadmap

## 現在地: v1.5.0(10skill実装済み + GitHub公開 + ドキュメントサイト稼働中 + 実運用対象領域をMCP/Claude Code/AI Agentの3領域に拡大)

- GitHubリポジトリ(パブリック): https://github.com/TNKfreelance/N-HUB-OS
- ドキュメントサイト(GitHub Pages、稼働確認済み): https://tnkfreelance.github.io/N-HUB-OS/

このバージョンで完成しているもの:

- [CLAUDE.md](../CLAUDE.md) — 絶対ルール(N-Link経由・N-Linkフォルダ不可侵)
- `docs/00`〜`90` — 構想全容(番号帯の意味はCLAUDE.md参照)
- トップレベルディレクトリ: `docs/ spec/ templates/ bootstrap/ skills/ mcp/ brain/ articles/ automation/ self-evolution/ examples/`
- `docs/50_bootstrap.md` — 再現手順
- Research / Verification / Knowledge / SkillBuilder / SecondBrain / MCPBuilder / Writer / Automation / Publisher / Analytics の10skillすべて実装・実地テスト・独立監査済み
- GitHubをSecond Brainの実際の保管庫として稼働(実データをpush済み)
- `docs/`から生成したドキュメントサイトをGitHub Pagesで実際に公開・稼働確認済み(構想文のタグライン反映済み)
- 対象領域をMCPから「Claude Code」へ拡大し、Research→Verification→Knowledge→Writerのループを実データで再実行(下記マイルストーン13参照)

このバージョンで**意図的に未実装**のもの(段階的構築、[00_constitution.md](00_constitution.md) 原則3):

- MCP サーバーの実導入(現時点で `mcp/registry.md` に導入済みのMCPはN-Link本体のみ。候補評価は実施済み、下記参照)
- 自動化ワークフローの実際のスケジュール有効化(定義のみ完了、有効化はオーナー承認待ち)

## 実装済みマイルストーン

1. **Research skill** — [skills/research/SKILL.md](../skills/research/SKILL.md)(2026-07-07)。実際にWebSearch/WebFetchで稼働させ、`brain/research/` に2件の実データを収集。重複排除ロジックも実地で確認。過程で見つかった引用の誤帰属バグ(存在しない一次ソースへの誤引用)を検出・修正済み。
2. **Verification skill** — [skills/verification/SKILL.md](../skills/verification/SKILL.md)(2026-07-07)。Research skillが集めた2件の未検証ノートを実際に裏取りし、両方とも `brain/verified/` へ昇格(1件は独立3ソースの一致、1件はレジストリAPIへの実アクセスによる再現確認で昇格条件を満たした)。
3. **Knowledge skill** — [skills/knowledge/SKILL.md](../skills/knowledge/SKILL.md)(2026-07-07)。Verification skillが昇格時に追加した`related`エッジの分類を実際に本文を読んで再確認(正しいと判断)し、両方の検証済みファイルの`related_ids`をエッジと同期。versionを上げ変更履歴に記録。
4. **SkillBuilder skill** — [skills/skillbuilder/SKILL.md](../skills/skillbuilder/SKILL.md)(2026-07-07)。3つの既存skillから抽出した規約(命名・セクション構成・N-Linkブラックリスト)を定義し、実際に3skillへ規約チェックを実行(byte-for-byte比較を含む)。ドリフトはゼロ件だった。
5. **SecondBrain skill** — [skills/secondbrain/SKILL.md](../skills/secondbrain/SKILL.md)(2026-07-07)。`brain/research/`・`brain/verified/`・`knowledge_graph.json`を横断する6項目の整合性チェックを実データに対して実行(昇格リンク切れ・ノード欠落・孤立エッジ・未検証放置・重複見落とし・アーカイブ候補)。全項目「問題なし」。
6. **N-HUB → N-HUB-OS 再構成**(2026-07-07)。オーナー提示の3案を統合した構造へ全面リネーム・再編。実データ(brain/の2研究ノート・2検証済みエントリ・5skill)は一切失わずに移行。詳細は [self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) の v1.0.0 エントリ。
7. **MCPBuilder skill** — [skills/mcpbuilder/SKILL.md](../skills/mcpbuilder/SKILL.md)(2026-07-07)。実際に`github/github-mcp-server`を4基準で評価し、`mcp/registry.md`に登録。Research skillの現需要はWebSearch/WebFetchで足りるため「却下」と正直に判断(導入すること自体が目的化しないよう、過剰実装回避の原則を実地で適用した)。
8. **Writer skill** — [skills/writer/SKILL.md](../skills/writer/SKILL.md)(2026-07-07)。実際に2件の検証済み知識(MCP仕様・レジストリ)から記事下書き[articles/mcp-2026-latest-updates.md](../articles/mcp-2026-latest-updates.md)を作成。新規の未検証情報は追加せず`brain/verified/`の内容のみを根拠にした。
9. **Automation skill** — [skills/automation/SKILL.md](../skills/automation/SKILL.md)(2026-07-07)。SecondBrain整合性チェックの定期実行ワークフロー定義[automation/secondbrain-integrity-check.md](../automation/secondbrain-integrity-check.md)を作成。実際のスケジュール有効化は行わず「defined」ステータスに留め、有効化にはオーナー承認が必要である旨を明記。
10. **Publisher skill** — [skills/publisher/SKILL.md](../skills/publisher/SKILL.md)(2026-07-07)。公開前チェックリストを実際にN-HUB-OSリポジトリ全体(GitHub公開予定)に対して適用(引用元明記・機密情報スキャン・裏取り根拠の確認)。公開自体はオーナーの明示承認を経てから実施(下記参照)。
11. **Analytics skill** — [skills/analytics/SKILL.md](../skills/analytics/SKILL.md)(2026-07-07)。実際に`articles/publish_log.md`の有無を確認したところ公開実績が存在しなかったため、「分析対象なし」と正直に報告(架空のデータを作らなかった)。
12. **GitHubへの実公開 + ドキュメントサイト稼働**(2026-07-07)。`git init`からプライベートリポジトリ作成・push、その後GitHub Pagesがプライベートリポジトリの無料プランでは使えないという実際の制約に当たったためオーナーに選択肢を提示し、パブリックへの切り替えとPages有効化の承認を得た。実際にPagesのビルドステータスが`built`になり、トップページと個別ページの両方がHTMLとして正しくレンダリングされることをWebFetchで確認済み。詳細は [self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) の v1.3.0 エントリ。
13. **実運用の対象領域拡大(Claude Code)**(2026-07-07)。MCP以外の初めての実運用対象として、Research→Verification→Knowledge→Writerのループを「Claude Code」で実行。GitHub Releasesから6項目を収集したが、独立裏取りできたのは2項目(Sonnet 5デフォルト化・バックグラウンドサブエージェント標準化)のみだったため、その2項目だけを正直に検証済みへ昇格し記事化。残り4項目は単独ソースのまま未検証で保持した。詳細は [self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) の v1.4.0 エントリ。
14. **実運用の対象領域拡大(AI Agent)**(2026-07-07)。GoogleのGemini CLIがMCPに対応していることをGitHub公式リポジトリ+Google Cloud公式ドキュメントの独立2ソースで確認し検証済みへ昇格。この発見を[docs/70_cross_tool_extensibility.md](70_cross_tool_extensibility)に反映(Skill仕様レベルの互換性は依然未検証と明記)。knowledge_graph.jsonに根拠のある`related`エッジ(MCP仕様ノードとの関連)を追加。詳細は [self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) の v1.5.0 エントリ。

いずれも skill-creator のガイドに沿って作成。低リスク・仕様が明確なタスクのため、フルの eval/ベンチマークループは省略し、独立監査官によるレビューで代替した([self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) 参照)。

## 次のマイルストーン候補(優先順位順、あくまで目安)

1. 実運用の対象領域をさらに拡大する(Browser Automation / AI Coding / AI SaaS / Immersive Web など、[01_vision.md](01_vision.md) の残りの対象領域を順次)
2. MCP サーバーの実導入(必要が生じた時点で MCPBuilder skill を使って再評価)

## 進め方

各マイルストーンは個別タスクとして必ず `brain_analyze_task` から開始し、規模に応じて `brain_deploy_plan` -> `brain_alignment_meeting`(オーナー承認)-> 実装 -> `brain_evaluate_council` の canonical pipeline を通す。まとめて一括実装しない。
