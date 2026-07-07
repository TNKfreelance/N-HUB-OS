# 21. Verification Engine

## 目的

`brain/research/` の未検証ノートを実際に裏取りし、`brain/verified/` へ昇格させるかどうかを判断する。実装は [skills/verification/SKILL.md](../skills/verification/SKILL.md)(Claude Code Skill、実地テスト・独立監査済み、[90_roadmap.md](90_roadmap.md) 参照)。

## 昇格条件

[02_principles.md](02_principles.md) で定義される条件をそのまま適用する:

1. 独立した2ソース以上で同じ主張が確認できる、または実際に手元で再現確認ができた
2. 情報の鮮度が記録されている
3. 実用性がある

条件を満たさない場合は昇格させず、元の research ノートに理由を記録して未検証のまま残す。

## 入力・出力

- 入力: `brain/research/*.md`(`status: unverified`)
- 出力: `brain/verified/<slug>.md`(新規作成)、または昇格見送りの理由を記録した research ノートの更新

## 保存形式

昇格先のファイル形式は [11_brain.md](11_brain.md) を参照。

## 実績

2026-07-07時点で実データ2件を実際に裏取りし昇格させた実績あり(1件は独立3ソースの一致、1件はAPIへの実アクセスによる再現確認)。詳細は [../self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) の v0.3.0 を参照。
