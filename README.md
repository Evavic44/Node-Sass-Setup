![node-sass.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640357313284/dYLdh315i8y.png)

# Node-Sass
Environment Setup with Node-sass

This involves installing sass using the <a href="https://www.npmjs.com/" target="_blank">node package manager(NPM)</a>, coupled with a simple NPM script that watches a certain folder where we created our sass files and complies it to regular CSS in the folder we specified. 

![giphy.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633802132439/OPb4yr8j9.gif)
Sounds like mumbo jumbo? 😅 don't worry about it, it'll make sense as we go.

## Step 1. Download and install node
In other to use NPM to install sass, we have to download and install node into our PC. Visit <a href="https://nodejs.org/en/" target="_blank">Nodejs</a> official website to download it. You can choose whichever version of node you would like to install, it doesn't really matter in this case. I went with the long-term support version(LTS), but either one works.

![node.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640077892588/BLVD7zlEo.png)

If you already have node installed, skip this step. 

Now we're done downloading and installing node into our PC, to check if it was installed properly, open up your terminal or command line and type in `node --version`, and hit enter. This should give us the version of node currently installed.

![node-version.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640101905491/nteDDZdNr.png)

## Step 2. Create a package.json file
Since we're installing anything from NPM, we'll need to create a `package.json` file.

To do that, type the following command in your terminal.

```js
npm init -y
```

The `-y` flag is used to skip any questions NPM will ask you and create the `JSON` file with the default settings.
 
This command will create our `package.json` file in the project folder, using the default settings.

![create-a-package.json-file.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640104070410/6yUhiUIRr.png)

## Step 3. Install Node-sass
Now we have created our `package.json` file, we can install Node SASS which will install SASS in the `node-modules` folder, and add it as a dependency in the `package.json` file. 

To install Node SASS, type the following command.

```js
npm install node-sass
```

![node-modules.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640110248987/qIqmkwo76.png)

Now we have successfully installed node-sass in the `node_modules` folder and it is also added as one of the dependencies in the `package.json file`. 

## Step 4. Create an NMP script to run SASS
The next step is to create an NPM script that will allow us to use SASS in our project. To do that, modify

this line:

```js

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },

```

and change it to:

```js

"scripts": {
    "sass": "node-sass -w scss/ -o dist/css/ --recursive"
  },

```

![npm-script.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640111751995/l79kpmJBv.png)

Here's what it looks like in our editor. So let's just go over what this new script is trying to do.

- Node-sass: This is saying run sass.
- `-w` is a watch flag that watches for an SCSS folder (You can name this folder anything you want, but this is where our SASS files will be saved.)
- `-o` dist/css/ --recursive is simply saying, output the compiled SASS code into the dist/css/ folder.

This is a basic page structure of our SASS project, you might choose to structure your project differently, don't forget to update it in your `package.json` file.

## Step 5. Create our respective folders and files
This next step is to create the appropriate files and folders for our SASS project. Which will follow the page structure in the `package.json` file.

- Create two folders, dist, and scss
- Inside the dist folder, we'll have our HTML file, and CSS folder.
- And then finally, our `main.scss` file.


![Node SASS folder structure](https://cdn.hashnode.com/res/hashnode/image/upload/v1640371894181/8BrV4RV2A.png)

## Step 6. Start SASS
After successfully creating the required folders, run the following command to start SASS.

```js
npm run sass
```

This command will constantly watch the SCSS folder and any changes made to the SASS file will be compiled immediately to CSS in the dist folder.

Let's write some code to test this out.

```scss
// sass variable 
$color: red;

body {
  background: $color;
}
```
 
And when we hit save, we get a success message on the command line that says: **rendering complete, saving .css file** which means our sass file will be compiled to regular CSS and give the desired output, which is a red background.

![output-sass.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640274650838/37daLvyYa.png)

So that's how you set up SASS using NPM.

## Issues with Node SASS

![seriously.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1640278170758/PUo4K1Ux4.gif)

If you are using Node Sass in VS code, you might come across this <a href="https://github.com/sass/node-sass/issues/2022">issue</a> that prompts an error in the command line when you save your changes:

```js
Error: Unrelated file
Message: File to read not found or unreadable:
"formatted": "Internal Error: File to read not found or unreadable:
```
 
When this error happens, the changes you made at that time won't be compiled, you will have to keep hitting save until it shows success. 

I took the liberty of researching about this error, and luckily, I found a patch that works just right for it. 
You can read more about it and how to fix it <a href="https://github.com/sass/node-sass/issues/1894#issuecomment-390199128">here</a>.

Too lazy to do that, locate the file `node-sass/lib/render.js` inside your local `node_modules` folder and replace it with this code: https://github.com/marcosbozzani/node-sass/blob/bug-vscode-watch/lib/render.js

This fix detects 'File to read not found or unreadable' and 'File to import not found or unreadable' errors that occasionally happens after a file save in Visual Studio Code when node-sass is running on watch mode.

Those errors happen with 'node-sass (watch mode)', 'chokidar + node-sass' and 'node-sass-chokidar (watch mode)' too.
<a href="https://github.com/sass/node-sass/pull/2386">Node-Sass</a>
