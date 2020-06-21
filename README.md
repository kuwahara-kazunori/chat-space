# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

# DB設計

## usersテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|index: true, null: false, unique: true|
|email|string|null: false|

### Association
- has_many :messages
- has_many :groups_users
- has_many :groups, through: :groups_users

## messagesテーブル

|Column|Type|Options|
|------|----|-------|
|body|text|null: false|
|image|string||
|user_id|integer|null: false, foregin_key: true|
|group_id|integer|null: false, foregin_key: true|

### Association
- belongs_to :user
- has_many :groups_messages
- has_many :groups, througt: :groups_messages

## groupsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|index: true, null: false, unique: true|

### Association
- has_many :groups_users
- has_many :users, through: :groups_users
- has_many :groups_messages
- has_many :groups, througt: :groups_messages

## groups_usersテーブル

|Column|Type|Options|
|------|----|-------|
|group|references|null: false, foregin_key: true|
|user|references|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :user
