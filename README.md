## Users テーブル
| Column       | Type   | Options     |
| ------------ | ------ | ----------- |
| nickname     | string | null: false |
| introduction | text   |             |
| email        | string | null: false |
| password     | string | null: false |

### Association
- has_many :relationships
- has_many :followings, through: :relationships, source: :follow
- has_many :reverse_of_relationships, class_name: 'Relationship', foreign_key: 'follow_id'
- has_many :followers, through: :reverse_of_relationships, source: :user
- has_many :house_users
- has_many :houses, through: :house_users
- has_many :roles
- has_many :checks



## Relationships テーブル
| Column | Type       | Options                           |
| ------ | ---------- | --------------------------------- |
| user   | references | foreign_key: true                 |
| follow | references | foreign_key: { to_table: :users } |

### Association
- belongs_to :user
- belongs_to :follow, class_name: 'User'



## Houses テーブル
| Column       | Type    | Options     |
| ------------ | ------- | ------------|
| name         | string  | null: false |
| introduction | text    |             |
| owner_id     | integer | null: false |

### Association
- has_many :house_users
- has_many :users, through: :house_users
- has_many :roles



## House_users テーブル
| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| user_id   | references | null: false, foreign_key: true |
| house_id  | references | null: false, foreign_key: true |

### Association
- belongs_to :user
- belongs_to :house



## Roles テーブル
| Column   | Type       | Options                        |
| -------- | ---------- | ------------------------------ |
| title    | string     | null: false                    |
| house_id | references | null: false, foreign_key: true | 
| user_id  | references | null: false, foreign_key: true |  

### Association
- belongs_to :house
- belongs_to :user
- has_many :checks



## Checks テーブル
| Column   | Type       | Options                        |
| -------- | ---------- | ------------------------------ |
| body     | text       | null: false                    |
| role_id  | references | null: false, foreign_key: true |
| user_id  | references | null: false, foreign_key: true | 

### Association
- belongs_to :role
- belongs_to :user