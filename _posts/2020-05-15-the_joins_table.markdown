---
layout: post
title:      "The Joins Table "
date:       2020-05-15 21:14:35 +0000
permalink:  the_joins_table
---


While making my sinatra project, I ended up having 4 different models that were related. The project was a watchlist tracker for birding enthusiasts. So a user would be able to create an account, then log everybird they see on a date at a particular location. It's a simple CRUD model, just with several models. The following shows the schema for my database.

User model:
   Has many Watchlists
	 has many locations through watchlists 
	 has many birds through watchlists 
	 
Watchlist model:
    Belongs to User
		Belongs to location
		Has many birds 
		
Location model:
   Has many Watchlists 
	 Has many birds Throgh watchlists
	 Has Many users through watchlists 
	 
Bird model:
  Has many Watchlists 
	Has many Users through watchlists
	Has many Locations through Watchlists 
	
	
So there are many has many-has many relationships through out my project. For all of them except the bird watchlist relationship, the watchlist will act as the joining method. The only missing watch table is the one joining birds and watchlists. 

![](https://i.imgur.com/WdnMhCY.jpg)

So as can be seen in the above chart, I had to add one more table that would handle the joins table beween birds and watchlists. Since birds can be seen my many users at many areas, there obviously needed to be a has many has many relationship between the two. 

The watchlist table worked very well, since it acted as the main avenue that a user would use to post, it also acted as the main interface btween which all models interacted. Every model was created when the watchlist model was created excluding the user. It turns out the joins table ended up being a great way to relate ALL of my models, and not a giant hurdle, like I had originally thought it may be.


