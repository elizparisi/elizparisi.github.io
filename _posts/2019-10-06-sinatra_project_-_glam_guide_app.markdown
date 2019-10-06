---
layout: post
title:      "Sinatra Project - Glam Guide App "
date:       2019-10-06 18:58:13 +0000
permalink:  sinatra_project_-_glam_guide_app
---

As I approach project mode, I seem to experience a slowdown. I know it should be the opposite, that I should be ready to tackle it head on and breeze through things. But with a big undertaking ahead, knowing that I need to implement everything I've learned up to this point and create something of my own, it can feel a little overwhelming. To combat this feeling I decided to join a project planning session way before I was ready to start. Going over the requirements and the initial setup process was very beneficial. I also joined a lot of Sinatra study groups! The live project builds were SUPER helpful and so thorough. Overall, I felt a lot more prepared for this project than the previous one. 

I started brainstorming what I wanted to do for my app. I wanted to create something I was interested in and that I thought would also be helpful to others. Everyone loves beauty products and tools but finding the perfect one and making sure it works like advertised can be annoying. So I decided to create the Glam Guide, a place for users to go to rate and review beauty products and tools. I hope that it will be similar to getting a product recommendation from a best friend. The app requires a user to signup, once they're signed up they can login, create a product, rate and review it.

I also (mostly) followed Ayana's SinatraOOO Guide. Thanks Ayana! So before even writing any code I mapped out my user story (see above) and wireframed my models, attributes and associations. It was helpful seeing this on paper and how things would associate with each other. 

Finally, it was time to get coding! I used the Corneal gem - huge shoutout to Jen and Ayana for recommending this. It made the intial setup so much easier. You can read about it [here](http://https://github.com/thebrianemory/corneal). After installing the gem with `gem install corneal`, you just need to type `corneal new APP-NAME` and it scaffolds for you - magical! With the bones of my app now done, and a github repo made, first up were my models. 

I used Corneal to generate my models by typing `corneal model NAME` I did this to build a user model, a product model and a review model. Make sure your model files are singular - if you pluralize it when using Corneal it should throw an error at you. My associations looked like this: the user model `has_many` products and `has_ many` reviews, the product model `has_many` reviews and `belongs_to` a user, and the review model `belongs_to` a user and `belongs_to` a product. Now with the migrations, models and associations all done I moved on to the controllers. 

I didn't use `Corneal` to build my controllers, I wanted to test my knowledge limits and stretch to the edge of my capabilities. If you do use `Corneal` it lays out your routes for you. In addition to the `ApplicationController`, I decided on three other controllers. I would need a `UsersController`, a `ProductsController` and a `ReviewsController`. Make sure not to forget to mount your other controllers in `config.ru`, like I did the first time. This is what the `config.ru` file should look like when you've successfully mounted your controllers: 
```
    require_relative './config/environment'
    if ActiveRecord::Migrator.needs_migration?
      raise 'Migrations are pending. Run `rake db:migrate` to resolve the issue.'
    end
    use Rack::MethodOverride
    # use OtherController1
    # use OtherController2
    run ApplicationController
```

Before tackling the other controllers, in ApplicationController make sure to enable sessions, and set them to secret: `enable :sessions`
`set :session_secret, 'super_secret_beauty_session'`
Then on to my `UsersController`, first we need to inherit from the `ApplicationController` by typing `class ApplicationController < Sinatra::Base`. Here I built out routes for /signup, /login and /logout. Then I built the corresponding forms in the users views- a form to signup a user up, a form to enter an existing user's login info. I flipped back to the `ApplicationController` to create a few helper methods that will save some redundant code:
  helpers do

```
    def current_user
      @user ||= User.find_by_id(session[:user_id])
    end

    def logged_in?
      !!current_user
    end

    def authorized_to_edit?(product)
      current_user == product.user
    end
  end
```

I used full CRUD (Create, Read, Update, Destroy) in my ProductsController which allows users to create new products, read the index of products, read an individual product, edit their own products and delete their own products. I added authorizations to protect user's info from being edited or deleted by another user. Only logged in users have access to create a product, edit, delete and create a review. This image from a previous lab is a good visual explanation of CRUD: 
![](https://i.imgur.com/4o3Qtrv.png)

I used restful routing-a RESTful route is a route that provides mapping between HTTP verbs (get, post, put, delete, patch) to controller CRUD actions (create, read, update, delete). This table provides a nice visual: 
![](https://miro.medium.com/max/2692/1*pv-pmMPED1XuTtWlHd6b1g.png)

Finally, I wrapped things up with the `ReviewsController` with just a get /reviews/new route and a post /reviews route. A corresponding form to enter the new review info. This caused a bit of trouble for me. I know a review had saved to the database, I used tux to locate the data. It actually saved a few times because there was an error that while running shotgun kept asking to resubmit the form. Whoops. After a bit of back and forth trying to make it work, I joined a session with Jen Pazos (lifesaver!) and she helped me figure out I need some nested routes. We completely reworked my `ReviewsController`, now the routes were correct and working, we also cleaned up the reviews views as well. 

I was hoping to have finished this project in a little less time than I did but I feel like my limits and knowledge were definitely tested and once everything was working like it should, it was really great feeling. I already have plans on future styling and possibilities to expand the app. With all that said, Rails here I come! 


