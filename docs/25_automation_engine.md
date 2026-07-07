# 25. Automation Engine

## 自動化してよいもの

- 定型的な収集・整理作業(例: 特定カテゴリの定期リサーチ、`brain/` の整合性チェック)
- 低リスク(tier1〜2)かつ既に人間が承認済みの繰り返しタスク

## 自動化しないもの(常に人間の承認を要求)

- 外部への公開・送信(Publishing Engine の実行)
- 金銭・契約・不可逆な操作(tier3、`brain_approval_check` が常に必須)
- N-Link / N-HUB-OS の設定変更を伴うもの

## スケジュール実行

定期実行が必要な場合は `scheduled-tasks` MCP または `CronCreate` を使う。導入前に:

1. `brain_analyze_task` でタスクの意図を確認
2. `brain_approval_check` でリスクtierを確認(tier2以上は明示承認を得る)
3. 実行結果を記録し(保存先は実装時に確定)、失敗時は `brain_record_failure` で記録する

## ワークフロー定義の保存形式

保存先は実装時に確定させる(現時点で先取りして仕様化しない)。ファイル形式のみ以下で固定する:

```markdown
---
schedule: <cron式 または "task-driven">
risk_tier: 1|2|3
last_run: <YYYY-MM-DD>
---

# <ワークフロー名>

## 目的
## トリガー
## 処理内容
## 失敗時の挙動
```

## 現状

このリポジトリには自動化ワークフローは未実装。実装は個別の需要が発生してから行う(過剰実装回避)。
