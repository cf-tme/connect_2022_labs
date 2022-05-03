# Cloudflare Pages 
## testing
Some **text**!
```{admonition} Here's my title
:class: warning

Here's my admonition content
```

step 1 connect GH to pages 


step 2 fork & clone repo

gh repo fork cloudflare/images.pages.dev

y (would you like to clone the fork)


cd images.pages.dev

ls

open up account and add to pages


begin setup 

branch is main

framework is create react app


all others default 

press save and deploy

watch build progress 

once done check the URL

See how new builds are done 

create a new function - pages functions

time.js example 

git add -A to add all files

git commit -m "added new time function" 

git push 

now in the dashboard should see a new deployment in progress! good work 

edit the images ts file

and then go to settings and bind kv namesapce
get started 
and create namespace


call it IMAGES

back to pages and add env for functions

IMAGE = IMAGES

modify the app tsx to include routes to home and setup and admin

run the setup


then do the setup api endpoint to check to see if its working

then do the images listing to see if images are there *should be empty as we have none *

great! 

remove the middleware file because we dont want to deny login - explain what this can be used for if you need! 





npm run build
npx wrangler pages dev ./build --kv KV_NAMESPACE


lab 2 - upload images and now use these for the dashboard vs the original images 

<for returning clone the premade repo and run the setup (step2 repo)>


edit the imagegrid.tsx file to remove the static images so we can use the images that we upload

upload multiple images via the uploader built in

check the metadata written to KV

see the page update


Lab 3 - write the workers js as a function for AB

<for returning clone the premade repo and run the setup (step2 repo), there will already be images in the const data file so they dont need to do any setup either since there is no upload - this will be a clean state page >

clone the repo and write the new worker js file 

check the page on refresh 

check the google analytics logs

Lab 4 
setup pihole as container 
setup cloudflared as upstream proxy

configure policy

