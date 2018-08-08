---
layout: post
title:      "Conditional rendering in React"
date:       2018-08-08 01:48:19 +0000
permalink:  conditional_rendering_in_react
---


One of the great things about React is the fact that the simplicity of its syntax opens a number of options on what logic to use, as well as where and how. Since everything we type into a React component, stateless or stateful, is essentially JavaScript, the variety of options of implementation of various functionalities is as broad as the variety of ways things can be written in JavaScript. This variety is in fact so broad that it is even considered one of the drawbacks of React, which is so unopinionated that a developer can end up with too much choice. 

This is, nevertheless, a good thing when it comes to techniques like conditional rendering. Unlike in Angular or Vue.js, there’s no need to use any non-JS syntax specifically dedicated to conditions; all we need to do is use JavaScript constructs like in any JS file. For instance, conditional rendering of a list of persons can happen based on a condition contained in the property of state of the component that initially evaluates to false: 

```
state = {
    showPersons: false,
}
```

We can then assign this property of the state to a variable, e.g. doesShow, and attach an event listener to a button or any other control responsible for rendering the list conditionally, or toggling between rendering and not rendering, and then manipulate the state using the setState method: 

```
togglePersonsHandler = () =>  {
    const doesShow = this.state.showPersons;
    this.setState({showPersons: !doesShow})
} 
```

Then, inside the render function, we can declare a variable persons and initially assign it to null, keeping in mind the condition where the list of persons is not going to be rendered: 

```
let persons = null;
```

After that we can declare a conditional statement, where if showPersons, which is a Boolean, happens to evaluate to true, the list of persons gets rendered dynamically in a separate div, which we then reassign to already declared variable persons: 

```
if (this.state.showPersons) {
    persons = (
        <div>{this.state.persons.map(person… ) 
… … 
    }
        </div>) 
```

This way of rendering the content conditionally is very clean and easily readable in terms of plain JavaScript, because after setting the conditions like we just did all we have to do is return the variable persons in the return statement, whether it evaluates to the list of persons or to null: 

```
return (
    <div>
    … … … 
        {persons} 
    </div> 
);
```

Another option would be to place the entire conditional rendering inside the return statement, using for instance a ternary expression. The way described above is nevertheless cleaner, as well as more logical and transparent, because every piece of logic in the component takes care of its own part of the task and therefore complies with the principle of separation of concerns. 

