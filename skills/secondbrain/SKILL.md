---
name: n-hub-secondbrain
description: Runs a whole-Brain integrity check across N-HUB-OS/brain/research/, N-HUB-OS/brain/verified/, and N-HUB-OS/brain/knowledge_graph.json together (cross-file consistency, orphan detection, stale/superseded entries) and owns moving entries into N-HUB-OS/brain/archive/. Use this whenever the user asks to audit, clean up, check the health of, or "整理して"/"整合性チェックして" the whole N-HUB-OS knowledge base, or explicitly says "N-HUB-OS SecondBrain". Do not use this for promoting a single research note (Verification skill's job), do not use this for relating two already-verified entries to each other (Knowledge skill's job), and do not use this to collect new information (Research skill's job) -- this skill only looks at what already exists across all three stores together.
---

# N-HUB-OS SecondBrain Skill

## 目的

`N-HUB-OS/brain/` 全体(`research/` + `verified/` + `knowledge_graph.json`)を横断してチェックし、個々のskill(Research/Verification/Knowledge)が見ない「ストア間の整合性」を担保する。正本は `docs/11_brain.md` と `docs/23_skill_engine.md`(SecondBrain行)。

**他skillとの役割分担**: Research/Verification/Knowledgeはそれぞれ自分が書き込むファイルの内部整合性(frontmatterが正しいか等)には責任を持つが、ストアをまたいだ整合性(例: 昇格済みとマークされた research ノートに対応する verified ファイルが本当に存在するか)までは見ない。SecondBrainはその横断チェックと、`brain/archive/` への移動(アーカイブ運用)を担う。

## チェック項目

1. **昇格リンク切れ**: `brain/research/` の `status: promoted` なファイルすべてについて、本文の `## Verification` セクションが指す `brain/verified/` ファイルが実在するか。
2. **ノード欠落・孤立ノード**: `brain/knowledge_graph.json` の `nodes` と `brain/verified/` の実ファイル(拡張子を除いたファイル名 = `id`)が1:1で対応しているか(ファイルはあるがノードがない/ノードはあるがファイルがない、をどちらも検出する)。
3. **孤立エッジ**: `edges` の `from`/`to` が両方とも実在するノードを指しているか。
4. **未検証の放置**: `brain/research/` に `status: unverified` のまま長期間(目安: 検証を一度も試みていない)残っているものがないか(件数のみ報告。削除・昇格の判断はこのskillの範囲外)。
5. **重複の見落とし**: Research/Verificationのdedupをすり抜けた可能性のある重複(同一URLや酷似タイトルが `research/` と `verified/` に跨って存在する等)がないか、念のため確認する(一次的なdedup責任は各skillにあり、これは安全網)。
6. **アーカイブ候補**: `brain/verified/` の中で、`docs/11_brain.md` が定義する条件(verified_dateから著しく時間が経ち、かつKnowledge skillが`supersedes`エッジで否定している)に該当するものがあるか。

## 手順

1. `brain/research/`・`brain/verified/`・`brain/knowledge_graph.json` を全て読み込む。
2. 上記チェック項目を順に実行し、結果を記録する。
3. アーカイブ候補が見つかった場合のみ、`brain/archive/`(なければ作成する)に該当ファイルを移動し、移動元だった場所には移動先を示す一行だけを残さず、移動先ファイル自身の `## 変更履歴` に「アーカイブされた日付・理由」を追記する。
4. 整合性レポートをユーザーに直接報告する(専用の保存ファイルは作らない。過剰実装回避)。問題がなければ「問題なし」の一言で終えてよい。
5. 修正が必要な軽微な不整合(frontmatterのタイプミス等)を見つけた場合は、該当ファイルのみを直接修正してよい。ただし本文の実質的内容は書き換えない。

## 出力フォーマット

```markdown
## Brain 整合性レポート(<date>)
- 昇格リンク切れ: <件数>件
- ノード欠落/孤立: <件数>件
- 孤立エッジ: <件数>件
- 未検証放置: <件数>件
- 重複の疑い: <件数>件
- アーカイブ実施: <件数>件(詳細)
```

## 守るべき制約

- 書き込み先は `brain/research/`・`brain/verified/`・`brain/knowledge_graph.json`・`brain/archive/` のみ。
- 他skillが書いた本文(`## 結論` `## 根拠` `## 実用上の示唆`)を書き換えない。frontmatterと`## 変更履歴`、アーカイブ移動のみが対象。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
- 昇格判断(Verificationの仕事)や関連性判断(Knowledgeの仕事)を代わりに行わない。このskillは「すでにある状態が矛盾していないか」だけを見る。
