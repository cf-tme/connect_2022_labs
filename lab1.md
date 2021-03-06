# Lab 1 - Cloudflare Pages
Welcome to Lab 1 at Cloudflare Connect 2022 - This lab will focus on setting up a simple image gallery deployed on Cloudflare Edge using Cloudflare Pages.
By the end of this lab you will have:

- Set up your first Pages project
- Felt the developer experience when using Pages
- Added dynamic functionality with help from Cloudflare Workers/Functions

Build fast sites, in record time. Cloudflare Pages is a JAMstack platform for frontend developers to collaborate and deploy websites.

```{admonition} Learn More about Cloudflare Pages! 
:class: note
Check out the [Cloudflare Homepage](https://pages.cloudflare.com/) to learn more
```

## Clone GitHub Repository
To make things easier we have setup a starter gallery app on GitHub. Lets fork and clone the repository.

Move back up to your home directory (if you are not already there)
``` sh
cd $HOME
```

``` sh
gh repo fork cf-tme/connect_2022_lab1
```
This should create a fork of the starter repository in your gh account and prompt you to clone - enter *Yes*

``` sh
✓ Created fork <github-username>/connect_2022_lab1
? Would you like to clone the fork? Yes
```

Now all the files should be local in your working directory, let navigate into the repo and start coding! 

``` sh
cd connect_2022_lab1
```

## Deploy Pages Project from GitHub Repository
Deploying our GitHub project to pages is as simple as connecting our GitHub account to Cloudflare.

