---
layout: post
title:      "Polymorphic Associations"
date:       2020-11-16 06:17:09 +0000
permalink:  polymorphic_associations
---


Polymorphic association is a way to structure our database in rails where a model can belong to more than one model on a single association. 

An example of how a model would structured is:

```
class Comment < ActiveRecord::Base
  validates :user_id, presence: true
  validates :content, presence: true
  validates :commentable_id, presence: true
  validates :commentable_type, presence: true

  belongs_to :user
  belongs_to :commentable, polymorphic: true

  has_many :comments, as: :commentable
  has_many :reactions, as: :reactable
end
```

In this example, a comment belongs to a user and a commentable. A commentable acts similar to an alias that can encompass several items. Items that can be commented on can belong to commentable.
