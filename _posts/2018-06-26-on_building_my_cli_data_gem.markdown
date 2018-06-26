---
layout: post
title:      "On Building My CLI Data Gem"
date:       2018-06-26 05:46:19 +0000
permalink:  on_building_my_cli_data_gem
---


<p> After going over the requirements I settled on making something movie related. I checked out the features and HTML for a few different movie sites then decided to make an app to find movies that will be released next week. Since Rotten Tomatoes links for individual movies followed a predictable pattern, had the most details on a movie, and workable markup it became my scrape target. I submitted my ideation and fought the impulse to get started. </p>

<p> Once the ideation acceptance email came through I used Bundler to setup a rubygem called MOTW (Movies Opening This Week). I started trying to scrape Rotten Tomatoes Opening This Week list. Even though I could see the data in my browser nothing I tried could touch it. Eventually I found out that Javascript content can't be pulled with the combo of open-uri and Nokogiri I was using. I tried to make headless browsers work but every one I found had requirements that were incompatible with the Ruby Gem format. So I decided to find another movie website to scrape a list from and ended up with IMDB. </p>

<p> I wish at this point I would have taken a step back and rethought the overall picture. Scraping two seperate websites added difficultly and a lot of time down the road that was ultimately wasted. But back to the process, I went through and came up with scrapes for both IMDB's In Theaters list and any specific movie in Rotten Tomatoes. This was the start of my second misstep. I got so caught up in making my idea that I forgot in the ideation I said my first feature would be the movie list, I ignored the recommendation against scraping everything, and the fact that all the examples of what this project should look like pulled significantly less data then I was starting off with. </p>

<p> At this point I created a Movie class with 15 instance variables for all of the different attributes. Other than just housing data it was capable of taking the return values from scraper (a hash for single movies and an array of hashes for the movie list) and turning them into new Movie objects. This was probably the smoothest part of the entire project and is the one example of code I got almost entirely right the first time. </p>

<p> Now that I could create objects I did some testing. Right off the bat I noticed that some movies were missing information so I had to add a lot of conditionals to make scrapes handle this. In order to avoid turning the Scraper class into a giant mess I used a lot of short cuts to save lines. The biggest mistake of the entire project happened here. By not deciding to reduce how much I was grabbing I ended up almost doing three times more work than necessary (on managing movie information). Since I have to handle scraping it, getting it into a useable format, and displaying it I sank the majority of the projects time trying to support my initial dataset. </p>

<p> Creating the CLI was the catalyst for change in my process. I got fed up with trying to split every possible action into seperate methods and the code I wrote to make Scraper small was difficult for even me to read. Luckily in a technical one on one Dakota explained to me that single responsibility principle doesn't mean you have to have one method to display options to the user, one to validate, and one to act on their input but that if the code to handle this interaction won't be repeated in can be in a single function. As long as this function doesn't handle anything else. We also went through my Scraping class code and the best solution he could come up with is splitting the list and movie scrapes out into seperate methods. </p>

<p> This reinvigorated me and freed me from the trap I had created. As I worked through filling out the CLI I got over trying to make my original vision work and cut the amount of information I was scraping in half. This allowed me to refactor the project significantly and to refocus on creating the minimum viable product. 

>>> potentially remove this later <<<

At the time of this writing I currently need to finish testing the CLI to call the programming part of the project done, but all of my connections to Rotten Tomatoes are timing out so I may be getting blocked. 
We'll see </p>





