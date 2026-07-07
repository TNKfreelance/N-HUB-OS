# Brain(N-HUB-OS Second Brain)

**注意: これは N-Link の脳(`~/.n-link`, `n-link-brain` MCP)とは別物。** N-HUB-OS 自身の知識ストア(収集物・検証済み知識・知識グラフ)であり、N-Link のフォルダには一切書き込まない。両者を混同しないこと([CLAUDE.md](../CLAUDE.md) 絶対ルール2/3、[docs/00_constitution.md](../docs/00_constitution.md) 参照)。

## 構成

- `research/` — 未検証の収集物。保存形式は [docs/20_research_engine.md](../docs/20_research_engine.md)
- `verified/` — 検証済み知識。保存形式は [docs/11_brain.md](../docs/11_brain.md)
- `knowledge_graph.json` — 検証済み知識間の関連を保持する軽量グラフ
- `archive/` — 陳腐化・supersededされた知識の退避先(必要になった時点で作成する)

現時点では空(収集実績なし)。Research skill 実装後に運用を開始する。
