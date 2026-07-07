# 02. Principles — 判断基準

## 情報源の優先順位

構想書に基づき、収集時の優先順位を以下に固定する(上が高優先):

1. GitHub(実装・READMEなど一次ソース)
2. Reddit
3. Hacker News
4. X(旧Twitter)
5. YouTube
6. Product Hunt
7. Medium / Dev.to
8. 公式ブログ・公式ドキュメント

日本語コンテンツは前提として除外し(海外一次情報を優先する構想書の方針)、日本語化・要約は Knowledge Engine 側の仕事とする。

## 「検証済み(Verified)」に昇格する条件

`brain/research/` から `brain/verified/` へ昇格するには、以下をすべて満たすこと([11_brain.md](11_brain.md) の保存形式と対応):

- 独立した 2 ソース以上で同じ主張が確認できる、または実際に手元で再現確認ができた
- 情報の鮮度(いつの情報か)が front-matter に記録されている
- 実用性(実際に何かを作る・判断する際に使えるか)がある

## 除外対象

- 公式発表前の未確定情報・噂ベースの推測
- 誇大広告のみで再現性が確認できないもの
- 著作権的にグレーな無断転載・全文コピー
- 個人情報を含むもの

## 品質の最終判断は N-Link に委ねる

N-HUB-OS 側では「収集・検証・生産」のドメイン判断を行うが、成果物としての品質保証(Golden Ticket 10 項目・PASS/FAIL 判定)は N-Link の `brain_evaluate_quality` / `brain_evaluate_council` が担う。N-HUB-OS は判定結果を偽ったり、FAIL を PASS として扱ったりしない。

## 最適化方針

- 同じ調査・同じ実装を繰り返さない(`brain/verified/` と過去の `brain_record_success` を先に確認する)
- 使われない抽象化・空の engine ディレクトリを作らない
- 1つのタスクは1つの明確な成果物に対応させる(巨大な一括実装をしない)
