---
name: n-hub-verification
description: Reviews unverified research notes in N-HUB-OS/brain/research/ and decides whether to promote each one to N-HUB-OS/brain/verified/ (the Second Brain) by independently re-checking claims against a second source or hands-on reproduction. Use this whenever the user asks to verify, double-check, fact-check, promote, or "確認して"/"検証して" the collected research notes, or explicitly says "N-HUB-OS Verification". Do not use this to collect new information (that is the Research skill) and do not use it for topics that have no existing note under brain/research/.
---

# N-HUB-OS Verification Skill

## 目的

`N-HUB-OS/brain/research/` にある未検証ノート(`status: unverified`)を、実際に裏取りした上で `N-HUB-OS/brain/verified/` へ昇格させるかどうかを判断する。判断基準の正本は N-HUB-OS リポジトリの `docs/02_principles.md`(昇格条件)と `docs/11_brain.md`(保存形式)。矛盾があればそちらを正とする。

## 昇格条件(docs/02_principles.mdより)

以下をすべて満たすもののみ昇格させる:

1. **独立した2ソース以上で同じ主張が確認できる**、または**実際に手元で再現確認ができた**(例: 該当サービスに実際にアクセスして稼働を確認する)
2. 情報の鮮度(いつの情報か)が記録できている
3. 実用性(実際に何かを作る・判断する際に使える)がある

これらを満たさない場合は昇格させず、元の research ノートに理由を記録して未検証のまま残す(削除しない)。

## 手順

1. `N-HUB-OS/brain/research/` から `status: unverified` のノートを1件選ぶ。
2. ノートの `source_url` を `WebFetch` で再取得し、主張が実際にそこに書かれているか再確認する(Research skillの誤引用を再度拾うための二重チェック)。
3. 昇格条件1を満たすため、以下のいずれかを行う:
   - 独立した別ソース(異なるドメイン)を `WebSearch` で探し、同じ主張を裏付ける記述があるか確認する。
   - サービス・リポジトリ等が対象の場合は、実際にそのURL・APIにアクセスして稼働状況を再現確認する。
4. 条件を満たせば、`docs/11_brain.md` のフォーマットで `N-HUB-OS/brain/verified/<slug>.md` を新規作成する。`source_urls` には元の research ノートの `source_url` と、裏取りに使った2つ目のソースを両方記載する。
5. 昇格させたら、元の research ノートの frontmatter に `status: promoted` を設定し、本文末尾に `## Verification` セクションを追記して昇格先ファイルへのリンクと昇格日を記録する(research ノート自体は履歴として残す。削除しない)。
6. 条件を満たさない場合は昇格させず、research ノートに `## Verification memo` セクションを追記し、確認した内容・不十分だった理由・再確認すべき時期を記録する。`status` は `unverified` のまま。
7. 昇格させた場合は `N-HUB-OS/brain/knowledge_graph.json` にノードを追加する(`id` は verified ファイルの slug、`title`、`category`)。関連する既存ノードがあれば `edges` にも追記する。

## 出力フォーマット(brain/verified/<slug>.md)

```markdown
---
title: <知識のタイトル>
category: <対象領域>
source_urls:
  - <一次ソースURL>
  - <裏取りに使った2つ目のURL>
verified_date: <YYYY-MM-DD>
confidence: high|medium
version: 1
related_ids: []
---

# <タイトル>

## 結論(何が分かったか)

## 根拠(複数ソースの裏取り内容)

## 実用上の示唆(何に使えるか、どの Skill/成果物に繋がるか)

## 変更履歴
- v1 <date> 初版
```

## 守るべき制約

- 書き込み先は `N-HUB-OS/brain/verified/`(新規作成)と `N-HUB-OS/brain/research/`(既存ノートへの追記)、`N-HUB-OS/brain/knowledge_graph.json` のみ。N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
- 裏取りできなかった主張を「検証済み」として書かない。確認できた範囲だけを `## 結論` に書く。
- 1つの research ノートにつき1つの判断(昇格 or 保留)を下し、判断理由を必ず記録する。
