# 12. Workflow

## 標準タスクフロー

N-HUB-OS 内でのすべての実装タスクは、[CLAUDE.md](../CLAUDE.md) の絶対ルール1に従い、N-Link の canonical pipeline に乗せる。

```
1. brain_context_resume          セッション開始時に直近の記憶を取得
2. brain_analyze_task(task)      着手前に必ず実行。真意・推奨skill・過去の失敗を取得
3. リスク・規模に応じて分岐:
   a. 軽量(Q&A・小さい修正・低リスク)
      -> 実装 -> brain_evaluate_quality -> brain_record_success / brain_remember
   b. 本実装(新しい Engine・Skill・複数ファイルにまたがる変更)
      -> brain_deploy_plan -> brain_alignment_meeting(オーナー承認 = user_gate)
      -> 承認された範囲のみ実装(build -> verify -> fix loop)
      -> 独立監査 brain_evaluate_council(自己採点しない)
      -> オーナー承認 -> brain_record_success / brain_remember
4. 副作用のある操作(削除・外部送信・公開・課金・不可逆操作)の前には
   必ず brain_approval_check を呼ぶ。tier3 は常にオーナー承認必須。
```

## Engine 別の入出力フロー

```
Research Engine
  入力: 収集対象キーワード/カテゴリ(02_principles.md の優先順位に従う)
  出力: brain/research/<date>_<source>_<slug>.md

Verification Engine
  入力: brain/research/ の未検証エントリ
  出力: 昇格したものは brain/verified/ へ、却下したものは research 側に理由を追記して残す

Knowledge Engine
  入力: brain/verified/ の新規・更新エントリ
  出力: brain/knowledge_graph.json のノード/エッジ更新

Skill Engine / MCP Engine / Automation Engine / Writer Engine
  入力: brain/verified/ の知見 + ユーザーからの明示的な生産依頼
  出力: skills/ , mcp/ , templates/ 配下の成果物、および各Engine未実装分は実装時に保存先を確定
        (各生成は 23_skill_engine.md / 24_mcp_engine.md / 25_automation_engine.md / 26_writer_engine.md の個別仕様に従う)

Publishing Engine
  入力: 生産済み成果物 + オーナー承認(brain_approval_check)
  出力: 外部チャネルへの公開(実行は 27_publishing_engine.md のチェックリストに従う)

Analytics Engine
  入力: 公開後の利用実績・フィードバック
  出力: brain/verified/ への注記、次の収集優先順位への反映
```

## 更新頻度の方針

常時ポーリングやスケジュール実行はデフォルトでは行わない(コスト最適化)。収集・生産はタスク駆動(ユーザーの依頼または明示的にスケジュールされたタスク)を基本とし、定期実行が必要な場合のみ `scheduled-tasks` / `CronCreate` を個別に検討し、`brain_approval_check` でゲートする。
