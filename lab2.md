# Cloudflare Images
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
Some **text**!

for those of you returning from previous lab go ahead and SKIP to this section


clone the lab 1 complete repository 

create a KV namespace called Images 
note the ID 

got to pages and deploy the application 

bind the namespace in settings 

then re-build the projkect

the url for api/images should return empty

and the homepage should be blank



SKIP 

clone the lab 2 github repository 


ensure that python is installed (write the steps for prereq)


open up the image upload file in your favorite editor

now we need some value 
find this from when we created the KV namespace - if you forgot go to workes → kv namespaces and select IMAGES there shoudld be an ID there

kv_id = "ENTER YOU WORKERS KV NAMESPACE ID"

this can be easily found in the URL after "dash.cloudflare.com" that value is your account ID 

kv_account_id = "ENTER YOUR CLOUDFLARE ACCOUNT ID"

we need to generate a new API token - lets do that 


kv_token ="ENTER YOUR API TOKEN"


now that we have all of our values filled in lets take a look at the code -

the first part is uploading images to cloudfalre pages 
>> since we are using a common images account 

we only only have one image variant in this account but its important to note that you can define any number of variants just by creating a variant and changing the URL 

once we do the upload we are then writing the image metadata to KV - this will be in the right format for our homepage to show the new images we upload 


- lets go ahead and ruyn it! 


terrfici we should ahve gotten an aoutput that looks something like: 
uploaded image gallery-images/cat1.jpeg and added KV metadata with status True

uploaded image gallery-images/cat2.jpeg and added KV metadata with status True

uploaded image gallery-images/cat3.jpeg and added KV metadata with status True

uploaded image gallery-images/pup1.jpeg and added KV metadata with status True

uploaded image gallery-images/pup2.jpeg and added KV metadata with status True

uploaded image gallery-images/pup3.jpeg and added KV metadata with status True



this means that our images were uploaded and the metadata was written it should look something like below! 


Now if go back to our homepage and navigate to /api/images 

this should return a full list of images 
and our homepage should now have a full array! 

AWESOME! congratulations you create a FULL stack application with Workers, KV, and IMAGES! 
