# 22. Knowledge Engine

## 目的

すでに `brain/verified/` に存在する検証済みエントリ同士の関係性(`related`/`supersedes`/`depends_on`)を見直し、`brain/knowledge_graph.json` と各ファイルの `related_ids` frontmatter を同期させる。実装は [skills/knowledge/SKILL.md](../skills/knowledge/SKILL.md)(Claude Code Skill、実地テスト・独立監査済み)。

## Verification Engineとの役割分担

Verification Engineは研究ノートを検証済みへ昇格させる瞬間に最小限のノード・エッジを追加する。Knowledge Engineはその後、既存エントリ同士を横断的に見直し、関係性の精査・修正・同期を担う。昇格判断そのものはKnowledge Engineの範囲外([21_verification_engine.md](21_verification_engine.md) 参照)。

## 関連の種類

- **related**: 話題として関連するが、互いを前提にはしていない
- **supersedes**: 新しいエントリが古いエントリの結論を置き換える
- **depends_on**: 片方を理解するにはもう片方の理解が前提になる

判断はアルゴリズム(embedding検索等)ではなく、実際に本文を読んだ上で行う([00_constitution.md](00_constitution.md) 原則3: 過剰実装を避ける)。

## 入力・出力

- 入力: `brain/verified/*.md`、`brain/knowledge_graph.json`
- 出力: `brain/knowledge_graph.json` の更新、影響する `.md` ファイルの `related_ids`・`version`・`## 変更履歴` の更新

## 保存形式

[11_brain.md](11_brain.md) を参照。

## 実績

2026-07-07時点で実データ2件間の`related`エッジを実際に本文照合の上で確認・同期した実績あり。詳細は [../self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) の v0.4.0 を参照。
