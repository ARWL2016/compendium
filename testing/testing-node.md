### Complete Node (Mead)
- Link: https://github.com/ARWL2016/node-tests
- Libraries: Mocha, Expect, Supertest, Rewire 
- `"test": "mocha **/*.test.js"` 
- `"test-watch": "nodemon --exec \"npm test\""`
- Nb. The test using rewire and expect spies is not clear from this module. 

#### Testing the Server 
- Mocha runs globally
- libraries: expect and supertest (as request) libraries are imported 
- method: the request is mocked with supertest: `request(app).get('/')` and then expect is used for assertions  
- `done` is passed into the `it` callback and passed to `end` 

#### Testing a Utilities File (with async)  
- libraries: expect 
- This test file simply imports a group of functions and asserts the result with expect
- It also mimics an async test. 
- It does this by passing the whole assertion into the function to be tested as its callback, 
and then calling done(). The test dives into the belly of the function like an interepid explorer. 