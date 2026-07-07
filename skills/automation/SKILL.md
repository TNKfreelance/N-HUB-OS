---
name: n-hub-automation
description: Defines and records automation workflow specs (schedule, risk tier, what it runs) under automation/, for low-risk, already-approved, repeatable tasks like periodic SecondBrain integrity checks. Use this whenever the user asks to automate, schedule, or "定期的に実行して"/"自動化して" a repeatable N-HUB-OS task. Do not use this to actually activate a live cron job or scheduled task without the user's explicit separate approval, and do not use this for anything that publishes externally, spends money, or is irreversible (those always need tier3 owner approval regardless of this skill).
---

# N-HUB-OS Automation Skill

## 目的

定型的・低リスクな繰り返しタスクをワークフロー定義として `automation/` に記録する。正本は `docs/25_automation_engine.md`。

## 自動化してよいもの/いけないもの

`docs/25_automation_engine.md` の基準をそのまま適用する: 低リスク(tier1〜2)かつ既に人間が承認済みの繰り返しタスクのみ。外部公開・送信、金銭・契約・不可逆操作は対象外(常にオーナー承認が必要)。

## 手順

1. 自動化候補のタスクを特定し、`brain_approval_check` でリスクtierを確認する。
2. `automation/<name>.md` にワークフロー定義を記述する(下記フォーマット)。
3. **定義を作るだけでは実際のスケジュール実行を開始しない。** `scheduled-tasks` MCPや`CronCreate`で実際に有効化する場合は、必ずユーザーに明示確認を取ってから行う(このスキル自身が無断で有効化しない)。
4. 実行結果は当該ワークフロー定義ファイルに追記して記録する。

## 出力フォーマット

`automation/<name>.md`:

```markdown
---
schedule: <cron式 または "task-driven">
risk_tier: 1|2|3
status: defined|active|paused
last_run:
---

# <ワークフロー名>

## 目的
## トリガー
## 処理内容
## 失敗時の挙動
```

## 守るべき制約

- 書き込み先は `automation/` のみ。
- ワークフロー定義を作ることと、実際にスケジュール実行を有効化することは別の行為として扱う。後者は必ずユーザーの明示承認を経る。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
