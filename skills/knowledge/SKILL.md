---
name: n-hub-knowledge
description: Reviews the relationships between already-verified knowledge entries in N-HUB-OS/brain/verified/ and keeps N-HUB-OS/brain/knowledge_graph.json (and each verified file's related_ids frontmatter) in sync and correctly classified as related, supersedes, or depends_on. Use this whenever the user asks to organize, connect, relate, restructure, or "整理して"/"関連付けて" the verified knowledge base, or explicitly says "N-HUB-OS Knowledge". Do not use this to collect new information (that is the Research skill), do not use this to decide whether an unverified note should be promoted (that is the Verification skill), and do not use this to archive or delete old knowledge (archival is out of scope for this skill).
---

# N-HUB-OS Knowledge Skill

## 目的

`N-HUB-OS/brain/verified/` にすでに存在する検証済みエントリ同士の関係性を見直し、`N-HUB-OS/brain/knowledge_graph.json` のエッジと各ファイルの `related_ids` frontmatter を正しく同期させる。正本は N-HUB-OS リポジトリの `docs/11_brain.md`(Knowledge Graph仕様)と `docs/23_skill_engine.md`(Knowledge行: 入力=`brain/verified/*.md`、出力=`brain/knowledge_graph.json`)。矛盾があればそちらを正とする。

**Verification skillとの役割分担**: Verification skillは研究ノートを検証済みへ昇格させる「その瞬間」に最初のノード・エッジを追加する(最小限)。Knowledge skillはその後、`brain/verified/`にすでにあるエントリ同士を見直し、関係性の精査・修正・同期を担う。昇格判断そのものはこのスキルの範囲外。

## 関連の種類(relation types)

`docs/11_brain.md`で定義される3種類を、アルゴリズムではなく実際に本文を読んだ上での判断で使い分ける(全文embedding検索などの新しい仕組みは導入しない — `docs/00_constitution.md`原則3):

- **related**: 話題として関連するが、互いを前提にはしていない(同じ分野の別トピック)
- **supersedes**: 新しいエントリが古いエントリの結論を置き換える・古くする
- **depends_on**: 片方を理解するにはもう片方の理解が前提になる

## 手順

1. `N-HUB-OS/brain/verified/` の全ファイルを列挙する。
2. `N-HUB-OS/brain/knowledge_graph.json` の `nodes` と突き合わせ、ファイルとノードが1:1で対応しているか確認する(欠けているノードがあれば追加する)。
3. エントリのペアごとに、両方の本文(`## 結論` `## 根拠`)を実際に読み、関連の種類(上記)を判断する。既存エッジがあれば分類が今も正しいか再確認し、必要なら修正する。
4. 判断結果を `knowledge_graph.json` の `edges` に反映する(新規追加・分類修正・重複エッジの整理)。
5. エッジを追加・変更した場合は、影響する両方の `.md` ファイルの `related_ids` frontmatter を実際のエッジと一致するように更新する。これは内容変更にあたるため、`version` を1つ上げ、`## 変更履歴` に日付付きで一行追記する(履歴を上書きしない、`docs/11_brain.md`の原則)。
6. `knowledge_graph.json` が引き続き妥当なJSONであることを確認する。
7. 何を変更した(または「既存の分類は正しかったため変更なし」)かをユーザーに簡潔に報告する。

## 出力フォーマット

`knowledge_graph.json` のエッジ:

```json
{"from": "<slug>", "to": "<slug>", "relation": "related|supersedes|depends_on"}
```

`.md`ファイルの変更履歴への追記:

```markdown
- v<N> <YYYY-MM-DD> <何を変更したか(例: knowledge_graph.jsonのエッジとrelated_idsを同期)>
```

## 守るべき制約

- 書き込み先は `N-HUB-OS/brain/knowledge_graph.json` と、`N-HUB-OS/brain/verified/*.md` の frontmatter(`related_ids`・`version`)および `## 変更履歴` セクションのみ。`## 結論`・`## 根拠`・`## 実用上の示唆` など、他のスキルが書いた本文を書き換えない。
- `N-HUB-OS/brain/archive/` への移動・削除は行わない(範囲外。将来のSecondBrain skillの仕事)。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
- 裏付けのない関連性を作らない。本文を実際に読んで判断できないペアは無理に分類せず、未判定のまま残してよい。
