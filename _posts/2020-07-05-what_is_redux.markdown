---
layout: post
title:      "What is Redux?"
date:       2020-07-06 01:19:48 +0000
permalink:  what_is_redux
---


Redux is a Javascript library that is used for state management in React applications. Redux encourages a single source of truth by building a global store, a javascript object that is separate from the component tree to store component state. The components have access to this global store through a higher order component that wraps each component that needs access to the store. This higher order component is Provider. Provider contains the Connect() function which takes in two arguments, MapStateToProps() and MapDispatchToProps(). This implementation can be seen below:

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
