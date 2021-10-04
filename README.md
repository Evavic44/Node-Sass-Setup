# Node-Sass-test
Environment Setup with Node-sass


# Error
```js
Internal Error: File to read not found or unreadable:
```

This fix detects 'File to read not found or unreadable' and 'File to import not found or unreadable' errors that occasionally happens after a file save in Visual Studio Code when node-sass is running on watch mode.

Those errors happen with 'node-sass (watch mode)', 'chokidar + node-sass' and 'node-sass-chokidar (watch mode)' too.
<a href="https://github.com/sass/node-sass/pull/2386">Node-Sass</a>

# Fix
locate the file `node-sass/lib/render.js` inside your local `node_modules` folder and replace with this code:
https://github.com/marcosbozzani/node-sass/blob/bug-vscode-watch/lib/render.js
