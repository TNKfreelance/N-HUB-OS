---
name: n-hub-analytics
description: Analyzes usage/feedback data from published N-HUB-OS content and feeds insights back into brain/verified/ notes and the source-priority ordering in docs/02_principles.md. Use this whenever the user asks to analyze usage, engagement, or feedback on published N-HUB-OS content, or explicitly says "N-HUB-OS Analytics". Do not use this if nothing has been published yet -- there is no usage data to analyze until Publisher skill has actually published something and real engagement data exists.
---

# N-HUB-OS Analytics Skill

## 目的

公開済み成果物の利用実績・フィードバックを分析し、`brain/verified/` エントリへの注記や `docs/02_principles.md` の情報源優先順位見直しへフィードバックする。正本は `docs/28_analytics_engine.md`。

## 前提条件

このスキルは `articles/publish_log.md` に公開実績が存在することを前提とする。公開実績がまだ無い場合は、分析対象データが存在しないため「分析対象なし」と正直に報告し、架空のデータを作らない。

## 手順

1. `articles/publish_log.md` を確認し、公開実績があるか確認する。
2. 公開実績がある場合、その利用実績・フィードバックデータ(取得元は都度確認する。現時点で自動収集の仕組みは無い)を確認する。
3. 実績データがあれば、関連する `brain/verified/*.md` に注記を追加し、`docs/02_principles.md` の優先順位見直しを提案する。
4. 公開実績が無い場合は、その旨を報告して終了する(架空の分析結果を作らない)。

## 出力フォーマット

分析結果がある場合、対象の `brain/verified/*.md` の `## 実用上の示唆` セクションに、日付付きで利用実績の要点を追記する(既存内容を上書きしない)。

## 守るべき制約

- 実際のデータが存在しない状態で分析結果を捏造しない。
- 書き込み先は `brain/verified/*.md` の該当セクション追記と `docs/02_principles.md` の見直し提案のみ。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
