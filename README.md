# chat-space

## chatspaceの機能
- ユーザーの新規会員登録、ログイン機能
- グループ内でのチャット機能
- 複数人によるグループチャット機能
- チャット相手の検索機能
- チャットグループへのユーザー招待機能
- チャットの履歴表示機能
- チャットグループの作成、チャットメンバーの編集・削除機能
- 画像送信機能
- チャットの自動更新機能

## 本番環境
http://18.182.128.102

## テストアカウント
- name "Mr.Tester"
- email "tester@test"
- password "tester123"

## 使用技術(開発環境)
0.requirement
- Rails "5.0.7.2"
- Ruby "2.5.1"
1.markup
- スタイル追加
- Message モデル, messages テーブル追加
- /messages にアクセスできる
2.messages
- メッセージ投稿
- Messageモデルにバリデーション設定
- Rspecインストール
    - bundle exec rails g rspec:install
    - bundle exec rspec
- locale設定によるエラーメッセージの日本語化
3.devise
- Devise, User モデル導入
    - bundle exec rails g devise:install
- RspecにDevise用マクロ追加
4.group
- Group, GroupUser モデル追加
- チャットグループの追加・更新
- side_menuの共通化
5.incremental_search
- jQuery導入
- チャットグループ設定時にインクリメンタルサーチ
6.async_messages
- メッセージ投稿の非同期化
7.image_upload
- 画像投稿
    - carrierwave導入
8.auto_reload
- 自動再読み込み

## DB設計
### usersテーブル
|Column|Type|Options|
|------|----|-------|
|email|text|null: false|
|password|text|null: false|
|name|string|null: false|
#### Association
- has_many :groups, through: :users_groups
- has_many :users
- has_many :messages

### messagesテーブル
|Column|Type|Options|
|------|----|-------|
|text|text
|user_id|references|null: false, foreign_key: true|
|group_id|references|null: false, foreign_key: true|
|image|string
#### Association
- belongs_to :user
- belongs_to :group

### groupsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
#### Association
- has_many :users, through: :users_groups
- has_many :users_groups
- has_many :messages

### users_groupsテーブル
|Column|Type|Options|
|------|----|-------|
|users_id|references|null: false, foreign_key: true|
|groups_id|references|null: false, foreign_key: true|
#### Association
- belongs_to :user
- belongs_to :group
