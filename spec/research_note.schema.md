# Schema: research note (`brain/research/*.md`)

物語的な説明は [docs/20_research_engine.md](../docs/20_research_engine.md) を参照。ここでは frontmatter のキーのみを機械可読的に定義する。

```yaml
source: github|reddit|hackernews|x|youtube|producthunt|medium|devto|official   # required, enum
source_url: string (URL)                                                       # required
collected_date: string (YYYY-MM-DD)                                            # required
category: string                                                               # required, docs/01_vision.md の対象領域から1つ以上
status: unverified|promoted                                                    # required
```

本文セクション(固定、[templates/research_note.md](../templates/research_note.md) のテンプレートに準拠):
`# <タイトル>` → `## 要約` → `## 元情報からの引用・根拠` → `## 再現性メモ` → (任意) `## Updates` → (昇格後のみ) `## Verification`
