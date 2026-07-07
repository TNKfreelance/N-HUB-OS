---
name: n-hub-writer
description: Turns already-verified knowledge in brain/verified/ into human-readable content drafts (articles, note-style write-ups, video scripts) saved under articles/. Use this whenever the user asks to write, draft, summarize into an article, or "記事にして"/"note用に書いて" the verified knowledge base, or explicitly says "N-HUB-OS Writer". Do not use this to collect new information (Research skill), verify claims (Verification skill), manage knowledge relationships (Knowledge skill), or actually publish/send anything externally (Publisher skill's job) -- this skill only produces a draft file, it never sends or posts anything.
---

# N-HUB-OS Writer Skill

## 目的

`brain/verified/` の検証済み知識から、記事・note原稿・動画台本などの人間向けコンテンツ下書きを作る。正本は `docs/26_writer_engine.md`。このスキルは**下書きを作るところまで**が範囲で、公開・投稿は行わない(Publisher skillの仕事)。

## 手順

1. 対象の検証済み知識(`brain/verified/*.md`)を1件以上選ぶ。裏取りされていない主張を新たに追加しない(`brain/verified/`にある内容だけを根拠にする)。
2. `templates/article.md` のフォーマットに従い、`articles/<slug>.md` を作成する(`articles/`が無ければ作成する)。
3. 元となった検証済み知識のIDを frontmatter の `source_ids` に記録する(トレーサビリティ確保)。
4. 断定的な表現は `brain/verified/` の `confidence` が `high` のものに限定し、`medium` のものは「〜とされる」等の留保表現を使う。
5. 下書きが完成したら、公開が必要な場合は Publisher skill に引き継ぐ旨をユーザーに伝える(このスキル自身は公開しない)。

## 出力フォーマット

`templates/article.md` を使用する:

```markdown
---
title: <記事タイトル>
category: <対象領域>
source_ids: [<brain/verified/のファイル名(拡張子除く)>]
draft_date: <YYYY-MM-DD>
status: draft
---

# <タイトル>

## リード文

## 本文

## 参考(根拠となった検証済み知識)
```

## 守るべき制約

- 書き込み先は `articles/` のみ。
- `brain/verified/` にない主張を新規に追加しない(このスキルは「知識の言い換え・構成」担当であり、新しい調査は行わない)。
- 公開・投稿・外部送信は一切行わない(Publisher skillに引き継ぐ)。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
