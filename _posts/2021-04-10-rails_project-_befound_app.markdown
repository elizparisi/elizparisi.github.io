---
layout: post
title:      "Rails Project- BeFound App"
date:       2021-04-10 23:07:10 +0000
permalink:  rails_project-_befound_app
---


I have to say this was not easy, even with Rails being intuitive. I thought about what I wanted to do for my project and something immediately came to mind. But after starting and trying to get the relationships to work and meet the requirements, I realized I had eyes bigger than my current coding capabilities. So, then I thought about something that would be useful, fun, and of course, hit all the requirements. I finally decided on app for making recommendations. 

The user journey would be: users can sign up, once they're signed up, in the future they'd login with their credentials- after signup or login, a user can navigate to a form to create a new recommendation or they can view all the recommendations made by both them and other users. The authorized user can edit or delete the recommendations they created. And finally, users can create comments on recommendations made by other users as well as view all comments for a particular recommendation. 

I tried not to get overly complicated and keep things to three models: `user.rb, recomendation.rb, comment.rb` (comments would be my join table).  Trying to figure out the best way to get a join table was a little tricky, especially after starting to write out my relationships in notes. To be honest, thinking about join tables give me a little bit of a headache but fortunately one of the instructors had mentioned the easiest way of thinking about it is your join table will be whatever has two `belongs_to` relationships. Great! Comments it is. My next issue popped up immediately- how was I suppsed to write out my `has_many` relationships in my user model? I'd have two `has_many, through: :comments`. Not good. Again, one of the instructors pointed out a way to rename the second `has_many` so instead I'd code it out as `has_many :commented_recommendations, through: :comments, source: :recommendation`. If you want to learn more about this, I suggest this [article](https://www.theodinproject.com/paths/full-stack-ruby-on-rails/courses/ruby-on-rails/lessons/active-record-associations).

I thought I wanted to use [devise](https://github.com/heartcombo/devise) and make things easier (it's definitely some amazing witchcraft) but I changed my mind because I wanted to have control over everything and try to better grasp some of the concepts devise just handles for you. 

I hit a bit of a hiccup with my nested routes. What I was aiming for was `recommendations/:id/comments` and I had some trouble getting the recommendation id to come through (hint: hidden_field in the form). I thought I had everything right and was get a no method error 'post' so I thought I was not able to create new comments. I changed some code and was still getting an error. So I carefully combed through my code and I had a big, typo in my validations! (Always spell check people). My form with the addition of the hidden_field worked correctly: 

`<%= form_for([@comment.recommendation, @comment]) do |f| %>

  <%= f.hidden_field :recommendation_id, :value => @recommendation.id %>

  <%= f.label :title %>
  <%= f.text_field :title %>
  <br>
  <br>

  <%= f.label :content %>
  <%= f.text_area :content %>

  <%= f.submit %>

<% end %>`

And once that was resolved a new error said that my recommendation id was not found when I hit the back button, nil was coming up for one of the attributes that was previously working fine. I dropped my database and ran my migrations again, same error when I tried to edit or hit the back button.  After again combing through my code, I found my routes were out of order in my recommendations controller. Order counts! 

Then I moved on to my scope method which I thought would be more difficult than it was- I went with order `scope :alpha, -> { order (:name)}`. [Here](https://api.rubyonrails.org/v6.1.3/classes/ActiveRecord/Scoping/Named/ClassMethods.html) is some good documentation on scope methods and writing them correctly. 

While going through the coursework I, personally, found the concept of omniauth a little overwhelming. There are added gems:
`gem 'omniauth'
gem 'omniauth-rails_csrf_protection'
gem 'omniauth-google-oauth2'
gem 'dotenv-rails'`
Then there's the .env file, secrets (not to mention the possibility of accidentally pushing those to Github if you forget to include your .env in the .gitignore file), a callback route. So I waited until I was mostly complete to do this piece. I started out trying to use Google which was not easy to navigate, especially with OAuth 2.0. I couldn't really find many articles that covered all the steps for what was needed for the new updates. I kept getting all kinds of various errors. It said my client id was incorrect which it definitely wasn't since I copied it from Google. So I switched to Github, thinking a developer friendly site would have very clear instructions on how to implement them as a third party sign in.  But surprisingly I found that to be more confusing and I got to the Gihub login but I kept getting logged in to Github's actual site not my app. So after trying a few more things, I came across this amazing [video](https://www.youtube.com/watch?v=9pD0uXLI5uE) that helped me figure it out! And like all the tutorials and articles I read during this process said, once you have one down it will be a lot easier in the future to add more. 

And with omniauth complete, that brought this rollercoaster ride to an end. Rails has a lot of magic behind it and it’s very intuitive but it’s definitely good to have a working understanding of why it does some of things it does for you. The [documentation](https://guides.rubyonrails.org/) was a huge help to me. You can view my complete project [here](https://github.com/elizparisi/rails_project). Thanks for checking it out! 
