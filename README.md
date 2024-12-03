# Laravel + Sanctum 学習プロジェクト

このリポジトリは、Laravel 11、Sanctumを使用したシンプルなトークンベースのWebアプリケーション開発の学習用プロジェクトです。

## 概要

- Laravel 11
- Sanctum
- SQLite
- React (Inertia.js)

## 前提条件

- PHP 8.2以上
- Composer
- Node.js / npm
- SQLite

## プロジェクトの目的

このプロジェクトは以下の学習を目的としています：

1. Laravel Sanctumを使用したAPIトークン認証の基本的な実装方法
2. SPAとAPIの連携
3. セキュアなAPI認証の実践

## 環境構築手順

```bash

# .envファイルの準備
cp .env.example .env

# プロジェクトのインストール
composer install
php artisan key:generate
npm install

# データベースの作成
touch database/database.sqlite
php artisan migrate

# 開発サーバーの起動
php artisan serve
npm run dev

# テスト用のユーザーを作成
php artisan tinker
>>> User::create(['name' => 'test', 'email' => 'test@example.com', 'password' => Hash::make('password')]);
>>> exit

# ブラウザでアクセスしてトークン発行＆plain-text tokenを確認
http://localhost:8000

```

## API エンドポイント

| エンドポイント | メソッド | 説明 | 認証要否 |
|--------------|---------|------|---------|
| /api/user    | GET     | ユーザー情報の取得 | 要 |

## トークン認証のテスト方法

1. ブラウザで http://localhost:8000 にアクセス
2. ログイン後、トークンを取得
3. 以下のヘッダーでAPIリクエストを送信：
   - Content-Type: application/json
   - Accept: application/json
   - Authorization: Bearer <取得したトークン>

## セキュリティ設定

- CORSの設定は `config/cors.php` で管理
- トークンの有効期限は `config/sanctum.php` の `expiration` で設定可能
- デフォルトでCSRF保護が有効

## この後の進展

- sanctumガード下のAPIを増やす
- 基本的に、認証が必要なAPIは、毎回ヘッダにトークンを含める

## トラブルシューティング

よくある問題と解決方法：

1. トークン認証エラー
   - トークンの形式が正しいか確認
   - ヘッダーに「Bearer」が含まれているか確認

2. CORS エラー
   - `config/cors.php` の設定を確認
   - `supports_credentials` が `true` に設定されているか確認


## 参考資料

本プロジェクトは以下の記事を参考に作成しています：
- [API認証に使えるLaravel SanctumのToken APIを完全理解](https://reffect.co.jp/laravel/laravel-sanctum-token)

## 謝辞

Reffectの皆様には、いつも大変参考になる技術記事を提供していただき、心より感謝申し上げます。

## ライセンス

[MIT license](https://opensource.org/licenses/MIT)
