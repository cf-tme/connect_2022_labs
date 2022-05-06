# Cloudflare Workers (WIP)

lets start with A/B testing!

Cloudflare Workers makes it easy to a/b test applications by add custom logic infront of a web application.

In our lab we will be writing a Cloudflare Pages function to act as a method to A/B Test a website.

Also since we will be using free web application we cant use workers


LEts start with cloning the gh repo

lets deploy it with pages 

once deployed let go ahead and check to see the website is just presented with Hello World.

what we will do is create some middle ware 

explain what middleware is 

we will use HTML rewrite to dynamically change the content on the page.

the choice will be random, however you will easily be able to see how you can adapt the code to fill other more complex scenarios


with the repo cloned lets go ahead anad 

cd function

and touch _middleware.js

this is where we will add our logic 

const imageA =
  "https://imagedelivery.net/Upv7Q0MhroCOJHZCX_pZgA/9b0fabf0-8a5d-4d84-29d7-c438eb002d00/public";
const imageB =
  "https://imagedelivery.net/Upv7Q0MhroCOJHZCX_pZgA/2b143d0b-006a-47e7-db0e-ce523edf5300/public";

export const onRequest: PagesFunction = async ({ env, request }) => {
  const response = await env.ASSETS.fetch(request);

  const imageURL = Math.random() > 0.5 ? imageA : imageB;

  return new HTMLRewriter()
    .on("body", {
      element(body) {
        body.append(`<img src="${imageURL}" />`, { html: true });
      },
    })
    .transform(response);
    
};

Go to google and choose any two image URLs for A & B ! 

NOTE you can use the images we uploaded in the pervious lab (if you have them)


if we look at hte code we can see that 

we are using the HTML rewriter function to manipulate the content on the welcome page. 

The random function will spit out a value between 0 & 1 making the odds of each image close to 50% this is perfect for us to be able to see the changes live.


since we want to be able to develop regularly lets go ahead and setup a local wrangler environment to test / debug our page before we push the changes live! 

if you dont have npm installed check out the instructions here: <link to npm>


npm install wrangler@beta
npx wrangler pages dev ./public


should see --- 
> npx wrangler pages dev ./public
🚧 'wrangler pages <command>' is a beta command. Please report any issues to https://github.com/cloudflare/wrangler2/issues/new/choose
Compiling worker to "/var/folders/5x/85cqyfb17tjbx6sxvdgpsk8h0000gp/T/functionsWorker.js"...
Compiled Worker successfully.
Serving at http://localhost:8788/

this will start up a local instance and open your browser you should see once of the images presented! 

great that means the A/B test is working - lets be sure,
open the webpage in an incognito window and navigate to http://localhost:8788/ 

thats it you have used HTML re-writer to create an A/B test the dynamicaly changes the html content to the end user based on a random seed.

Done! 



