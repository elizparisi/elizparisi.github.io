---
layout: post
title:      "React/Redux Project - Booket Lists"
date:       2021-05-28 19:08:22 +0000
permalink:  react_redux_project_-_booket_lists
---


This is it, I’ve come to the final project. This one was tough, it required the most work and the most knowledge. This build tested me immensely. I hit quite a few roadblocks but as always, I looked at my resources for solutions. I definitely recommend this [one](https://reactrouter.com/web/guides/quick-start), it got me out a route and render jam. 

As I mentioned in previous posts about project builds, I stick with what I know and love- beauty and books. So no surprise here that I chose an app idea that integrates one of those, this time it was books. While I was brainstorming, I thought of something I wanted, actually needed- a single place to note all the books I want to read. I know, I know- Goodreads, well, this app is a little less complicated…for now. I wanted a user to be able to come to the app, create a reading list and add their must-reads to it.

At first, I was just going to have a book model and call it a day but then I thought, wouldn’t it be better to categorize your never-ending to-be-read list into similar groupings? Yes! Then, of course, I started thinking bigger, maybe too big. Scratch that, definitely too big. I was going to include a user model, which would then require emails and passwords and auth. So I met my ideas in the middle and decided on lists and books. Two models: list `has_many :books` and book `belongs_to :list`. Perfect. 

The backend was created using a Rails API and was pretty simple to get started on since it hadn’t been too long since using this method for the JS project. Create a Rails API by using `rails new` command followed by name of your API and adding the `--api` flag after the name to ensure that Rails only includes what’s necessary for API usage. Make sure to uncomment gem ‘rack-cors’, which allows Cross Origin Resource Sharing (CORS). Add the `gem ‘active_model_serializers’` to the gemfile. Serialization is responsible for converting objects into data types understandable by javascript and front-end frameworks. 

Inside config/initializers/cors.rb file uncomment this code: 
```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

For the client side (frontend) we’re building in React and Redux. To start, the project requires us to use create-react-app, read more [here](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app). Run the following: 
`npx create-react-app <name> and npm install redux && npm install react-redux`

Then I created my folders for components, containers, reducers, actions. If that seems like a lot, it’s because it is. React has a lot of moving parts and you’re always importing or exporting something. Remember to export your components at the end and import whatever you need from it’s respective folder/file. Even more importantly, name things consistently and correctly otherwise you’ll have a hard time tracing errors to their exact source. One thing I did love about coding with React is when you run `npm start`, you know immediately when it can’t compile. 

I chose to set up my store right away. This is not the entirety of index.js but the necessary things for creating the store are below: 

```
import React from 'react';
import ReactDOM from 'react-dom';
import { createStore, applyMiddleware, compose } from 'redux'
import thunk from 'redux-thunk'
import { Provider } from 'react-redux'

const composeEnhancer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const store = createStore(listReducer, composeEnhancer(applyMiddleware(thunk)))

ReactDOM.render(
  <Provider store={ store }>
    <Router>
      <App />
    </Router>
  </Provider>,
  document.getElementById('root')
);

```

I didn’t want to get everything set up and then have to go back and implement Redux. We use Redux middleware (thunk) to respond and modify state change. The middleware lets you call action creators that return a function instead of an action object.

I know I still have so much to learn about React and Redux. Overall, this experience tested my knowledge and my patience. Once these concepts really sink in, I’ll definitely be revisiting this project and adding more to it. 
