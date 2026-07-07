# Schema: verified knowledge (`brain/verified/*.md`)

物語的な説明は [docs/11_brain.md](../docs/11_brain.md) を参照。ここでは frontmatter のキーのみを機械可読的に定義する。

```yaml
title: string                        # required
category: string                     # required
source_urls: string[] (URL)          # required, 昇格条件を満たす裏取り元。最低1つ、通常2つ以上
verified_date: string (YYYY-MM-DD)   # required
confidence: high|medium              # required, enum
version: integer                     # required, 1始まり。内容変更のたびインクリメント
related_ids: string[]                # required(空配列可)。knowledge_graph.json のノードidと一致させる
```

ファイル名(拡張子除く)は `related_ids` および `knowledge_graph.json` の `id` と必ず一致させる。

本文セクション(固定、[templates/verified_knowledge.md](../templates/verified_knowledge.md) のテンプレートに準拠):
`# <タイトル>` → `## 結論` → `## 根拠` → `## 実用上の示唆` → `## 変更履歴`
