### Javascript Development Environment (House) 
https://github.com/ARWL2016/ps-javascript-dev-env 

#### Testing Styles
- Unit - tests a single module or function 
- Integration - tests interactions between modules 
- UI - automated UI testing 

#### Key Frameworks 
- Mocha - most popular
- Jasmine - has a built in assertion library
- Jest - wrapper on Jasmine designed for React

#### Test Runners 
- Karma - runs tests in actual browser  
- JSDOM - simulates the browser when testing Node (in memory dom)

#### Other Libraries 
- Chai, Expect, Should - very similar assertion libraries 
- Cheerio - query the DOM using JQuery syntax (JQuery for the server)

#### Continuous Integration 
- Travis (Linux)
- Appveyor (Windows)
--- 

#### Test Scripts 
- "test": "mocha --reporter progress buildScripts/testSetup.js \"src/**/*.test.js\"" - escape double quotes 
- "test:watch": "npm run test -- --watch"

####Setting up Tests 
1. `npm install mocha chai jsdom --save-dev`  
2. Create a `buildScripts/testSetup.js` file. This contains test config information - use ES5 only here   
3. ES6: register babel to transpile before mocha runs in `testSetup.js`  
4. Webpack: disable webpack features which mocha does not understand, such as importing css  
5. add an npm test script: `"test": "mocha --reporter progress buildScripts/testSetup.js \"src/**/*.test.js\""`. The `--reporter progress` flag defines the type of output. Then we list the setup file and the files to test. 
6. Create test files in the same folder as the file to be tested: `file.test.js` 
7. import the assertion library: `import {expect} from 'chai';`  
8. describe our tests  

####Testing the DOM with `jsdom`  
1. install packages as above  
2. import `jsdom` and `expect` into our test file  
3. To bring in our `index.html` for testing, we do not use import (I think because js can only import js files). Instead, use the node `fs` module, and use `const index = fs.readFileSync('./src/index.html', "utf-8");` inside the test function.  
4. To use `jsdom`, we pass the index.html into the jsdom environment: `jsdom.env(index, function(err, window) {}`. 
5. The window param in the callback then gives us the root of the DOM. We can now access any element: `const h1 = window.document.getElementsByTagName('h1')[0];` Remember that the js dom traversal methods will return an array of elements.  
6. In an async function (ie one with a callback), remember to pass in `done` and then call `done()` at the end to tell mocha it is safe to evaluate the tests.  
7. Calling `window.close()` saves memory  

---
####Continuous Integration with TravisCI and AppVeyor 
1. Travis tests our app on Linux and AppVeyor on a Windows platform. They allows us to test our app automatically on commit on another machine. Both work in the same way:
2. Create a `.travis.yml` and an `appVeyor.yml` file to configure the servers. 
3. Commit changes and push to Github 
4. Navigate to the projects page https://ci.appveyor.com/projects/new or https://travis-ci.org/ and select the app and run build. 
5. The CI server will download dependencies, run the build and run any tests, then show some stats and any error messages.  
