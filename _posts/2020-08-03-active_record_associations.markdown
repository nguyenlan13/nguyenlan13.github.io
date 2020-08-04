---
layout: post
title:      "Active Record Associations"
date:       2020-08-03 00:44:11 -0400
permalink:  active_record_associations
---


Rails Active Record is a library that provides methods for object relational mapping. Object relational mapping, or associations are connections between models and their database entries. Active record provides the six types of associations below:

```
belongs_to
has_one
has_many
has_many :through
has_one :through
has_and_belongs_to_many
```

Examples of how these associations are utilized in within models are shown below:

```
class User < ApplicationRecord
    has_many :user_identities, dependent: :destroy
    has_many :identities, through: :user_identities
    has_many :habits, through: :identities
    has_many :steps, dependent: :destroy
    has_many :streaks, dependent: :destroy
    has_many :comments, dependent: :destroy
    has_many :reactions, dependent: :destroy
end

class Identity < ApplicationRecord
    has_many :user_identities, dependent: :destroy
    has_many :users, through: :user_identities
    has_many :identity_habits, dependent: :destroy
    has_many :habits, through: :identity_habits
    has_many :comments, as: :commentable, dependent: :destroy

    validates :pact_name, uniqueness: true, presence: true
    validates :description, uniqueness: true, presence: true
end

class Habit < ApplicationRecord    
    has_many :streaks, dependent: :destroy
    has_many :steps, dependent: :destroy
    has_many :identity_habits, dependent: :destroy
    has_many :identities, through: :identity_habits
    has_many :users, through: :identities
    has_many :comments, as: :commentable, dependent: :destroy
end


class IdentityHabit < ApplicationRecord
    belongs_to :identity
    belongs_to :habit
end
```
