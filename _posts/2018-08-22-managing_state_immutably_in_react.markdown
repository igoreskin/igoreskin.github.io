---
layout: post
title:      "Managing state immutably in React "
date:       2018-08-22 11:36:43 +0000
permalink:  managing_state_immutably_in_react
---


Updating components in React happens in two different ways – externally via props passed down from the component’s parent component, and internally by manipulating the state of the component itself. In external manipulation props can in fact be not only passed down from the parent, but also mapped from the state of the application or from dispatch when using Redux, but the actual component receiving the props remains passive in the sense that it doesn’t participate in the initiation of the manipulation. Manipulating the state of the component is a different thing – here the initiative of the manipulation originates in the component itself. 

Manipulating the state of a component is a very convenient and powerful tool, perhaps most frequently used in various event listener functions, when we change the appearance of the page on the screen for instance by typing something in an input field of clicking a button. What is often forgotten is the fact that the state is essentially an object, i.e. a complex, or reference data type. It means that when we assign the state to a variable and then manipulate the variable in the event listener function, what is stored in the variable is actually a reference to the state, a kind of a pointer, not its actual value, and the change in the variable can redirect the pointer to a new value and therefore mutate the state. 

The good news is that there are, especially in the ES6, simple ways to manipulate the state of a component in a safe immutable way. For example, if we need to change the name of a person by entering it in an input field, we must first find the person in the array of persons, which is a part of the state of the component. It can done like this: 

```
const person = this.state.persons[personIndex];
```

While this is going to work, the problem with this approach is exactly as described above – as soon as we mutate person in the event listener function, for instance: 

```
person.name = event.target.value;
```

we are also in danger of mutating the state, because, instead of the real value, person only contains a reference to the state, and by mutating the reference we are also mutating the state. The solution to this problem is simple – instead assigning the state to the variable directly, we make a copy of the state and assign this copy to the variable, using in this case a spread operator provided by the ES6: 

```
const person = { ...this.state.persons[personIndex] };
```

The same can be done, although less elegantly, with the Object.assign() method in the previous JS versions. After that, no matter how we manipulate the person variable, it is not going to make any impact on the state of the component until we explicitly use the this.setState() method, and even then, as we mutate a copy of the state and then assign it to the new state, the original state of the component always remains unchanged.  

