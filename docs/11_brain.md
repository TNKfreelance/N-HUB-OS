# 11. Brain (Second Brain & Knowledge Graph)

## Second Brain の保存形式

`brain/verified/<slug>.md`

```markdown
---
title: <知識のタイトル>
category: <01_vision.md の対象領域>
source_urls:
  - <裏取りに使った1つ目のURL>
  - <裏取りに使った2つ目のURL>
verified_date: <YYYY-MM-DD>
confidence: high|medium
version: 1
related_ids:
  - <他の verified エントリの slug>
---

# <タイトル>

## 結論(何が分かったか)

## 根拠(複数ソースの裏取り内容)

## 実用上の示唆(何に使えるか、どの Skill/成果物に繋がるか)

## 変更履歴
- v1 <date> 初版
```

## Knowledge Graph

`brain/knowledge_graph.json` に軽量なノード/エッジ構造で保持する。専用グラフDBは導入しない(過剰実装回避)。

```json
{
  "nodes": [
    {"id": "<slug>", "title": "<タイトル>", "category": "<category>"}
  ],
  "edges": [
    {"from": "<slug-a>", "to": "<slug-b>", "relation": "related|supersedes|depends_on"}
  ]
}
```

- ノードは `brain/verified/` の各エントリと 1:1 対応させる。
- エッジは Knowledge Engine がエントリ追加・更新時に手動または半自動で追記する。自動生成の全文embedding検索などは、実需要が出るまで導入しない。

## 更新方法

- 既存エントリを更新する場合は `version` をインクリメントし、`## 変更履歴` に追記する。上書きによる履歴消失を禁止する。
- ある知識が古くなった(verified_date から著しく時間が経ち、かつ新情報で否定された)場合は削除せず、`confidence` を下げるか `## 変更履歴` に「supersededされた」旨を記録し、`brain/archive/` へ移動する運用とする(`brain/archive/` は必要になった時点で作成する)。

## 重複排除

- 新規知識を `brain/verified/` に追加する前に、`knowledge_graph.json` のノード一覧と `brain/verified/` のタイトルを検索し、既存エントリの更新で済むかを必ず確認する。
