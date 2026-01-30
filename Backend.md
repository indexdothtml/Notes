# Backend notes

## Project Setup
1) Create node js project with `npm init`.
2) Create folders - `/public/temp` (to store uploaded files temporary), `/src` (Main file and other backend code goes here.)
3) Add .gitignore file. (You can auto generate the contents of gitignore file from online tools available.)
4) Create `/.env` file to store environment variables.
5) Inside `/src` folder create three files (or as per requirement you can add more) - `index.js/server.js` (contains code related to establishing connection with db, our http webserver and environment variable configurations.), `app.js` (Contains express middlewares that requires to process request from user, Different routes), `constant.js` (Contains global constants).
6) Inside `/src` create required folders - `/controllers` (Contains app controller functions like login, logout etc.), `/db` (Contains database connection file which mainly contains functions to connect or disconnect database.), `/middlewares` (Contains app middlewares), `/models` (Contains database schemas for different collections), `/routes` (Contains all enpoints/routes catagorized with router), `/utils` (Contains utility functions).
7) Nameing of files inside folders such as `/controllers`, `/db`, `/middlewares` etc. are given as per convension, for ex - inside `/controllers` folder `<fileName>.controllers.js` same like this for all other folders.
8) In `package.json` dev scrip should be added like. `"scripts": { "dev": "nodemon -r dotenv/config src/index.js" }` "-r" flag is "required" flag it includes the package first before starting server, in this case dotenv/config which is required to configure environment variables. (required at the time of development only also prerequisite is nodemon).

## Rules
1. Never use 'g' or 'global' flag in regex expression while validating email or password using regex.
2. Sending request with 'form-data' requires middleware that can handle 'multipart/form-data' like 'multer' package. 'form-data' request can handle files, which requires special package ex- multer.
3. Sending only text data, then just sending request with 'raw json' is fine.
4. Unused parameters in controllers or middlewares functions such as 'req, res, err, next' can be replaced with _ (underscore), suppose if 'req' is not used then it can be written like this (_, res, err, next)
5. Calling `.exec()` on a query in Mongoose does not trigger `pre('save')` middleware. The `pre('save')` hook only runs when you explicitly call `.save()` on a document instance, not when executing queries with `.exec()`.
6. Everytime you generate access token and refresh token for same user the signature will be different, because in payload part `jsonwebtoken` package automatically adds issuedAt (iat) and expiresAt (exp, if you have given expiresAt option to jwt function) and issuedAt time changes everytime you call it and expires at depends on issuedAt so both values changes, causing generating different signature everytime, but this is good for security purpose.
7. `findByIdAndUpdate` method of mongoose gives some useful options to use. like `new: boolean` by default `false` but if becomes `true` gives new object after update instead of old object before update. `select: string` allows you to select which fields from document you want or which fields you want to avoid, (use minus sign for avoiding). `lean: truthy` if becomes `true` then return document from query will be only user entered data document and not mongoose document. More will be on https://mongoosejs.com/docs/api/model.html#Model.findByIdAndUpdate()
8. Important cookie options to set while sending response are `httpOnly: boolean` which flags the cookie to be accessible only by the web server. `secure: boolean` which marks the cookie to be used with HTTPS only. More will be on https://expressjs.com/en/5x/api.html#res.cookie
9. Access token are short lived ex - from 15 min to 1 day
10. Refresh token are long lived ex - from 30 day to 1 year
11. Access token are used to access protected resources of application without entering credentials again and again for every http request to protected resource. This increases user experience.
12. Refresh token are used to cycle access token or refresh access token or generate new access token when it expires.
13. Its important to send access token and refresh token as response to user while setting it simultenously in user's browser cookies. Sending access token and refresh token as a response helps non browser clients or non web clients like mobile apps to save it and send it using Authorization headers. Setting it in client's browser cookies helps server to access it any time, because browser sends cookies with every http request that helps client to authorize itself, it is automatic so client don't need to send header explicitly.
14. Standard for Authorization header `Authorization: Bearer <token>` prefix Bearer is a standard to send authentication token, server understands this Bearer prefix means "anyone has access to this token are authorized to access protected resource."
15. Point to note that Headers can be logged by proxies or monitoring tools, so Refresh tokens are best to send via httpOnly cookies where broswer send them automatically or if mobile device then by "request body" and "not by request headers in authentication header".
16. Access token can be send by authentication header, they are short lived so less risk.
17. It is best to cycle Access as well as Refresh token, while cycling Access token when it expires. When Access token expires, Refreshing it with Refresh token, making new refresh token with access token helps to avoid replay attack.

### Error Handler - Globally

1. Signature: Must have 4 arguments → (err, req, res, next) so Express knows it’s an error handler.
```js
//error.middleware.js

import APIError from "../utils/apiErrorHandler.js";

const errorHandler = (err, req, res, next) => {
  return res
    .status(500)
    .json(
      new APIError(
        "SERVER ERROR",
        "Internal Server Error",
        500,
        process.env.NODE_ENV === "development" ? err.stack : ""
      )
    );
};

export { errorHandler };
```
2. Order matters: Register it after all routes so it catches errors from anywhere.
```js
//app.js

//...
app.use("/api/v1/user", userRouter);
// When there is a request on http://localhost:8000/api/v1/user then request will transfer to userRouter, from there further it will handle.
// Like http://localhost:8000/api/v1/user/register register endpoint will get handle in userRouter.

// Error handling global middleware.
// Should be defined at the end after all routes.
app.use(errorHandler);

export default app;
```
3. Default behavior: Without a custom handler, Express sends back an HTML error page.
4. Error object (err): Standard JS Error → has .name, .message, .stack. You can add custom fields like .status.
5. Stack traces: Show in development for debugging; hide in production for security and cleaner responses.
```js
//.env

NODE_ENV=development
```

### Identify the need of indexes.

1. Run a Query Without Index
Suppose you have a users collection and you run:
```js
db.users.find({ email: "alice@example.com" }).explain("executionStats")
```
2. Look at the Output
The explain() output is detailed, but the key parts are:
- `winningPlan` → shows how MongoDB executed the query.
  - If you see `"COLLSCAN"`, it means a collection scan (no index used).
  - If you see `"IXSCAN"`, it means an index scan (index used).
- `executionStats` → shows performance metrics:
  - `nReturned`: number of documents returned.
  - `totalDocsExamined`: how many documents MongoDB had to check.
  - `executionTimeMillis`: how long the query took.
 If `totalDocsExamined` is much larger than `nReturned`, the query is inefficient and needs an index.


