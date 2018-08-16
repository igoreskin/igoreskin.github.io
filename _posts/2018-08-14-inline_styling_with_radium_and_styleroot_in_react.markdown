---
layout: post
title:      "Inline styling with Radium and StyleRoot in React "
date:       2018-08-14 22:59:53 -0400
permalink:  inline_styling_with_radium_and_styleroot_in_react
---


Like plenty of other things in React, styling can be implemented in a number of different ways. The most conventional way of declaring and using CSS styles, and not just in React, is to simply create separate .css files and use CSS selectors. This way e.g. a class can be given the same style across the entire application, which may be a good thing as long as the application is not too large and still easy to control. There is, however, a considerably more flexible and powerful way to inline style individual elements of our components right inside the component itself without using separate .css files at all. Not only inline styling does allow us to avoid conflicts between specific classes in different components, it also gives us more freedom to style a component without inadvertently altering styles in other components and even eliminates a lot of potentially unnecessary .css files in our application. 

Using a button as an example, as long as we use ordinary CSS features, such as color, border, etc., we can easily style the button inline by collecting our styles into a JS object and assigning this object to a variable, for instance style: 

```
const style = {
      backgroundColor: 'green',
      color: 'white',
      border: '1px solid blue',
      padding: '8px',
      cursor: 'pointer', 
}

```

We can then use this object when rendering the button inside the return statement: 

```
<button style={style} … … /> 
```

The problem with this approach is that since things like pseudoselectors and media queries are not CSS features, they can’t be used for inline styling without a special set of tools, and that’s where Radium comes in, which is a set of tools particularly designated to managing advanced inline styling. To use Radium in a component, it must first be installed from the command line by typing: 

```
npm install radium 
```

and then imported at the top of the component in the usual way: 

```
import Radium from ‘radium’;
```

This will allow us to use pseudoselectors, such as for instance :hover, in our style variable – but, since they are still not CSS features, they must be written as strings: 

```
const style = {
      backgroundColor: 'green',
      color: 'white',
      border: '1px solid blue',
      padding: '8px',
      cursor: 'pointer',
      ':hover': {
        backgroundColor: 'lightgreen',
        color: 'black',
      } 
}
```

An important thing to remember is, when exporting the component at the end of the file, it must be passed to Radium as an argument like this: 

```
export default Raduim(App); 
```

To use media queries in our inline styling, we must go an extra length and use a Radium tool called StyleRoot, which we can also import from Radium: 

```
import Radium, { StyleRoot } from 'radium'; 
```

The difference is that, instead of passing our App to StyleRoot as an argument, we must wrap the entire div in the return statement into StyleRoot to enable the use of inline media queries in the child components of the App: 

```
return (
  <StyleRoot>
      <div class=”App”> 
      … … 
      … … 
      </div>
    </StyleRoot> 
) 
```

Now, in a child component of the App, let’s say Person, we can declare its own variable style with a media query assigned to it: 

```
const style = {
    ‘@media (min-width: 500px)’: {
    width: ‘450px’
  }
}
```

and then use this variable for the inline styling in our component: 

```
return (
<div className=”Person” style={style}>
… …
… …
</div>
)
```

Again, the important thing to remember is not only to import Radium from ‘radium’, but also to pass our component to Radium as an argument: 

```
export default Radium(person);
```

These examples show that Radium offers an excellent comprehensible interface where advanced inline styling is not only standardized, but also very clear, readable, and manageable. 
