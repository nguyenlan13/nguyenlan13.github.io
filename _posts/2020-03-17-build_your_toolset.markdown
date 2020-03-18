---
layout: post
title:      "Build your toolSet"
date:       2020-03-18 01:54:28 +0000
permalink:  build_your_toolset
---



This application was built utilizing a Ruby on Rails backend with session cookies for API authentication and a React/Redux frontend.


## Adding Tools to Your toolSet

This application uses a learn by teaching methodology to learn new concepts. The concepts can be anything the user chooses. The user creates a lesson and each attempt at the lesson is posted to the community for feedback.  The user can make as many attempts as needed in order to fully understand. 


## Rails API Backend

The API backend uses a Model-View-Controller structure with CRUD actions and RESTful routes. The views are omitted because it is communicating with a JavaScript frontend. The core model associations were:

```
class User < ApplicationRecord
    
    has_many :lessons
    has_many :topics, through: :lessons
    has_many :comments
    has_one :reactions
    
end



class Lesson < ApplicationRecord

    belongs_to :topic
    belongs_to :user
    has_many :attempts
		
end

class Attempt < ApplicationRecord

    belongs_to :lesson
    has_many :comments, as: commentable, dependent: :destroy
    has_many :reactions, as :reactable, depended: :destroy

end
```

## React/Redux Frontend




