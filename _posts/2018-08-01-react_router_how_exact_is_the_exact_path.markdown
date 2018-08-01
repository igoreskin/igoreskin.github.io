---
layout: post
title:      "React Router: how exact is the exact path? "
date:       2018-08-01 15:18:54 +0000
permalink:  react_router_how_exact_is_the_exact_path
---


The mindset of having and running all applications locally on a device, stationary or mobile, has been already for quite some time shifting towards a completely different, cloud based approach. As applications move from local devices to the cloud and essentially become websites, a user interface, who’s speed and reliability in a local application are taken for granted, becomes perhaps the most important part of the context of the cloud based approach, especially in applications dealing with large amounts of data. 

Instead of rendering countless HTML files from the server, in a Single Page Application React, when browser URL changes, renders components, which are essentially JavaScript files, and that emphasizes the importance of the React Router being actually one of the most important part of React both conceptually and technically. 

Using nested routes for rendering React components, instead of HTML files in an MVC application, is a great way from the point of view of user experience as it may save from a few seconds to even minutes, rendering whatever the user wants to see with the speed of light, but there are a few considerations that must be taken into account, one of them is using the exact path. 

When wrapping the div that we normally return in the App component into <Router> and defining the route to the root, or the landing page of the application, the most intuitive thing would be to define nested routes, including the dynamic ones, in the child components of the App. This is where I encountered an interesting problem – as I defined the exact path to the index page of the application exact path=’/recipes’ the application as if didn’t see the nested routes defined in the App’s child components and, in spite of the changing the URL, just kept rendering the index page. I’ve even consulted with a number of experienced coders only to eventually find out that this kind of approach doesn’t work and that apparently all nested routes should be, at least in the current version of React, defined in the same file, i.e. where the div returned in the App component is whapped into <Router>. Although it solves the problem, the situation may be different if the application has dozens of different routes or if rendering is implemented via multiple HTML pages and the application is therefore no longer an SPA. Nevertheless, knowing little details like this one can save a lot of coding time, because this kind of a problem doesn’t raise any errors, just prevents components from being rendered, and therefore it’s hard to determine where even to begin to debug it. 

The App component with all the routes defined in the same div can be found [here](https://github.com/igoreskin/react-recipe-book/blob/master/recipe-book-client/src/App.js). 

