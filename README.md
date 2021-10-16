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

NPM will ask a series of questions (It is okay to accept the defaults, except one - see below) before creating a package.json file, which will contain all the details NPM needs, your information, dependencies, etc that the build project will need.
  
When npm init asks for the entry point, which will default to index.js, enter

```console
entry point: (index.js) src/index.js
```
  
## Step 3: Install Parcel
  
```console
npm install parcel-bundler
```

If you follow the instructions on the Parcel website itself (i.e. npm install parcel), this will not work.  When you try to run a project, it will not compile index.js, rather it will treat it as a normal Javascript file.  Errors will be thrown such as when one tries to use import, which is not allowed in a regular web Javascript file.  Parcel-bundler is the correct package and designed to compile JS resources as part of the build.

With Parcel installed, all the build and deployment tools are now available.  The next step is to setup Bootstrap.

## Step 4: Install Bootstrap

Bootstrap has a number of dependencies, so we'll start with those prior to adding Bootstrap to the project

```console
npm install @popperjs/core
npm install bootstrap
```

# Step 4: Setting up your project files

As a minimum, both Parcel and Bootstrap require two files for your index web page, index.html and index.js.  To keep everything tidy, we'll create a sub-folder called src and these two files.  Use the following templates to seed each files respectively.

```console
mkdir src
cd src
```

Create the html file, index.html.

```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <script src="./index.js"></script>
  </body>
</html>
```

Create the js file, index.js.

```js
// Import all plugins
import * as bootstrap from 'bootstrap';
import "bootstrap/dist/css/bootstrap.css"; // Import precompiled Bootstrap css
```

I am going to import everything from Bootstrap, but checkout their online documentation for more options [https://getbootstrap.com/docs/5.0/getting-started/javascript/](https://getbootstrap.com/docs/5.0/getting-started/javascript/).

# Step 5: Create the CSS file (SCSS)

Start by creating a new subfolder in the root called scss and create a file within it called custom.scss.

```console
mkdir scss
cd scss
```

Now create the file custom.scss within the scss folder and copy the following text into it.  Save the file.

```js
// Custom.scss

// Include any default variable overrides here (though functions won't be available)
// Include all of bootstrap
@import "../node_modules/bootstrap/scss/bootstrap";
```

Check out [https://getbootstrap.com/docs/5.0/customize/sass/#importing](https://getbootstrap.com/docs/5.0/customize/sass/#importing) for all possible scss options.

# Step 6: Edit the package.json file adding scripts to run and build

All the basic editing is complete.  The final step is to modify the package.json file with the commands necessary to build and run your bootstrap based projects.
Back in the root folder edit package.json and add the following script declarations.

```js
"scripts": {
  "dev": "parcel ./src/index.html",
  "prebuild": "npx rimraf build",
  "build": "parcel build --public-url ./ ./src/index.html --experimental-scope-hoisting --out-dir build"
}
```

# Step 7: How to run and build your project

Congratulations, you are now ready to run and/or build your project.  To run a dev copy of your project, use the following command:

```console
npm run dev
```

And to build your project, use the following command.  Run will automatically build a project and in all cases, the output of the build it saved to the folder called Dist found in the root directory of the project.

```console
npm run build
```
