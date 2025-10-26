# Repository Guidelines

## プロジェクト構成 & モジュール配置
- `app/`: MVC 本体。`controllers/`・`models/`・`views/`、フロントは `app/javascript`（Importmap）と `app/assets`（CSS/画像）。
- `config/`: ルーティング・初期化・`importmap.rb`・`puma.rb`・`deploy.yml`（Kamal）。
- `db/`: マイグレーション・スキーマ。`storage/` は Active Storage。
- `test/`: Minitest 構成（`models/`、`controllers/`、`system/`）。`fixtures/` あり。
- `bin/`: `rails`・`dev`・`setup`・`rubocop`・`brakeman`・`kamal` などの実行スクリプト。

## ビルド・テスト・開発コマンド
- 開発環境準備: `bin/setup`（依存関係/DB 初期化）。
- ローカル起動: `bin/dev`（`rails server` を起動）。
- DB 準備: `bin/rails db:prepare`（作成/マイグレーション）。
- テスト実行: `bin/rails test`（全テスト）/ `bin/rails test:system`。
- Lint: `bin/rubocop`（`-A` で自動修正）。
- セキュリティ検査: `bin/brakeman`。
- デプロイ（参考）: `bin/kamal deploy`。

## コーディング規約 & 命名
- Ruby 2 スペースインデント、行長は RuboCop 基準（`rubocop-rails-omakase`）。
- 命名: クラスは `CamelCase`、メソッド/変数は `snake_case`、パーシャルは先頭に `_`。
- Rails 慣習に従い、ロジックはモデル/サービスへ、コントローラは薄く。

## テスト方針
- フレームワーク: Minitest（`test/`、`*_test.rb`）。
- モデルはバリデーション/スコープ、コントローラはレスポンス/リダイレクト、System は主要ユーザーフローを網羅。
- 追加/変更時は関連テストを必ず更新。`fixtures/` を活用。

## コミット & PR ガイド
- コミット: 簡潔な英語の命令形（例: `Add user signup flow`）。関連範囲はスコープを先頭に（例: `users:`）。
- ブランチ命名: `feature/<短説明>`、`fix/<短説明>`。
- PR 要件: 目的/背景、変更点、テスト観点、動作確認手順、UI 変更はスクリーンショット、関連 Issue をリンク。
- マージ条件: CI グリーン、`rubocop`/`brakeman` パス、レビュー 1+。

## セキュリティ & 設定
- 機密情報は Rails Credentials を使用（`bin/rails credentials:edit`）。`master.key` を外部に共有しない。
- DB/キャッシュ/キュー設定は `config/*.yml` を参照。環境変数で上書き可能。
