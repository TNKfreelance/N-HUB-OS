# 60. Self Evolution

## N-HUB-OS 自身の改善サイクル

N-HUB-OS は N-Link とは異なり、自律的に自分自身のコードを書き換える「自己進化エンジン」は持たない(過剰実装・暴走リスクを避けるため)。改善は以下の人間参加型サイクルで行う:

```
気づき(運用中に見つかった不足・矛盾)
   -> docs/ の該当ドキュメントへの変更提案を作成
   -> brain_analyze_task で影響範囲を確認
   -> 変更が構造に関わる場合は brain_deploy_plan / brain_alignment_meeting でオーナー承認
   -> docs/ を更新 + CHANGELOG.md に記録
   -> バージョンを SemVer でインクリメント(self-evolution/VERSION)
```

## バージョニング

- `self-evolution/VERSION` に現在バージョン(例: `0.1.0`)を保持する。
- `self-evolution/CHANGELOG.md` に変更履歴を追記する(Keep a Changelog 形式に準拠)。
- 破壊的変更(既存ルールの撤回・ディレクトリ構造の変更)は MAJOR、仕様追加は MINOR、誤字修正等は PATCH。

## Pull Request 運用(GitHub 化した場合)

N-HUB-OS を GitHub リポジトリとして運用する場合、Specification の変更は PR ベースで行い、オーナーレビューを経てマージする。N-HUB-OS 自身が自分の PR を自動マージすることはない。

## 学習の記録

改善が完了したら `brain_record_success` / `brain_remember`(category=decision）で N-Link に記録し、同種の改善提案が将来再度出た際に過去の判断を参照できるようにする。
