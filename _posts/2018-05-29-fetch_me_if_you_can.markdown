---
layout: post
title:      "'Fetch me if you can'"
date:       2018-05-29 22:17:59 -0400
permalink:  fetch_me_if_you_can
---


The transition from XMLHttp requests to fetch() requests can be seen as a part of a comprehensive conceptual paradigm shift, the objective being improved user experience, essentially speed. Where React, instead of manipulating HTML, turns websites into fast and flexible JavaScript applications, similarly Fetch API allows us to write code that is not only cleaner, but also considerably faster. The code is cleaner and simpler because we don’t have to create an XHR object, handle the complexity of callback functions that we must pass to the asynchronous functions, and deal with the exposure to all kinds of errors due to all this complexity. A fetch() request also looks more logical and therefore is more readable. 

From the point of view of speed and user experience, the important thing is that a Fetch API request allows us to asynchronously execute actions without waiting for the request to actually return the result. Instead, a fetch() request returns a hypothetical object called Promise – hypothetical because no real object has yet been returned, so the Promise object acts as a kind of a placeholder. When the Promise is successfully fulfilled, a .then method is always called and moves on with the sequence of the actions. 

Most importantly, and this is particularly useful in action creators in React/Redux, if we make a fetch() request a part of an action creator function, the function doesn’t wait for the Promise to be fulfilled. Instead it jumps right to the next step, and then returns to the result of the request to resolve the Promise with the .then method, which means that the user doesn’t have to wait in the meantime for the Promise to be resolved. That is why in the following example: 

```
  const callApi = () => {
    console.log('a')
    fetch('http://localhost:3001/recipes')
    .then(response => {
      console.log('b')
      return response.json()
    })
    .then(responseJSON => console.log('c', responseJSON))
    .catch(err => console.log('d', err))
    console.log('e')
```


‘a’ is logged to the console first, upon invoking the function; after that the fetch() request is made, but instead of waiting for the result of the request, the function goes ahead and logs ‘e’ to the console, although this action is seemingly the last one. And only after that it jumps back to the Promise, and when it is fulfilled, .then it logs ‘b’ and .then it logs ‘c’ + JSON (if the request is successful) or ‘d’ (if it failed). 

