---
layout: post
title:      "React Hooks"
date:       2020-03-30 15:47:03 +0000
permalink:  react_hooks
---


With the addition of React hooks, functional components could now use state and mimic the functionality of lifecycle hooks which were previously only available to class components. Hooks were added to the React library in v16.8. Two popular and widely used built in hooks are useState and useEffect. The useState() hook makes it possible to add local state to a functional component and can be called multiple times in the same component. This function returns a pair, the current state and a function to update the current state. It is comparable to this.setState in a class component except the old and new state is not merged together. An example of a sign up form using hooks is below:

```
import React, { useState } from "react";

const SignupForm = (props) => {
  const [email, setEmail] = useState("");
  const [username, setUsername] = useState("");
  const [name, setName] = useState("");
  const [password, setPassword] = useState("");
  const handleSubmit = e => {
    e.preventDefault();
    // send the inputs to the signup thing
    console.log(email, username, name, password);
    setEmail("");
    setUsername("");
    setName("");
    setPassword("");

   props.handleSubmit(email, username, name, password)
  };
  return (
    <form onSubmit={handleSubmit}>
      <input
        className="mr-sm-2"
        type="text"
        placeholder="Email"
        onChange={e => setEmail(e.target.value)}
        value={email}
      />
      <br/>
      <input
        className="mr-sm-2"
        type="text"
        placeholder="Username"
        onChange={e => setUsername(e.target.value)}
        value={username}
      />
      <br/>
      <input
        className="mr-sm-2"
        type="text"
        placeholder="Name"
        onChange={e => setName(e.target.value)}
        value={name}
      />
      <br/>
      <input
        className="mr-sm-2"
        type="password"
        placeholder="Password"
        onChange={e => setPassword(e.target.value)}
        value={password}
      />
      <br/>
      <input type="submit" />
    </form> 
  );
};
export default SignupForm;
```


