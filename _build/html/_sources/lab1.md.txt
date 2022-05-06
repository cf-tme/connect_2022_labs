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

## Clone GitHub Repository
To make things easier we have setup a starter gallery app on GitHub. Lets fork and clone the repository.

``` sh
gh repo fork cf-tme/connect_2022_lab1
```
This should create a fork of the starter repository in your gh account. Follow the fork with a clone

``` sh
gh repo clone <yourgithubusername>/connect_2022_lab1
```

Now all the files should be local in your working directory, let navigate into the repo and start coding! 

``` sh
cd <yourgithubusername>/connect_2022_lab1
```

## Deploy Pages Project from GitHub Repository
Deploying our GitHub project to pages is as simple as connecting our GitHub account to Cloudflare.

Login to the [Cloudflare Dashboard](https://dash.cloudflare.com)

Select **Pages** on the left hand side and press **Create a Project** and select **Connect GitHub**

![pages](./screencaps/pages_gh_setup.png)

```{admonition} Authenticate to GitHub
:class: note
If you are not already logged into GitHub in your browser you may be asked to re-authenticate
```
You will be prompted to **Install and Authorize** Cloudflare Pages to your github account, press the button to proceed.

![linkgh](./screencaps/pages_gh_auth.png)

Once connected you will be brought back to the Cloudflare Pages dashboard. Select *connect_2022_lab1* on the following page 

![linkgh](./screencaps/pages_gh_repo_select.png)

Once selected you will need to configure build parameters. This is build using React so we will set the following build parameters:

```
Project name - connect-2022-lab1
Production branch - master
Framework preset - Create React App
Build command - npm run build
Build output directory - /build
```

![linkgh](./screencaps/pages_gh_add.png)


Press **Deploy**

```{admonition} Deployment Progress
:class: note
Once started the deployment will take a few moments to complete - you can follow the deployment details to monitor progress of the deployment.
```
Once the deployment has completed you will be presented with a success message as well as a URL to visit your new project Select the **link**.
```{admonition} pages.dev Domain
:class: note
By default new projects will automatically be given a *.pages.dev domain, If you would like to setup custom routes to your own domain you can do that through DNS CNAMEing (or directly in the project settings if your domain nameservers are Cloudflare)
```
When navigating to the link you should see a blurry image gallery.

![linkgh](./screencaps/blurry-img-gallery.png)

Terrific! Congratulations you have successfully deployed a custom application using Cloudflare Pages.

## Using Functions with Cloudflare Pages

Functions enable you to run server-side code to enable dynamic functionality without running a dedicated server. With Functions, you can introduce application aspects such as authenticating, querying databases, handling form submissions, or working with middleware.

```{admonition} Learn More about Functions! 
:class: note
Check out the [Cloudflare Docs](https://developers.cloudflare.com/pages/platform/functions/) to learn more
```
For our simple gallery application we are going to create a new function that will simply return the time when navigating to the *time* page for our application.

Returning to our command line lets change to the *functions* directory

``` sh
cd functions
```

Whatever name we give this file is going to be the path in our url. Lets create a new file called *time.js*

``` sh
touch time.js
```
Now open that file in your favorite text editor.

```{admonition} Text Editor
:class: note
VS Code is a versatile text editor that can be launched directly from the terminal using *code <filename>* to install VS Code follow the steps found in the [Documentation](https://code.visualstudio.com/download)
```
In the file enter the following code:

```js
export const onRequest = () => {
  return new Response(new Date().toISOString())
}
```


Some **text**!
```{admonition} Here's my title
:class: warning

Here's my admonition content
```



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



