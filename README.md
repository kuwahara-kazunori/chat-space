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
- has_many :groups, through: :groups_users

## messagesテーブル

|Column|Type|Options|
|------|----|-------|
|message|text|null: false|
|date|datetime|null: false|

### Association
- belongs_to :user
- has_many :member, througt: :members_messages

## groupsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|index: true, null: false, unique: true|

### Association
- has_many :user, through: :groups_users
- has_many :member, througt: :groups_members

## membersテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

### Association
- has_many :members, through: :groups_members
- has_many :messages, througt: :members_messages

## groups_usersテーブル

|Column|Type|Options|
|------|----|-------|
|groups_id|integer|null: false, foregin_key: true|
|users_id|integer|null: false, foregin_key: true|

### Association
- belongs_to :group
- belongs_to :user

## groups_membersテーブル

|Column|Type|Options|
|------|----|-------|
|groups_id|integer|null: false, foregin_key: true|
|members_id|integer|null: false, foregin_key: true|

### Association
- belongs_to :group
- belongs_to :member

## members_massegesテーブル

|Column|Type|Options|
|------|----|-------|
|members_id|integer|null: false, foregin_key: true|
|messages_id|integer|null: false, foregin_key: true|

### Association
- belongs_to :member
- belongs_to :messege

