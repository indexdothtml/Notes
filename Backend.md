# Backend notes

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
