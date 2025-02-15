# Express.js Route Handler Missing Error Handling for Invalid User ID

This repository demonstrates a common error in Express.js route handlers:  the lack of proper error handling for invalid input.  Specifically, the code attempts to parse a user ID as an integer without validating its format, potentially leading to application crashes or unexpected behavior.

## Bug Description
The `/users/:id` route attempts to retrieve a user based on the ID provided in the URL parameters.  It directly parses `req.params.id` as an integer using `parseInt()` without verifying if it's a valid integer.  If the ID is not a number (e.g., a string, or null), `parseInt()` will return `NaN`, causing the `.find()` method to fail unexpectedly and potentially throwing an error, or returning `undefined` leading to the `user` variable being null, resulting in an unexpected 404 status code, or even crashing the server. 

## Solution
The solution adds input validation to ensure the `userId` is a valid integer before attempting to use it.  It handles cases where the ID is invalid, returning appropriate error responses to the client.

## How to reproduce
1. Clone this repository.
2. Run `npm install` to install dependencies.
3. Run `node bug.js` to start the server.
4. Send a GET request to `/users/abc` (invalid user ID).
5. Observe the error or unexpected behavior.
6. Run `node bugSolution.js` and repeat step 4 to see the fixed version.
