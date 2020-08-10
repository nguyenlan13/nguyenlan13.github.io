---
layout: post
title:      "Redux Thunk"
date:       2020-08-10 01:21:49 +0000
permalink:  redux_thunk
---

Thunk is a higher-order function that returns a new function. It is a Redux middleware used to allow asynchronous actions to return a function instead of an action, this can be done through writing action creators. These action creators allow the dispatch of an action to be delayed or to dispatch only if a certain condition is met. An example of an asynchronous function is below:

```
export const getAttemptComments = (csrf_token, attemptId) => {
    return async function (dispatch) {
        try{
            dispatch({
                type: LOADING
            })
            let response = await fetch(baseURL + `attempts/${attemptId}/comments`, {
                method: "GET",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json',
                    'X-CSRF-TOKEN': csrf_token
                },
                credentials: 'include'
            })
            if(!response.ok){
                throw response
            }
            let attemptCommentsJson = await response.json()
                dispatch({
                    type: GET_ATTEMPT_COMMENTS,
                    payload: attemptCommentsJson
                })
        }catch(error){
            console.log(error.message)
        }
    }
}

```
