# README

## Owners テーブル

| Column       | Type   | Options                  |
| ------------ | ------ | ------------------------ |
| email        | string | null: false, unique:true |
| password     | string | null: false, default""   |
| first_name   | string | null: false, default""   |
| last_name    | string | null: false, default""   |
| first_kana   | string | null: false, default""   |
| last_kana    | string | null: false, default""   |
| phone_number | string |                          |

### Association

- has_one  :address, dependent: :destroy
- has_many :stores, dependent: :destroy
- has_many :cards, dependent: :destroy

## Owners_Cards テーブル

| Column      | Type    | Options                  |
| ----------- | ------- | ------------------------ |
| customer_id | string  | null: false              |
| card_id     | string  | null: false, unique:true |
| owner_id     | integer | foreign_key:true         |

### Association

- belongs_to :owner

## Stores テーブル
| Column        | Type    | Options                |
| ------------- | ------- | ---------------------- |
| name          | string  | null: false, default"" |
| owners_id     | integer | null: false            |

### Association
- has_one  :address, dependent: :destroy
- has_many :foods, dependent: :destroy
- belongs_to :owner, optional: true
- belongs_to_active_hash :prefecture



## Store_address テーブル

| Column        | Type    | Options                |
| ------------- | ------- | ---------------------- |
| zipcode       | string  | null: false, default"" |
| prefecture_id | integer | null: false            |
| city          | string  | null: false, default"" |
| address       | string  | null: false, default"" |
| build_name    | string  |                        |
| store_id      | integer | foreign_key: true      |

### Association

- belongs_to :store, optional: true
- belongs_to_active_hash :prefecture

## Foods テーブル

| Column        | Type    | Options                       |
| ------------- | ------- | ----------------------------- |
| name          | string  | null: false                   |
| detail        | text    | null: false                   |
| price         | integer | null: false                   |
| lost_time     | datetime| null: false                   |
| situation     | integer | enum, null: false, default: 0 |
| category_id   | integer | foreign_key: true             |
| user_id       | integer | foreign_key: true             |
| buyer_id      | integer |                               |

### Association

- has_many :images, dependent: :destroy
- has_many :users,through: :groupfood_users ,dependent: :destroy
- belongs_to :category
- belongs_to :store

## Images テーブル

| Column  | Type    | Options           |
| ------- | ------- | ----------------- |
| image   | text    | null: false       |
| food_id | integer | foreign_key: true |

### Association

- belongs_to :food


## Categories テーブル

| Column   | Type         | Options     |
| -------- | ------------ | ----------- |
| name     | string       | null: false |
| ancestry | string:index |             |

### Association

- has_many :foods


## food_user テーブル

| Column       | Type   | Options                  |
| ------------ | ------ | ------------------------ |
| food_id      | string | null: false, foreign_key |
| user_id      | string | null: false, foreign_key |

### Association

- belongs_to :food
- belongs_to :user


## Users テーブル

| Column       | Type   | Options                  |
| ------------ | ------ | ------------------------ |
| nickname     | string | null: false, unique:true |
| email        | string | null: false, unique:true |
| password     | string | null: false, default""   |
| first_name   | string | null: false, default""   |
| last_name    | string | null: false, default""   |
| first_kana   | string | null: false, default""   |
| last_kana    | string | null: false, default""   |
| birthday     | date   | null: false              |
| phone_number | string | null:false               |

### Association

- has_one  :address, dependent: :destroy
- has_many :foods, through: :food_users
- has_many :cards, dependent: :destroy
- has_many :addresses, dependent: :destroy
- has_many :cards, dependent: :destroy

## User_cards テーブル

| Column      | Type    | Options                  |
| ----------- | ------- | ------------------------ |
| customer_id | string  | null: false              |
| card_id     | string  | null: false, unique:true |
| user_id     | integer | foreign_key:true         |

### Association

- belongs_to :user



## User_address テーブル