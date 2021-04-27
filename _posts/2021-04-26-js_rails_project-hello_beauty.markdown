---
layout: post
title:      "JS/Rails Project-Hello, Beauty."
date:       2021-04-27 02:55:20 +0000
permalink:  js_rails_project-hello_beauty
---

JavaScript is hard, really hard! If you get it, wow, I'm super impressed. So building a JS project, even though it was just a single-page-application, was challenging for me. Coming off of Rails where there are very specific rules and pretty clear cut order of operations, JavaScript threw all that out the window. 

I have some themes going in my project building- I like books, beauty and sharing recommendations/reviews of those things. So it's not really any surprise I chose beauty as my foundation again. Beauty products bring joy to everyone, it's a fact....BUT those products can be really expensive. I'm always looking for more affordable alternatives for those crazy expensive products that everyone talks about. Turns out that a lot of people are. So my app is a place where people can share their favorite product dupes (a similiar yet less expensive version of the hero product). This was the easy part. 

The application would incorporate HTML, JavaScript, and CSS  ont the frontend and a Rails API backend. Communication would be through JSON fetch requests (GET and POST for my project). It was suggested that I create two seperate repositories; one for the frontend and another for the backend. Rails generators simplified things by automating a lot of the initial setup. [This](https://github.com/learn-co-curriculum/mod3-project-week-setup-example) is a great guide, and I referred to it quite a bit. And if like me, you also forgot how to create a Rails API- go [here](https://github.com/learn-co-curriculum/js-rails-as-api-creating-a-rails-api-from-scratch). 

A tip I got that I feel obligated to share is that you should create many branches in your repos while working on this project. Every time you work on a new piece, create a branch. If you make a mistake you can easily navigate back to working code. Plus Github's interface makes it so easy to see if you have any conflicts which would cause issues. Also, get ready to have your mind blown: you need to work ***vertically*** building things out in this project. Rails was so easy guiding us along...do all your migrations, build all your models, create all your controllers, create all your views. Not so much here with JS. Always have your console open, and constantly check that what you see is what you actually expect to see (console.log is your new best friend).

THIS!!!! ---> **JS MANTRA: When some event happens, I want to make what kind of fetch and then manipulate the DOM in what way? **

There is a lot to remember in JS, and manipulating the DOM can be confusing. JSON nests our attributes so accessing our information can be more confusing. Try to remember the JS mantra from above- when some event happens (loading the page), I want to make what kind of fetch (get), and I want to manipulate the DOM in what way (render JSON data coming from our API). Initially, I built everything out without OOJS and then refactored, and this can also be challenging, especially with `this` . But once I got the hang of it, it greatly reduced the amount of code required. And finally, with my simplistic MVP handled, my app was not looking too pretty so I used Bootstrap and CSS to make everything look nicer. 

The end result is something I'm happy with but it's incredibly simple so I look forward to adding more functionality to this app in the future. You can check it out [here](https://github.com/elizparisi/hello_beauty_frontend). 



