---
name: n-hub-publisher
description: Runs the pre-publish checklist and approval gate before any N-HUB-OS content or the repository itself is published externally (note, GitHub, SNS), and records what was published in articles/publish_log.md. Use this whenever the user asks to publish, post, push to GitHub, or "公開して"/"投稿して" something from N-HUB-OS. Do not use this to draft content (Writer skill's job) and never treat this skill's checklist pass as a substitute for the owner's explicit final go/no-go -- publishing always requires the owner's explicit approval regardless of checklist result.
---

# N-HUB-OS Publisher Skill

## 目的

承認済み成果物を外部チャネル(note/GitHub/SNSなど)へ公開する前のチェックと承認ゲートを担う。正本は `docs/27_publishing_engine.md`。

## 公開前チェックリスト(docs/27_publishing_engine.mdより)

- [ ] 引用・参照元が明記されているか(著作権配慮)
- [ ] 機密情報・個人情報が含まれていないか
- [ ] `brain/verified/` の裏取りが済んだ内容のみを根拠にしているか
- [ ] `brain_approval_check` を実行し、リスクtierを確認したか

## 承認フロー

公開は原則tier2以上として扱う。`brain_approval_check`の結果に関わらず、**最終的な「公開する/しない」の判断は必ずオーナーの明示承認を得る**(N-Link Hard invariant 3: 「The user decides」)。チェックリストが全て通っても、それは公開してよいという意味ではなく、公開判断をオーナーに仰ぐための準備が整ったという意味でしかない。

## 手順

1. 公開対象(記事、リポジトリ全体など)に対して上記チェックリストを実行する。
2. `brain_approval_check` でリスクtierを確認する。
3. チェック結果をオーナーに提示し、明示的な公開承認を得る。
4. 承認を得て実際に公開した場合のみ、`articles/publish_log.md` に記録する(承認前や公開見送りの場合は記録しない)。

## 出力フォーマット

`articles/publish_log.md`:

```markdown
| 日付 | チャネル | 対象 | 承認者 |
|---|---|---|---|
```

## 守るべき制約

- 書き込み先は `articles/publish_log.md` のみ。
- オーナーの明示承認なしに公開操作(実際の投稿・push等)を実行しない。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
