# 26. Writer Engine

**状態: 未実装**([90_roadmap.md](90_roadmap.md) 参照)。以下は仕様のみで、実装(`skills/writer/SKILL.md`)は個別タスクとして着手時に作成する。

## 目的

`brain/verified/` の検証済み知識から、記事・台本などのコンテンツ原稿を作る。

## 入力・出力

- 入力: `brain/verified/*.md` + `templates/`
- 出力: 原稿ファイル(保存先は実装時に確定させる。現時点で未確定のまま先取りして仕様化しない)

## 関連

- 原稿の元になる知識の裏取り状態は [21_verification_engine.md](21_verification_engine.md) に従う
- 公開前チェックは [27_publishing_engine.md](27_publishing_engine.md) を参照
