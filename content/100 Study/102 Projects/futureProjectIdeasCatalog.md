---
title: Catalog of ideas for future projects
draft: "True"
---
- Web Server
	- **Idea**: Not to reinvent the wheel but to learn more about the wheel HTTP is just text, a protocol for browsers to send and receive information from servers. The steps in completing this project are outlined here:
		- Create a bare-bone HTTP server that uses sockets.
		    - Implement error-handling for a _graceful exit_
		- Create a [HTTP parser](https://en.wikipedia.org/wiki/Recursive_descent_parser) eventually
- **No hardware component**, unless there's a way to get that in here. Generative AI games - essentially, from the art to the story to the choices presented to the user, AI creates every component of it. Might require a starting prompt from the user but after that, everything is created by AI.
	- So, we create a basic Game Layout with some controls to move right/left and the rest is AI?
- What if we rip-off Big Hero 6 and build one of the inventions they had in the movie? "A swarm of tiny microbots that can link together in any configuration using a neural transmitter" - HTN provides eye-tracking technology and also this thing: [Neurosity Crown](https://my.hackthenorth.com/hacker/hardware/items/?search=Lottery) so we could try to link this up with some hardware.
- Kind of going on the movie theme, it's cool to replicate a bunch of movie characters?
	- TARS from interstellar, EVE from Wall-E, etc..
	- **Integrate Viam with ChatGPT to create a companion robot.** Article on it: [https://docs.viam.com/tutorials/projects/integrating-viam-with-openai/](https://docs.viam.com/tutorials/projects/integrating-viam-with-openai/ "https://docs.viam.com/tutorials/projects/integrating-viam-with-openai/")
- Computer Vision project, not necessarily hardware based - but as you are doing your grocery trip, a camera to check for freshness of vegetables and see which one is a good one to buy
	- Sometimes with like fruits or veggies, there are important markers to look out for to see if they are ripe or not?
- Not really hardware AGAIN, but what if we have a AI look over terms and conditions and highlight out the most concerning things they are asking for. So, try and prioritize them into what seems dangerous, not really, and just filler text?
- **Hardware maybe? IoT** Like how if you copy something on your iPad, you can paste that onto your mac - something like this utility but accessible for all kinds of computers?
- **Not sure about hardware again?** Something that helps with taking photos of other people. An AI-guided photo taker to take the most appealing photos of other people/nature etc.
	- So, for example, if the subject is too close or too far. If there's a scenic photo somewhere nearby to your current location etc.
	- Also, add hardware by allowing it to move and then take the best photos?
- No hardware: Given the rise of AI, there's probably already an AI tool that exists out there. Some kind of way to connect AI tools with people who would want to use them? Like a database of some sort.
- AR Driving simulator - especially for people who are new to driving, along with some cheap hardware to make the experience better?
- Okay, I'm delirious now but you know that meme where the dog says 'Let me do it for you' and then goes down the pringles can to get a pringle. Basically, hardware replication of this meme because apparently this is what judges want to see :)
- Holographic interface: sort of builds on the whole Raspberry PI + mirror project actually and also no idea how to actually implement this :)
	- Running and subway surfers?
Okay, time to just write whatever comes out of my head and hope this makes sense or sounds like a good idea:
- A software application that can look at a resume and job description and figure out if they are good for each other or not (some kind of ranking system)
- A hardware-software application to make beverages just the right way (the same amount of ingredients every time, temperature checks and things like that?)
- When we lose our TV remote or other small items, it's annoying. So maybe a cheap solution, not like the AirTag expensive and easy to add to any device?
- AI models thrive off of data and collecting that data can be painful. So, maybe a way to help fix this. If it's to do with taking images, maybe some kind of images will be required for that.
- What if we have a robot that goes in your garden and then, identifies plant and figures out what's a weed/poisonous and marks it.
- Trans-scriber? Like listen into conversations and make translations, the suggested texts and ease out on language barriers
- When you are shopping and you don't have access to fitting rooms. You can have something sort through clothes? idk
- A terminal utility that can provide you with a full overview of CPU usage, and other stats with just one command 
- Business model that revives dead companies, connect communities to make them open-source, free projects?
- AI-powered wildlife recognizer.
- Facial recognition, scan through all of social media to find you
- Take a picture of a lecture room, apply facial recognition and take attendance essentially?
	- match faces with students in the picture?
rPi, sensors, breadboard materials, camera & an even better webcam?
- data logging from the front of your home, wildlife data? suspicious people lurking around, trespassers + measure humidity of area, like a weather station
	- {security system or nature route}
- Guess the word that I'm dying to say but can't figure out what it is
	- Voice assistant 
voice-detection to which celebrity you sound like




React Native Mobile Application (iOS, Android) with Python backend. 
- Is Python the best for mapping utilities? This seems like a good library to have: https://github.com/googlemaps/google-maps-services-python

**Features**
*What are the features we want?*
- Difficulty levels: So, maybe we can try factoring in terrain into the equation and then seeing how hard a particular route is. Might not work always and figuring out how to do this is a challenge (hence, a want)
- Can we integrate this with Apple Watch for example? So, it's easier to navigate on the run?
- Weather conditions - like if there is rain scheduled within the time of the run, or if there's sever weather warnings (not too hard to be honest - just need a weather API)
- Allow for conversion between km/miles or any other metric system related stuff

*What are the features we need?*
- Version 1: Given both a start point and end point, suggest a scenic route to walk/bike/run?
- Version 2: Given a start point, figure out a random location that is also a specific distance away..
- Version 3: Given just a start point, going a circular route.

- Data user enters: 
	- Distance they want to travel 
	- Time travel (using average human speed)
	- How they are travelling? (Running/Walking/Cycling/Driving)
- Have a timer that shows how long you are on track.. we should try and track location data/time

- So, at the end of the run,
	- We can give out stats: time + distance is a good start.
- Authentication --> Guest account, and if you make a profile, data persists. 
	- So, we use firebase.
- History. So, things we should keep in mind about running experience:
	- So, ability to reselect an old path. Save+share a path basically...
	- 
