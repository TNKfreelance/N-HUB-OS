---
source: github
source_url: https://github.com/anthropics/claude-code/releases
collected_date: 2026-07-07
category: Claude Code
status: promoted
---

# Claude Code 直近リリース(v2.1.196〜v2.1.202)の要点

## 要約

Claude Code は2026年6月末〜7月頭にかけて短いサイクルでリリースを重ねている。主な変化:

- **Claude Sonnet 5がデフォルトモデルに**(v2.1.197、2026-06-30): 1Mトークンのネイティブコンテキストウィンドウを持つ。2026年8月31日まで $2/$10 per Mtokのプロモーション価格。
- **サブエージェントがデフォルトでバックグラウンド実行に**(v2.1.198、2026-07-01)。バックグラウンドエージェントは完了時に自動でcommit・push・draft PR作成まで行う。
- **組織デフォルトモデル対応**(v2.1.196、2026-06-29): 管理者が組織コンソールで設定でき、ユーザーが未選択の場合`/model`に「Org default」と表示される。
- **AskUserQuestionダイアログの挙動変更**(v2.1.200、2026-07-03): デフォルトで自動継続しなくなった。デフォルト権限モードも「Manual」に変更。
- **スタック形式のslash-skill呼び出し対応**(v2.1.199、2026-07-02): `/skill-a /skill-b do XYZ`のように先頭に並べたskillをすべて読み込めるようになった。
- **動的ワークフローサイズ設定の追加**(v2.1.202、2026-07-06、最新): ワークフロー内のエージェント数を制御できる設定。

## 元情報からの引用・根拠

- 出典: [anthropics/claude-code の GitHub Releases ページ](https://github.com/anthropics/claude-code/releases)(公式リポジトリの一次ソース)
- 上記はv2.1.196(2026-06-29)からv2.1.202(2026-07-06、最新)までの各リリースノートを直接確認した内容。

## 再現性メモ(実際に試した場合のみ)

未実施(リリースノートの内容確認のみ。実際に各機能を動かした検証は別タスク)。

## Verification

- 2026-07-07: 本ノートに列挙した6項目のうち、**Sonnet 5デフォルト化とバックグラウンドサブエージェント標準化の2項目のみ**、独立3ソース以上(anthropic.com/news、platform.claude.com/docs、ai-tldr.dev)で裏取りができたため [brain/verified/claude-code-2026-q3-updates.md](../verified/claude-code-2026-q3-updates.md) へ部分昇格。残り4項目(組織デフォルトモデル・AskUserQuestion挙動変更・スタック形式slash-skill・動的ワークフローサイズ)はGitHub単独ソースのままで未検証。裏取りが取れ次第、追って昇格を検討する。
