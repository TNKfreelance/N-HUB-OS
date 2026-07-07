---
schedule: task-driven
risk_tier: 1
status: defined
last_run: 2026-07-07
---

# SecondBrain整合性チェック定期実行

## 目的

`brain/` 全体(research/verified/knowledge_graph.json)の整合性を定期的に確認し、昇格リンク切れ・孤立ノード・孤立エッジを早期発見する。

## トリガー

現時点では task-driven(ユーザーが明示的に依頼した時、または新しいskillを実装した後の節目)。定期cron化(例: 週次)は、実データ量が増えて手動確認が負担になった時点で改めて検討し、ユーザーの明示承認を得てから有効化する(現時点では有効化しない)。

## 処理内容

`skills/secondbrain/SKILL.md` の手順をそのまま実行する。

## 失敗時の挙動

整合性チェックで問題が見つかった場合は `brain_record_failure` で記録し、SecondBrain skillの守るべき制約の範囲でその場修正するか、範囲外ならユーザーに報告する。

## 実行履歴

- 2026-07-07: 手動実行(SecondBrain skill実装時の実地機能テスト)。全項目「問題なし」。
