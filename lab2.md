# Lab 2 - Cloudflare Images
Welcome to Lab 2 at Cloudflare Connect 2022 - This lab will focus on Uploading and Delivering Images via Cloudflare Images
By the end of this lab you will have:

- Uploaded images to Cloudflare via the API
- Used Image variants
- Seamlessly integrated Cloudflare Images and Pages


Cloudflare Images provides a straightforward, end-to-end solution to cost-effectively build and maintain your image infrastructure. Store, resize, and optimize images at scale using one unified product.

```{admonition} Learn More about Cloudflare Images! 
:class: note
Check out the [Cloudflare Homepage](https://www.cloudflare.com/products/cloudflare-images/) to learn more
```

## Guided Hands-On Experience
Cloudflare Images is a subscriptions based product, and to ensure you can experience all that Cloudflare Images has to offer this lab will be a guided experience.

The steps bellow can be executed when the instructor directs you to them. 

```{admonition} Running Scripts 
:class: note
During this lab you will be running scripts from within the repo in the "scripts" folder, these scripts will be using node, if you have not setup node please follow the steps [here](./npm.md) to learn more
```

## Clone Repository

To make things easier we have setup a starter gallery app on GitHub. Lets fork and clone the repository.
Move back up to your home directory
``` sh
cd $HOME
```

``` sh
gh repo fork netgusto/imagejam.net
```
This should create a fork of the starter repository in your gh account and prompt you to clone - enter *Yes*

``` sh
✓ Created fork <github-username>/imagejam.net
? Would you like to clone the fork? Yes
```

Now all the files should be local in your working directory, let navigate into the repo to start coding! 

``` sh
cd imagejam.net
```

## Prepare Repo for script execution

To run the scripts during the Hands On section you will need to first setup the environment, run:

``` sh
npm install
```

```{admonition} Initialization
:class: warning
Before running the command ensure that you are in the root directly of the repository - otherwise this will fail
```

## Upload Images

To upload images we will first need to define our api key as a system environment variable. 
```{admonition} API Key
:class: warning
The API Key will be provided to you during the session by the instructor
```
**MacOS / Linux**

``` sh
export CF_IMAGES_EVENT_KEY= ...
```

**Windows**

``` sh
$Env:CF_IMAGES_EVENT_KEY = ...
```

Once the environment variable is set you can run the upload script - you can do this with either the built in script or using `curl`

### Upload via Script ###

**Local Image File**
If you have an Image file locally you would like to upload you can use the following command:

``` sh
node scripts/handson/upload.js --file path/to/local/file.png [--id some-custom-image-id.png] [--metadata '{"tag": "connect"}']
```

**Image URL**
If you know an image URL that you would like to upload you can use the following command:

``` sh
node scripts/handson/upload.js --url https://example.com/image.png [--id some-custom-image-id.png] [--metadata '{"tag": "connect"}']
```


### Upload via cURL ###
**Local Image File**
If you have an Image file locally you would like to upload you can use the following command:

``` sh
curl -X POST https://imagejam.net/connect-upload/ \
    -H "Authorization: Bearer $CF_IMAGES_EVENT_KEY" \
    --form 'file=@/path/to/local/file.png' \
    --form 'id=some-custom-image-id.png' \
    --form 'metadata={"tag":"connect"}'
```

**Image URL**
If you know an image URL that you would like to upload you can use the following command:

``` sh
curl -X POST https://imagejam.net/connect-upload/ \
    -H "Authorization: Bearer $CF_IMAGES_EVENT_KEY" \
    --form 'url=https://example.com/image.png' \
    --form 'id=some-custom-image-id.png' \
    --form 'metadata={"tag":"connect"}'
```


```{admonition} LAB 2 COMPLETE! 
:class: note
You have successfully Completed Lab 2! Congratulations on uploading and optimizing your Web Application with Cloudflare Images.
```
