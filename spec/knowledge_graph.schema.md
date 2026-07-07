# Schema: `brain/knowledge_graph.json`

物語的な説明は [docs/11_brain.md](../docs/11_brain.md) と [docs/22_knowledge_engine.md](../docs/22_knowledge_engine.md) を参照。

```json
{
  "nodes": [
    {"id": "string (verified/配下のファイル名と一致)", "title": "string", "category": "string"}
  ],
  "edges": [
    {"from": "string (既存node id)", "to": "string (既存node id)", "relation": "related|supersedes|depends_on"}
  ]
}
```

制約:
- `nodes[].id` は `brain/verified/<id>.md` として実在しなければならない(孤立ノード禁止)。
- `edges[].from` / `edges[].to` は両方とも `nodes[].id` に存在しなければならない(孤立エッジ禁止)。
- 整合性チェックは [skills/secondbrain/SKILL.md](../skills/secondbrain/SKILL.md) が担う。
