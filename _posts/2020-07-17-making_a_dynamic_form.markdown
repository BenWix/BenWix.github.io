---
layout: post
title:      "Making a Dynamic Form"
date:       2020-07-17 23:56:37 +0000
permalink:  making_a_dynamic_form
---


While designing my Javascript project for the fulltime software engineering bootcamp, I ran into a daunting problem that I desperately wanted to figure out. To give a little background on the project, it was a weather app that would suggest different things to do based on the current weather conditions. So a user could submit a new activity and have it be associated with a bunch of different weather conditions. The problem I ran into, was trying to make a clean way for the app to have one form that would allow for a unique amount of weather conditions when an activity was submitted. 

This is what my form ended up looking like 

![](https://imgur.com/4C965C8)

![](https://imgur.com/3cu1FRRhttp://)

So you can see that each time a button is pressed an indentical set of input fields are added to the form. This works great on the user end and is quite dynamic to allow the user to submit any number of weather conditions they could want. 

Figuring out how I would grab this data and deal with it was a little more complicated. Each of the conditions form fields were in identical div tags. So it was easy to grab them, but then I had to get to each set of data. 

```
<div class="conditionsForm">
                        <label>Weather Condition</label>
                        <select name="condition" id="condition-dropdown">
                            <option value="any">Any Condition</option>
                            <option value="clear">Clear</option>
                            <option value="cloudy">Cloudy</option>
                            <option value="raining">Raining</option>
                            <option value="storming">Storming</option>
                            <option value="misting">Misting</option>
                            <option value="snowing">Snowing</option>
                        </select>
                        
                        <label>Min Temp</label>
                        <input type="number" name="minTemp">
                        
                        <label>Max Temp</label>
                        <input type="number" name="maxTemp">
                    </div>
                </div>
```

So to get all of the different conditions form I could simply 

```
let conditionsForms = document.querySelectorAll('.conditionsForm')
```

This leaves me with a node list that I will have to deal with. While I can iterate through the nodelist and look at each form individually, I am not able to use querySelector on these elements to pull out the correct element. So the solution I came to was getting the children of each of the items from the nodelist, and pulling out the corresponding values. 

```
conditionsForms.forEach(form => {
            let newCondition = {}
            newCondition["weather"] = form.children[1].value
            newCondition["min_temp"] = form.children[3].value ? form.children[3].value : -100
            newCondition["max_temp"] = form.children[5].value ? form.children[5].value : 200
            conditions.push(newCondition)
        })
```

While this does use some magic numbers, they are only used once in the code so it is not dry. It could be more adaptable in case the div were to change in the future. But at the moment, I feel as if this solution smoothly accomplishes the goal of creating the dynamic form I was looking for 

