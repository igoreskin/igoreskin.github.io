---
layout: post
title:      "Swapping every two adjacent elements in a linked list"
date:       2018-07-19 20:08:23 +0000
permalink:  swapping_every_two_adjacent_elements_in_a_linked_list
---


Although linked lists are not necessarily taught immediately among the fundamentals of JavaScript, it is quite an important dynamic data structure where each node contains some data and a reference to the next node. There is a lot of argument going on about the necessity of linked lists in web development or even in JavaScript in general, since we already have arrays; what is not arguable though is the fact that any developer can encounter linked lists in a technical interview. In my case the task of writing a function that swaps every two adjacent nodes in a singly linked list in JavaScript was given to me as homework. 

After quite a bit of research I recognized a few different approaches, none of them in JavaScript though, with a common thread of trying to squeeze all the logic into the actual swapping function, or some kind of a hang-up on the relationships between the nodes. Instead, I decided to approach a linked list like an array, essentially forgetting that nodes are nodes and treating them like elements of an array where every element has its index. All I needed to do is determine the indices of the nodes and then just swap those indices, instead of trying to change the relationship between the nodes in a single function. So, if we can get, insert, and remove nodes at a certain index number, all we need to do is write helper functions, like getAt(), insertAt(), and removeAt(), in say LinkedList class that would do it for us. Since we are going to iterate through a linked list like through an array, we also need to use a counter and a helper function that finds the size(), or the actual number of nodes in the linked list. 

This approach allowed me to come up with a very simple Object Oriented solution to this problem, where instead of incorporating complex logic of multiple iteration or recursion into the actual swap function, which would make it difficult to read as well as slow in terms of time complexity, I created a function that relies on a few simple helper functions and a counter. 

This solution demonstrates the power of the principle of separation of concerns in the sense that each of the class functions of the LinkedList class only takes care of its own specific task and nothing else, which makes these functions clear and concise. It also allows the actual swap function to completely focus on swapping positions of already located elements, which also makes this function extremely simple, short and easily readable. 
	
The entire code can be found [here](https://github.com/igoreskin/swap-elements-of-linked-list).

