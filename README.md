# Deploying Bootstrap HTML into Production

I started developing with HTML and Javascript back in the late 1990's but stopped long before the likes of AngularJS and Bootstrap came on the scenes.  There was certainly no SCSS or npm.  When I came back to HTML in 2021, I was aware of the likes of webpack and JS frameworks likes Angular, and happended upopn Bootstrap as a means to write great responsive web sites.  I followed the instructions on their "Getting Started", cloning their template web site, and succeeded in creating my own.  Everything was going well until I needed to deploy.  The instructions told of an npm run script called build, which didn't exist.  Searching the internet including Stackoverflow offered little help apart from the knowledge that I wasn't alone in this challenge.

After many hours rephrasing search queries on Google for knowledge of how to deploy bootstrap, I gave up.  It was time to start again.  At this point I tried one last try, searching for a solution and from a different angle.  I began to search for generic npm based web build tools.  I came across Parcel via a Mozilla web page [https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management), which it turned out was supported by Bootstrap, albeit via a knowledge base article [https://getbootstrap.com/docs/5.0/getting-started/parcel/](https://getbootstrap.com/docs/5.0/getting-started/parcel/).

Whilst this README presents much of the information found in the URL references above, it is a consolidated Step-by-Step version consolidated into a single document.

## Step 1: Dependencies

To complete the steps you will need the following.  I am going to assume that you already have node installed.  If not, node can be installed from [https://nodejs.org](https://nodejs.org).
  
* Parcel
* PopperJS
* Bootstrap
  
For those of you wanting to managing your projects inside of a source control like Github, and perhaps auto-deploy too, you will also need
  
* git
  
## Step 2: Setup your working folder

We begin by creating a folder where we want to keep all the project files and initialise the npm project.  For the sake of discussion I am going to call my folder my-web-project.

```console
mkdir my-web-project
cd my-web-project
npm init
```

NPM will ask a series of questions (It is okay to accept the defaults) before creating a package.json file, which will contain all the details NPM needs, your information, dependencies, etc that the build project will need.
  
## Step 3: Install Parcel
  
```console
npm install --save-dev parcel
```

With Parcel installed, all the build and deployment tools are now available.  The next step is to setup Bootstrap.

## Step 4: Install Bootstrap

Bootstrap has a number of dependencies, so we'll start with those prior to adding Bootstrap to the project

```console
npm install @popperjs/core
npm install bootstrap
```
