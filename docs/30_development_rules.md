# 30. Development Rules

N-HUB-OS 内でファイル・Skillを作成・更新する際の共通ルール。個々のSkillの型については [skills/skillbuilder/SKILL.md](../skills/skillbuilder/SKILL.md) がより詳細な規約を持つ(このドキュメントはその要約+リポジトリ全体のルール)。

## 命名規則

[03_terminology.md](03_terminology.md) の「命名規則」セクションを正本とする。

## ドキュメント形式

- すべて Markdown。JSON は `knowledge_graph.json` のような機械可読データのみに限定する。
- 各 `docs/` ファイルは冒頭に `# <番号>. <タイトル>` を置く。
- 他ドキュメントへの参照は相対リンク(`[label](relative/path.md)`)で行い、リンク先が実在することを常に確認する。

## Skillの型

[skills/skillbuilder/SKILL.md](../skills/skillbuilder/SKILL.md) の「N-HUB-OS skillの型(規約)」セクションを正本とする(frontmatter・セクション順序・N-Linkブラックリストの一字一句)。

## バージョニング

[60_self_evolution.md](60_self_evolution.md) の SemVer 方針に従う。バージョン番号の実体は [self-evolution/VERSION](../self-evolution/VERSION) に一元管理し、他ドキュメントにバージョン番号をハードコードしない(参照リンクで示す)。

## 変更履歴

内容に実質的な変更を加えたファイル(`brain/verified/*.md` 等)は、上書きせず `## 変更履歴` セクションに追記する。ドキュメント(`docs/`)自体の変更履歴は [self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) に一元管理し、個々の `docs/` ファイルには変更履歴セクションを設けない(過剰実装回避、[00_constitution.md](00_constitution.md) 原則3)。

## 品質保証

すべての実装作業は N-Link 経由で行う([CLAUDE.md](../CLAUDE.md) 絶対ルール1)。低リスクなSkill実装では、フルのeval/ベンチマークループの代わりに独立監査官によるレビューで品質を担保してよい(実績: [self-evolution/CHANGELOG.md](../self-evolution/CHANGELOG.md) の各バージョンエントリ参照)。
