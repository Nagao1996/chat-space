# README

## usersテーブル

|Column|Type|Options|
|------|----|-------|
|id|text|null: false|
|email|text|null: false|
|password|text|null: false|
|name|text|null: false|
### Association
- has_many :groups, through: :users
- has_many :users
- has_many :messages

## messagesテーブル
|Column|Type|Options|
|------|----|-------|
|id|text|null: false|
|text|text
|user_id|references|null: false, foreign_key: true|
|group_id|references|null: false, foreign_key: true|
|image|string
### Association
- belongs_to :user
- belongs_to :group

## groupsテーブル
|Column|Type|Options|
|------|----|-------|
|id|text|null: false|
|groupname|text|null: false|
### Association
- has_many :users, through: :users_groups
- has_many :users_groups
- has_many :messages
## users_groupsテーブル
|Column|Type|Options|
|------|----|-------|
|id|text|null: false|
|users_id|references|null: false, foreign_key: true|
|groups_id|references|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :group