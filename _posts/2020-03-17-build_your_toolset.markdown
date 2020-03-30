---
layout: post
title:      "Build your toolSet"
date:       2020-03-17 21:54:29 -0400
permalink:  build_your_toolset
---



This application was built utilizing a Ruby on Rails backend with session cookies for API authentication, PostgreSQL database,  and a React with Redux frontend.



## Adding Tools to Your toolSet

The idea behind this application was to “add a tool” to our mental library or “toolset” in which a learn by teaching methodology is used to learn new concepts. The concepts can be anything the user chooses; the user creates a lesson and each attempt at the lesson is posted to the community for feedback.  The user can make as many attempts as needed in order to fully understand. 



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


## React Frontend

React is a frontend JavaScript framework that makes it easy to create interactive UIs for SPAs and resusable components. Components can be written as functional or class based. Most of the components in this project were class based, which extends component: 

```
import React, { Component } from 'react'
import { connect } from 'react-redux'
import { addCategoryTopic } from '../actions/topic'
import TopicItem from '../components/Topic/TopicItem'
import TopicForm from '../components/Topic/TopicForm'
import { getCategoryTopics } from '../actions/topic'

class CategoryTopicContainer extends Component {

    componentDidMount() {
        let categoryId = this.props.match.params.categoryId
        this.props.get_category_topics(this.props.csrf_token, categoryId)
    }
    
    submitHandler = async (name) => {
        let categoryId = this.props.match.params.categoryId
        await this.props.add_category_topic(this.props.csrf_token, name, categoryId)
    }

    render() {
        const { categoryTopics } = this.props
        const sortedCategoryTopics = categoryTopics.sort(function(a,b){
            if(a.name < b.name) {return -1;}
            if(a.name > b.name) {return 1;}
            return 0
        })
        return(
            <div className="page">
                <h1 className="headlines"> TOPICS:</h1>
                    <TopicForm handleSubmit={this.submitHandler}/>
                    {sortedCategoryTopics.map(topic => {
                        return <TopicItem
                            topicName={topic.name} 
                            key={topic.id} 
                            topicId={topic.id}
                        />
                    })}
            </div>
        )     
    }
}

const mapStateToProps = (state) => {
    const { topics, csrf_token } = state
    return { 
        categoryTopics: topics.categoryTopics, 
        loading: topics.loading,
        csrf_token: csrf_token
    }
}

const mapDispatchToProps = (dispatch) => ({
    get_category_topics: (csrf_token, categoryId) => dispatch(getCategoryTopics(csrf_token, categoryId)),
    add_category_topic: (csrf_token, name, categoryId) => dispatch(addCategoryTopic(csrf_token, name, categoryId))
})

export default connect(mapStateToProps, mapDispatchToProps)(CategoryTopicContainer)
```


Inheriting from class Component allows the child class to have access to setState() to manage its own state and also have access to lifecycle methods. In this example, the lifecycle method componentDidMount(), which is invoked immediately after the component is mounted,  is used to call an async function to fetch the category topics from the API.



## Using Redux

As seen in the CategoryTopicContainer class above, the Redux library is used to manage state with connect() and its mapStateToProps and mapDispatchToProps arguments. Redux is a standalone library and React-Redux is used to bind Redux to React. 
The store is created using createStore() and passing in the rootReducer, which is created by using the combineReducers helper function from the Redux library to combine all the reducers into one. The Redux store is available to nested components through Provider from the React-Redux library. Provider wraps the root-level component, in this case, App: 


```

//index.js

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { Provider } from 'react-redux'
import { createStore, compose, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import rootReducer from './reducers/rootReducer'

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const store = createStore(rootReducer, composeEnhancers(applyMiddleware(thunk)))


ReactDOM.render(
<Provider store={store}>
    <   App />
</Provider>,
    
document.getElementById('root'));

```

```
// Reducers

import { combineReducers } from 'redux'
import tokenReducer from './tokenReducer'
import categoryReducer from './categoryReducer'
import userReducer from './userReducer'
import topicReducer from './topicReducer'
import lessonReducer from './lessonReducer'
import attemptReducer from './attemptReducer'
import commentReducer from './commentReducer'

const rootReducer = (combineReducers) ({
    csrf_token: tokenReducer,
    user: userReducer,
    categories: categoryReducer,
    topics: topicReducer,
    lessons: lessonReducer,
    attempts: attemptReducer,
    comments: commentReducer

})

export default rootReducer

```

The mapStateToProps and mapDispatchToProps functions makes the state and dispatching actions available through props, these two functions are the first and second arguments to connect(). Dispatching async logic is done through the use of the middleware, Thunk. Thunk allows action creators to return a function rather than an action, this allows a promise to resolve before dispatching the action:

```
export const getCategoryTopics = (csrf_token, categoryId) => {
    return async function (dispatch) {
        try {
            dispatch({
                type: LOADING
            })
            let response = await fetch(baseURL + `categories/${categoryId}/topics`, {
                method: "GET",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json',
                    'X-CSRF-TOKEN': csrf_token
                },
                credentials: 'include'
            })
            if(!response.ok) {
                throw response
            }
            let categoryTopicsJson = await response.json()
                dispatch({
                    type: GET_CATEGORY_TOPICS,
                    payload: categoryTopicsJson
                })
           return categoriesJson
        } catch(error) {
            console.log(error.message)
        }
    }
}
```

When get_category_topics is called, the return value of getCategoryTopics is dispatched to the reducer to update the store: 

```
import { 
    LOADING,
    GET_TOPICS,
    ADD_TOPIC,
    GET_CATEGORY_TOPICS,
    ADD_CATEGORY_TOPIC
} from '../actionTypes'

export default function topicsReducer(state = {
        topics: [], 
        loading: false, 
        categoryTopics: []
    }, action){

    switch(action.type){
        case LOADING:
            return {...state, loading: true}
        case GET_TOPICS:
            return {...state, topics: action.payload, loading: false}
        case ADD_TOPIC:
            return {...state, topics: [...state.topics, action.payload]}
        case GET_CATEGORY_TOPICS:
            return {...state, categoryTopics: action.payload, loading: false}
        case ADD_CATEGORY_TOPIC:
            return {...state, categoryTopics: [...state.categoryTopics, action.payload]}
        default:
            return state
    }
}

```

The store is updated with the current state by matching the action type to the case statement and using the spefically formatted keys.


## Additional Features

The next features that will be added will be reactions to lesson attempts and feedback and score keeping to rate the attempts.
