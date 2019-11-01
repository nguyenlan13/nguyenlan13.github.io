---
layout: post
title:      "Make an imPACT"
date:       2019-11-01 10:04:23 -0400
permalink:  make_an_impact
---


The project scope is comprised of building a complete Ruby on Rails application. The application utilizes nested RESTful routes and have multiple many to many,  has_many and belongs_to associations. 

# Topic: Identity-based habits

Habits are often thought of at the level of outcome or process change. Usually it is results driven; an example would be losing a specified amount of weight or implementing a daily meditation practice. Habits at this level often will not last long term.  

Building good habits that last is not an easy feat. The key to successfully building a lasting habit is to associate the habit to a new identity. Identity-based habits have a greater likelihood of lasting long term because they are more closely tied to how an individual is defined. An identity-based habit focuses on what kind of person you want to become and operates on the level of belief change.

The name “imPACT” has multiple meanings. Good habits can have a major impact on long term success. The prefix “im” represents self and who we wish to become, such as “I am a great programmer”. Pact represents an agreement with oneself or with others (accountability buddies) to stick to these habits that will lead us to the identity (goal) that we desire. 

This application uses “identity” as the connection between users and habits. A user has many habits through a, identity. It allows a user to create an identity and a habit and associate the two. Users who have a similar goal can join in on an identity and form pact. From the habits a user associates with an identity, action steps can be created to help break the habit into smaller and very specific steps in order to start the habit formation. For instance, using the previous identity of “I am a great programmer” could have a habit of “code often”. An action step will take this habit and break it into precise steps: “I will work on a coding challenge before work at home at 5am on Monday, Wednesday, and Friday for 2 hours. This sets a specific intention for the task at hand. 


# Implementation
This application uses a Model-View-Controller structure with CRUD actions, complex forms,  and RESTful routes. 

My core associations were as follows:

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
		
end

class Habit < ApplicationRecord   
    has_many :streaks, dependent: :destroy
    has_many :steps, dependent: :destroy
    has_many :identity_habits, dependent: :destroy
    has_many :identities, through: :identity_habits
    has_many :users, through: :identities
    has_many :comments, as: :commentable, dependent: :destroy
end

class Step < ApplicationRecord
  belongs_to :user
  belongs_to :habit
end
		
```

There is a many to many relationship between users and identities, identities to habits, and users to habits. Actions belong to both a habit and a user.


This is a sample of the nested routes available:
```
#nested routes

resources :users do  
        resources :identities, only: [:index, :new, :create]
        resources :habits
        resources :steps

    end

    resources :identities do
        resources :users, only: [:show, :index]
        resources :habits
     
    end

    resources :habits do
        resources :steps

    end
```




# Project Outcome

The core functionality of the application is working as I had envisioned. However, there were some features that I did not yet add to the application. Users are able to join an identity, or "pact" and they can unjoin if they wish. They can link habits to the identity and also unlink them as they wish. From the habits, they are able to create action steps for which they will follow to gradually build up their habit.


