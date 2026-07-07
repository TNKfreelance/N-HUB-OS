---
source: official
source_url: https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/
collected_date: 2026-07-07
category: MCP
status: promoted
---

# MCP 2026-07-28 仕様: プロトコルのステートレス化・拡張機能・認可強化

## 要約

Model Context Protocol の次期仕様(2026-07-28)のリリース候補(RC)が公開された。今回はプロトコル発足以来最大の改定で、主な変更点は以下の4つ:

1. **ステートレス化**: `initialize` ハンドシェイクや `Mcp-Session-Id` によるセッション管理を廃止し、リクエストをクライアントメタデータを含む自己完結型ペイロードにする。これにより、スティッキールーティングや共有セッションストアなしで標準的なロードバランサ配下に配置できるようになる。
2. **拡張機能フレームワーク**: Extensions が独自リポジトリ・バージョニングを持つ正式な機能区分になる。今回同梱される拡張は MCP Apps(サンドボックスiframe内でのサーバーレンダリングHTML UI)と Tasks(ステートレス実行に再設計されたタスクハンドル方式)。
3. **認可の強化**: OAuth 2.0 / OpenID Connect との整合性を高める6つの提案(RFC 9207準拠の `iss` パラメータ検証など)。
4. **運用性の改善**: `Mcp-Method` / `Mcp-Name` ヘッダーでボディを見ずにルーティング可能に、`ttlMs` / `cacheScope` でキャッシュ制御、W3C Trace Context 対応で分散トレーシングが可能に。

「Roots」「Sampling」「Logging」は非推奨(12か月のサポート猶予あり)。

## 元情報からの引用・根拠

- RCは2026年5月21日にロックされ、最終仕様の公開は2026年7月28日予定(検証期間10週間)。
- 出典: [The 2026-07-28 MCP Specification Release Candidate](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)(Model Context Protocol公式ブログ、本文を直接fetchして確認済み)

(注: 初回のWebSearch要約には「Python SDK stable v2も2026-07-27にリリース予定」という記述があったが、引用元として明記した公式ブログ本文を直接確認したところ該当の記述が見つからなかったため、この一文は削除した。一次ソースで確認できない内容は記載しないという [docs/02_principles.md](../../docs/02_principles.md) の検証済み昇格条件に基づく判断。)

## 再現性メモ(実際に試した場合のみ)

未実施(このエントリは公式ブログの内容確認のみ。実際にRC版SDKでの動作確認は別タスク)。

## Updates

- 2026-07-07: 認可強化の詳細を追加。Resource Indicators(RFC 8707)により、トークン発行時にどのMCPサーバー宛かを指定する必要があり、あるサーバー向けに発行されたトークンを別サーバーに対してリプレイできなくなる(confused deputy問題への対策)。プロトコルレベルで強制され、アプリケーション側のチェックに依存しない。(出典: [WorkOS - The biggest MCP spec update ships July 28](https://workos.com/blog/mcp-2026-spec-agent-authentication) 等、複数の第三者解説記事でも同旨の言及あり)

## Verification

- 2026-07-07: WorkOS・mcp.directory の2つの独立ソースで同一の技術的変更点(ステートレス化・認可強化)を確認できたため、[brain/verified/mcp-2026-07-28-stateless-spec.md](../verified/mcp-2026-07-28-stateless-spec.md) へ昇格。