Login to the [Cloudflare Dashboard](https://dash.cloudflare.com)

Select **Pages** on the left hand side and press **Create Project**
![pages](./screencaps/pages-create-project.png)

Select **Connect to Git**

![pages](./screencaps/pages-connect-git.png)

Make sure you are on the GitHub Tab and press **Connect to GitHub**

![pages](./screencaps/pages-connect-github.png)

```{admonition} Authenticate to GitHub
:class: note
If you are not already logged into GitHub in your browser you may be asked to re-authenticate
```
You will be prompted to **Install and Authorize** Cloudflare Pages to your github account, press the button to proceed.

![linkgh](./screencaps/pages_gh_auth.png)

Once connected you will be brought back to the Cloudflare Pages dashboard. 


```{admonition} Re-Select Connect to Git
:class: note
In certain cases you will be brought back to the Project Page where you have to select **Connect to Git** again - if so just press it and then it will bring you into the selection of a repository
```


Select *connect_2022_lab1* on the following page 

![linkgh](./screencaps/pages_gh_repo_select.png)

Once selected you will need to configure build parameters. This is build using React so we will set the following build parameters:

```
Project name - connect_2022_lab1
Production branch - master
Framework preset - Create React App
Build command - npm run build
Build output directory - /build
```

![linkgh](./screencaps/pages_gh_add.png)


Press **Save & Deploy**

```{admonition} Deployment Progress
:class: note
Once started the deployment will take a few moments to complete - you can follow the deployment details to monitor progress of the deployment.
```
Once the deployment has completed you will be presented with a success message as well as a URL to visit your new project Select the **link**.

```{admonition} URL Link
:class: warning
The URL will be at the top of the page, you may have to scroll up to see it
```

![linkgh](./screencaps/pages-success.png)

```{admonition} pages.dev Domain
:class: note
By default new projects will automatically be given a *.pages.dev domain, If you would like to setup custom routes to your own domain you can do that through DNS CNAMEing (or directly in the project settings if your domain nameservers are Cloudflare)
```
When navigating to the link you should see a blurry image gallery.

![linkgh](./screencaps/blurry-img-gallery.png)

Return to the Pages Dashboard and press **Continue to project**
![linkgh](./screencaps/pages-continue.png)


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
This is a fairly simple piece of code but it should just return the string with the current Date and Time in ISO format.

Save the file and return to our terminal window.

In order to push these changes to our project we simply just need to commit and push them to our repository and Cloudflare Pages will automatically rebuild the application.

Before we can commit code we need to ensure that the git CLI has our username setup properly (you will enter the email address for your Github account) 

``` sh
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```
```{admonition} Required Config
:class: Error
If you do not complete the config commands above, the next steps will fail and code will not be committed.
```

To commit and push changes we use standard git commands:

``` sh
git add .
git commit -m "added new time function"
git push
```

```{admonition} Paged Auto-Build
:class: note
By default Cloudflare Pages will rebuild and deploy your application with every push to the github repository, if this is undesirable auto-deployments can be temporarily turned off
```
If we return to the the Cloudflare Pages project we should see that the deployment is in progress - wait for it to complete.

![linkgh](./screencaps/pages-deploy.png)

Once complete we can renavigate to our application URL but this time going to the */time* pages. We should see a very simple readout of the current date and time. 

```
2022-05-06T02:58:04.165Z
```

```{admonition} Building APIs
:class: Note
Functions are great ways to build integrations into other APIs, or even build API endpoints for the web application itself
```

## Creating and Binding KV store
Workers KV is Cloudflare’s globally replicated key-value storage solution. Binding these KV namespaces with your application are what make it truly full-stack - the ability to read and write data dynamically right from Cloudflare's edge.

(content:references:kv)=
### Creating an IMAGES KV Namespace
Our application has been written to read data from env.IMAGES - this means we need to bind our KV namespace to our project with the variable name "IMAGES"

From your Cloudflare account landing page navigate to **Workers > KV** 

```{admonition} Verify Email
:class: Note
If you have not already confirmed your e-mail address for your Cloudflare Account you may be asked to Verify it here before creating any KV namespaces
```

Select **Create Namespace** and enter *IMAGES* in the *Namespace Name* and press **Add**

![kv-name](./screencaps/kv-namespace.png)

```{admonition} Namespace ID
:class: Note
Once  your namespace is created you will be given a Namespace ID - this will be needed later on in Lab 2, so if you plan on joining us for Lab 2 go ahead and take note of this id - you can always navigate back to this screen and grab it later if needed.
```

### Binding KV Namespace to Pages Project ###

Once our Namespace is created we must bind it to our Pages project so that our functions can leverage the data inside.

```{admonition} Look Ahead
:class: Note
We will be using this namespace in Lab 2 to store Image metadata that will then be read in dynamically update our gallery with images that we upload!
```
From the Left hand side navigation pane on the Cloudflare Dashboard select **Pages** then select our project *connect_2022_lab1* 

In the top navigation bar select **Settings** and then **Functions** On the left hand side.

Select **Add binding** under the *KV namespace binding* (under *Production* sub-tab)


![kv-name](./screencaps/add-binding.png)

Enter *IMAGES* in the Variable name and Select the *IMAGES* KV namespace from the dropdown. And press **Save**

![kv-name](./screencaps/save-binding.png)

```{admonition} Manual Re-Deploy
:class: Note
In order for KV binding to take effect we need to rebuild the project - this is generally not an issue when live developing as a git push will force it but in this case to test a few things out we will manually kick off a re-deployment
```
#### Manually Re-Deploy Application ####

To kick off a manual re-deployment we must first select *View build* (in the bottom right) on the latest deployment of our application.

![kv-name](./screencaps/view-build.png)

On the following page select **Manage Deployment** in the top right and press **Retry Deployment**

![kv-name](./screencaps/re-deploy.png)

This will kickoff a manual deployment, give it a few moments to complete.

```{admonition} Page Refresh
:class: Note
If the deployment hangs for more than a few minutes, go ahead and refresh the pages - in rare cases the page will not auto refresh even though the project has completed the deployment.
```

#### Validate KV Binding with API Call ####

Our web application has been build with an API to query KV store for image metadata and use that data to populate the image Gallery on the homepage. This api endpoint can be found at */api/images*.

```{admonition} Empty KV but Homepage still has images?
:class: Note
The Eagle eyed of you may have noticed that even after Binding our KV we still see images on the Homepage - but how? There is no data in the KV store yet. This is because the values have been hardcoded - for now - in a few moments we will be changing this so that the data is populated dynamically
```

To validate our KV namespace has been bound properly we can quickly just navigate to our API endpoint */api/images* in a Browser and should get back an empty array:

```json
{"images":[]}
```
Congratulations your KV namespace has been successfully bound to your Application functions!


### Fill Gallery images with dynamic data from KV ###

Now that our KV store is ready to use we can change our web application to dynamically fill gallery data with Images whose metadata is stored in the KV store. 
To change this behavior we need to go to edit our definition of the gallery images grid at - *connect_2022_lab1/src/components/ImageGrid.tsx* 

Open *ImageGrid.tsx* in your favorite text editor and look at `line:53 - line:119`

``` js
const data = {
    images: [
      {
        id: "8277aeb6-f3fb-445d-43f9-ae710b3ffc00",
        previewURL:
          "https://imagedelivery.net/c_kvDVNdc0jEhXS4gDzgVA/8277aeb6-f3fb-445d-43f9-ae710b3ffc00/blurred",
        name: "hannah-grace-fk4tiMlDFF0-unsplash.jpg",
        alt: "string",
        uploaded: "2021-11-17T06:31:25.203Z",
        isPrivate: true,
      },
      {
        id: "e45bc50e-814f-4f2a-e6ab-d68a3f457500",

        ... cont.
```

Either comment or delete the entire *data* array as we will be replacing it with our simple API call (The "A" in JAM stack) to pull the array of images from the KV store.

Enter the code below in place of the hard-coded image array

``` js
const { data, error } = useSWR<{ images: Image[] }>("/api/images");

  if (error || data === undefined) {
    return (
      <div>
        An unexpected error has occurred when fetching the list of images.
        Please try again.
      </div>
    );

  }
```

To commit and push changes we use standard git commands:

``` sh
git add .
git commit -m "add dynamic image population functionality"
git push
```

If we return to the the Cloudflare Pages project we should see that the deployment is in progress - wait for it to complete.

Once complete we can navigate to our application URL but this time we should see a blank Gallery Page!

```{admonition} Latest Build URL
:class: Note
You will need to get the latest build URL From the Pages Project Dashboard - each build is given a unique URL so that you can see & test the difference between builds. Since we just pushed out git repository there will be a new build and we need to make sure we use the URL for that build.
```

## Generate API tokens for account - Images ##

Before we can upload images or write values to our KV store with the API We need to generate API tokens for our account. 

```{admonition} Images API token
:class: Note
Cloudflare Images is a Paid product, for this lab you will be using a shared Images account with provided API tokens, in the real world you would swap out the Keys for your own.
```

## Generate API tokens for account Workers' Service ##

```{admonition} Account API tokens
:class: Note
Even though we are using pre-populated API tokens for Images, you will need to generate Keys for your specific account so we can write to the KV namespace of your web application.
```

To generate API tokens navigate to the [Cloudflare Dashboard](https://dash.cloudflare.com), login and select your user on the top right and select **My Profile**

![user](./screencaps/select-user.png)

On the left navigation pane select **API Tokens** and press **Create Token**

![token](./screencaps/api-token.png)

Select the **Edit Cloudflare Workers** as the template and press **Use template**
```{admonition} API Token Templates
:class: Note
API token templates are useful when trying to permit scoped access to API based applications, you even have the option to create a custom token with your desired permission level 
```
![token](./screencaps/tokentemplate.png)

In the token settings you only need to set both the *Account Resources* and *Zone Resources* to *Include* *All Accounts* and *All Zones*

![token](./screencaps/zoneaccess.png)
Some **text**!

With the changes made press **Continue to summary** and you should see something similar to below:

![token](./screencaps/tokensummary.png)

Press **Create Token**

On the following screen you will be presented with the the new API token - it is **IMPORTANT* to save this token value in a safe place as it will not be visible again once you navigate away from this page.

In addition to the API token we will also need your accountID this value is simply found in the URL bar in the browser for your Cloudflare dashboard 

**https://dash.cloudflare.com/`<accountid>`**

```{admonition} Before you Continue!
:class: Warning
At this stage you should have 3 values that we will use next to configure and make API calls to Cloudflare 
1. Account ID
2. API Token
3. KV Namespace ID (this was generated when we created the KV Namespace in this [section](content:references:kv))
```
## Upload images and store metadata into KV ##

To simplify uploads and writing data to KV we have written a ready to run python script that can be cloned from GitHub and run.

### Clone Image Upload Repository ###

Move back up to your home directory
``` sh
cd $HOME
```

``` sh
gh repo fork cf-tme/connect_2022_lab2
```
This should create a fork of the starter repository in your gh account and prompt you to clone - enter *Yes*

``` sh
✓ Created fork <github-username>/connect_2022_lab2
? Would you like to clone the fork? Yes
```

Now all the files should be local in your working directory, let navigate into the repo to start coding! 

``` sh
cd connect_2022_lab2
```

### Edit the upload script ###

Open the *upload_images.py* Python script in your favorite editor.
```{admonition} Text Editor
:class: note
VS Code is a versatile text editor that can be launched directly from the terminal using *code <filename>* to install VS Code follow the steps found in the [Documentation](https://code.visualstudio.com/download)
```

In the file editor identify the lines (`lines 11-13`) where you need to change values to reflect your account.

``` python
#CHANGE these are your value from your workers environment
kv_id = "ENTER YOU WORKERS KV NAMESPACE ID"
kv_account_id = "ENTER YOUR CLOUDFLARE ACCOUNT ID"
kv_token ="ENTER YOUR API TOKEN"
```

Before leaving the document take a moment to read through the comments on the code and see whats happening.

The script logic is build in 3 sections:

1. Upload a set of images from the local directory to Cloudflare Images
2. Collect data about uploaded images and structure metadata to be writing to KV Store
3. Write image metadata to KV store

Before we can run the script we need to install a python dependency - this is easy to do with a single command.

``` sh
pip3 install requests
```
```{admonition} pip
:class: note
pip is a python tool that can be used to quickly load python libraries that can be used in code. The requests library is a common import for most API based code as it provides a user friendly wrapper to the built in http request libraries in python.
```
With the dependencies resolved we can simply run our python script!

```sh
python3 upload_images.py
```

We should see success messages come onscreen as images are being uploaded and data is being written to your KV store.

```
uploaded image gallery-images/cat1.jpeg and added KV metadata with status True
uploaded image gallery-images/cat2.jpeg and added KV metadata with status True
uploaded image gallery-images/cat3.jpeg and added KV metadata with status True
uploaded image gallery-images/pup1.jpeg and added KV metadata with status True
uploaded image gallery-images/pup2.jpeg and added KV metadata with status True
uploaded image gallery-images/pup3.jpeg and added KV metadata with status True
```

Once this script is completed our Web Gallery should show these images. Lets confirm! 

#### Confirm values in KV Store ####

From your Cloudflare account landing page navigate to **Workers > KV** 

Select the **IMAGES** namespace

You should see a listing of the images uploaded with the same value "Values stored in metadata" - This is because the valuable information lives in the metadata of the KV pair and is not visible in the UI. 

![token](./screencaps/valueswritten.png)

Now if we return to our Web application URL - `https://<projectname>.pages.dev` we should see a gallery of images!

![token](./screencaps/gallery-complete.png)



```{admonition} Additional confirmation
:class: note
If you want to see the data that has been written into the KV store you can make the `/api/images` call in the web browser and check the data that is being read to fill the gallery on the homepage.
```

```{admonition} LAB 1 COMPLETE! 
:class: note
You have successfully Completed Lab 1 - Cloudflare Pages, now you have a simple web gallery Application that will read data out from a KV store to dynamically populate images.
```



