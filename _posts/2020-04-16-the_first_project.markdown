---
layout: post
title:      "The First Project"
date:       2020-04-16 09:15:35 -0400
permalink:  the_first_project
---


  Starting work on the first Flatiron Project was an incredibly exciting and slightly nerve wracking time. I was bouncing around in my head, making sure I knew everything I needed to accomplish the project. I was working to push hard throught the curriculum to get to the project on time or early. I wanted to make sure I was set up for success. 


  Thankfully, I was able to get to the project a little early and could put in some good work the weekend before project week, this started to bolster my confidence a little bit. The more time I had, the more likely I would be to succeed. When I dove into the project I wanted to make sure that it would not only make a good project to demonstrate my skills, but that it would also push me in some of the areas that I was weak. Every opporunity, can be an opportunity to turn a weakness into a strength. I identified my weakness before I dove in, so I knew I needed to find a project that would utilize gems more heavily. I found an API that was about rock climbing routes (climbing is my all time favorite activity), so I figured this could be a great fit for me. Looking at the big hurdles I would face in the project, I initially identified three.

1. To access the API, I would need to get that latitude and longitude of a location.
2. To get the latitude and longitude, I would need to use a gem I hadn't used before. Geocode.
3. The API required a private key, so I would need to learn how to make a .env and .gitignore file

  

   This tasks felt daunting in the moment, but knowing that they would start to round me out as a better overall programmer, I was excited to take on the task. I was pleasently surprised with how smoothly some of these steps went. It only took me one afternoon to decipher the geocode gem and get it working with the API. It took a bit more head scratching and google searching to get the .gitignore and .env file to function, but now that I have done it once, I will be totally prepared to do it next time. 
	 
	 The biggest technical hurdle other than the three mentioned above was gettng a complex sorting method to work. It was simple to sort all of thr route objects by name and by star, but sorting by grade was a different story. Climbing grades have a pretty abstract order. They all start with "5." then there is more after the ".". When there is 1-9 after the ".", each number can have a + or -, but when the number is 10 or higher, they are typically followed by "a,b,c, or d". So some examples would be "5.10b", "5.12d", "5.8", "5.9+". Climbing grades are not decimals, they are two integers seperated by a period, so a "5.11" is a "five eleven" not a "five and eleven hundredths". It is a common and understandable misconception that a "5.6" is more than a "5.12", but this is not true when it comes to climbing grades. Countried outside of the USA, use grading systems that are a bit more intuitive. So my first attempt had me first, split the grade, so I was only looking at the material after the period, then sorting that. 

```
grades.sort_by{|grade| grade.split(".").last}
```

This somehwat worked, the probelem was since there was a combination of numbers and letters, the value had to be a string. And in string talk "10" is less than "6". So It would sort everything "5.10a" and above quite well, but then everything that was a single digit grade, would be falsely after it. This meant I needed to split again and then turn the number into an integer, sort by that, then sort by the letters that followed. Unfortunately when I did this, I had more problems with edge cases. Sometimes climbers would grade something "5.10b/c" or a grade that was supposed to have a letter would have a "+" like "5.11+" instead of "5.11d". Also, sometimes grade had more information like a "5.11b PG13" (a PG13 signifies a route that is particularly dangerous). So I forsaw that there were still going to be issues. I concluded the only way around was to create a class constant, that held an array of all of the possible grades in order. I quickly created an array that had all of the grade possibilities in it and then got to coding. So I needed to sort the grades by their index in this constant. The other thing I did, is split the on the input, I could only use the characters after the "." since I knew everygrade would start with "5.". So my grades now looked like "10b", "9+", "12c PG13", or "11b/c". So the code that finally successfully sorted my grades was.

```
grades.sort_by{|grade| GRADE_ORDER.index(grade.split(" ").first)}
```

I needed to throw in the final split to account for any other extraneous information that would be on the grade. This finally sorted all of my grades, no matter what the outlier. I had to make quite a length array for GRADE_ORDER, but thankfully, ruby is great at making long repetitive arrays for me. Sorting by grade was definitely the longest and most difficult puzzle I had to tackle in the project. 
	 
   The rest of the project build process was a very fun challenge, that got me excited to see what I will build next. Little puzzles that I needed to solve kept the build fun and spicy. I am relatively happy with how I solves all of the problems, but I am excited to see the new ways I will learn to tackle these things in the future.
	 
	 That's one project down, and many more to go. And I couldn't be more excited about that.
