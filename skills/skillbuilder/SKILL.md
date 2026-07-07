---
name: n-hub-skillbuilder
description: Designs and scaffolds new N-HUB-OS Claude Code Skills (skills/<name>/SKILL.md) that follow N-HUB-OS's own conventions (naming, section structure, frontmatter schema, mandatory N-Link folder blacklist), and checks existing N-HUB-OS skills for convention drift. Use this whenever the user asks to create a new N-HUB-OS skill for one of the remaining engines (Writer, Publisher, Automation, MCPBuilder, Analytics, SecondBrain), or to review/lint existing N-HUB-OS skills for consistency, or explicitly says "N-HUB-OS SkillBuilder". Do not use this for generic (non-N-HUB-OS) Claude Code skill creation -- use the skill-creator skill directly for that, and for the full eval/benchmark iteration loop on any skill including N-HUB-OS ones.
---

# N-HUB-OS SkillBuilder Skill

## 目的

N-HUB-OS用の新しいSkillを、N-HUB-OS内で確立された構造(命名規則・セクション構成・frontmatterスキーマ・N-Link不可侵の明記)に沿って設計する。正本は N-HUB-OS リポジトリの `docs/23_skill_engine.md`(各skillの目的/入力/出力の一覧)。

**skill-creatorとの役割分担**: このスキルは汎用の `skill-creator:skill-creator` を置き換えない。むしろそれに乗る形で、N-HUB-OS固有の型(規約)を提供する薄い層である。実際のフルeval/ベンチマークループ(テストケース作成・並列実行・採点・比較)が必要な場合は `skill-creator:skill-creator` を呼ぶこと。低リスク・仕様が明確なN-HUB-OS skill(Research/Verification/Knowledgeがこれまでそうだったように)では、そのフルループは省略し独立監査官によるレビューで代替してよい。

## N-HUB-OS skillの型(規約)

既存の3つの実装済みskill(`skills/research/`, `skills/verification/`, `skills/knowledge/`)から抽出された、すべてのN-HUB-OS skillが従うべき構造:

**frontmatter:**
```yaml
---
name: n-hub-<engine-name>
description: <トリガー条件を具体的に列挙し、他のN-HUB-OS skillとの違い・「使わない場面」を明記した一段落>
---
```

**本文セクション(この順序):**
1. `# <Skill Name> Skill` — H1タイトル
2. `## 目的` — Specificationへの参照を含む2-3文
3. ドメイン固有のセクション(判断基準・分類方法など。skillごとに異なってよい)
4. `## 手順` — 番号付きの具体的な手順
5. `## 出力フォーマット` — 実際のテンプレート・スキーマ例
6. `## 守るべき制約` — **必ず最後**。以下を含む:
   - 書き込みを許可されたディレクトリの明記(他のディレクトリへの書き込み禁止)
   - N-Link関連フォルダのブラックリスト(下記を一字一句コピーする):
     `~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`
   - 他のN-HUB-OS skillとの範囲の重複回避(何をしないか)

**命名規則:**
- ディレクトリ: `skills/<engine-name>/SKILL.md`(英小文字、ハイフンなし、`23_skill_engine.md`の行名を小文字化したもの)
- frontmatterの`name`: `n-hub-<engine-name>`

## 手順

1. `docs/23_skill_engine.md` から対象のskill行(目的/入力/出力)を確認する。
2. 既存の実装済みskill(3つ)を読み、命名・セクション構成・N-Linkブラックリストの正確な文言を確認する(コピペで一字一句一致させる。手で書き直さない)。
3. 対象skillの入力・出力に基づき、他のskillと範囲が重複しないよう「やらないこと」を明確にする(例: 新しい知見の収集はResearchの仕事、昇格判断はVerificationの仕事、等)。
4. 上記の型に従って `skills/<engine-name>/SKILL.md` を作成する。
5. `skills/README.md` の実装済み/未実装リストを更新する。
6. `docs/90_roadmap.md` と `self-evolution/CHANGELOG.md`・`self-evolution/VERSION` を、これまでのマイルストーンと同じ形式で更新する。
7. 作成したskillを実際に(可能な範囲で)動かして機能を確認する。新規skillの場合は現実のデータに対して手順を実行し、既存skillの場合は規約への準拠を実地でチェックする。

## 出力フォーマット

新規skillは上記「N-HUB-OS skillの型」のテンプレートに従う。既存skillの規約チェック結果は以下の形式で報告する:

```markdown
| Skill | 命名 | セクション順 | N-Linkブラックリスト一致 | 判定 |
|---|---|---|---|---|
```

## 守るべき制約

- 書き込み先は `N-HUB-OS/skills/<name>/SKILL.md`(新規作成)、および規約チェックで既存skillの記述を修正する場合はその該当skillファイルのみ。
- N-Link 関連フォルダ(`~/.n-link`, `N-Link-Project`, `N-Link-Cockpit`, `N-Link-Cockpit-Electron`, `N-Link ♾️`, `N-link`, `n-link-brain.stale_bak_20260621`)には絶対に読み書きしない。
- 新規skillの「本文の実質的な中身(ドメイン固有の判断基準など)」を安易に空欄・TODOのまま残さない。中身まで含めて完成させられない場合は、そのskillの実装は完了扱いにせず、別タスクとして仕切り直す(未完成のものを成果物として残さない)。
- フルのeval/ベンチマークループ(skill-creatorの実行)が必要かどうかは、対象skillのリスク・仕様の明確さに応じて判断し、省略する場合はその理由をCHANGELOGに明記する。
