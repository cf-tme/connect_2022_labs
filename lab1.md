# Cloudflare Pages
Welcome to Lab 1 at Cloudflare Connect 2022 - This lab will focus on setting up a simple image gallery deployed on Cloudflared Edge using Cloudflare Pages.
By the end of this lab you will have:

- How to set up your first Pages project
- The developer experience when using Pages
- How to add dynamic functionality with with help from Cloudflare Workers/Functions

Build fast sites.In record time. Cloudflare Pages is a JAMstack platform for frontend developers to collaborate and deploy websites.

```{admonition} Learn More about Cloudflare Pages! 
:class: note
Check out the [Cloudflare Homepage](https://pages.cloudflare.com/) to learn more
```
## testing
Some **text**!
```{admonition} Here's my title
:class: warning

Here's my admonition content
```

clone the github repository 

they are goiing to then deploy to pages 

navigate to the page! the application works! 

now lets write a function that lets us execute some code - 
new file for time - and then git add . git commit -m "new file" git push

then add a new function file to learn how functions work - return 

boom now if we look at pages we see that there is an ongoing deployment! awesome it autodeploys it with the git push

if we got to /time you can see it returns the time - pretty cool! 

now functions are really powerfull for creating integrations and api endpoints - in the interest of time we have built most of these for you.

when using the API endpoints there is often a need to repeatedly refernce stored variable data - this is where we can use KV to persist variables. IN this example we will be using it to store details about the images in our gallery! 

create a new KV namespace called "IMAGES"

note down the ID as we will need it in later labs! 

once the space is created go to settings and go to function - edit binding with variable name IMAGES and kv namespace set to the Images namespace we created 

now we will need to rebuild the project so lets do that! 

once done 


there are a few api endpoints we can test if you go to /api/image - lets see the result 

hmm we it looks empty, but thats good, we havent uploaded any images yet.


now you might be wondering ... ok well then why were there images on the homepage! 

good eye - this is because we have actually hardcoded the image data for the homepage - so lets go and clear it out and change it to read image data from our KV store 

- delete the const data and uncomment the useSWR to get the data out of the kv store! this will make a call to the api/images endpoint and pull the data and present it.

now if we return to our homepage - look at that an empty gallery!  - unfortunatley that is all the time we have for lab 1 but if you join us for lab 2 we will upload some cute images hosted in cloudflare and serve them up with our application

at this stage you should ahve an empty pages on the home screen :) now lets add some pictures 



