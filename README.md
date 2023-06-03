# テーブル設計

## users テーブル

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| email              | string  | null: false, unique: true |
| encrypted_password | string  | null: false               |
| nickname           | string  | null: false               |
| avatar             | string  |                           |
| job                | text    |                           |
| language           | text    |                           |
| hobby              | text    |                           |
| profile            | text    |                           |

### Association

- has_many :events
- has_many :bookings
- has_many :messages
- has_many :entries
- has_many :rooms, through: :messages, entries

## events テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| title     | string     | null: false                    |
| workshop  | text       | null: false                    |
| stay      | text       | null: false                    |
| price     | integer    | null: false                    |
| address   | string     | null: false                    |
| latitude  | float      | null: false                    |
| longitude | float      | null: false                    |
| user      | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- has_one :booking

## bookings テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| user      | references | null: false, foreign_key: true |
| event     | references | null: false, foreign_key: true |


### Association

- belongs_to :user
- belongs_to :event
- has_one :contact

## contacts テーブル

| Column          | Type       | Options                        |
| --------------- | ---------- | ------------------------------ |
| adult           | integer    | null: false                    |
| kid             | integer    | null: false                    |
| infant          | integer    | null: false                    |
| last_name       | string     | null: false                    |
| first_name      | string     | null: false                    |
| last_name_kana  | string     | null: false                    |
| first_name_kana | string     | null: false                    |
| postal_code     | string     | null: false                    |
| region_id       | integer    | null: false                    |
| city            | string     | null: false                    |
| street          | string     | null: false                    |
| building_name   | string     |                                |
| phone_number    | string     | null: false                    |
| announce        | text       |                                |
| booking         | references | null: false, foreign_key: true |

### Association

- belongs_to :booking

## rooms テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
|           |            |                                |

### Association

- has_many :entries
- has_many :messages
- has_many :users, through: :entries, messages

## entries テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| user      | references | null: false, foreign_key: true |
| room      | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :room

## messages テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| user      | references | null: false, foreign_key: true |
| room      | references | null: false, foreign_key: true |
| comment   | text       | null: false                    |

### Association

- belongs_to :user
- belongs_to :room