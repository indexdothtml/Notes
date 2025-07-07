# Frontend with react notes

## What is CORS

CORS is "Cross Origin Resource Sharing" a security feature implemented by browser to allow or restrict accessing resources from different domain.

For ex - If you have front-end application hosted on https://example-frontend.com and you have backend API which is hosted on https://api-backend.com

If that backend domain is not allowing this front-end domain to access its resource, then browser blocks the request of front-end.

How it works in detail ->

I have front-end application running on https://example-frontend.com domain.

I make a request to backend api which is running on https://api-backend.com domain.

```js
fetch("https://api-backend.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

Before browser send actual request to backend, first it sends preflight request to backend with OPTIONS method.

Browser sends preflight request to backend with information like OPTIONS method, Host (api URL), Origin (front-end Domain OR requesting domain) and Access-Control-Request-Method (which HTTP method used while requesting)

```
OPTIONS /data HTTP/1.1
Host: api-backend.com
Origin: https://example-frontend.com
Access-Control-Request-Method: GET
```

Then browser checks preflight request and decide to allow or reject based on its set rules (rules like which domain, method, headers are allowed)

If Browser allows the preflight request then it sends response with 200 status code, Access-Control-Allow-Origin (the allowed requsted origin) and Acess-Control-Allow-Methods (allowed method)

```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://example-frontend.com
Access-Control-Allow-Methods: GET
```

After preflight request is approved actual request is sent to backend

```
GET /data HTTP/1.1
Host: api-backend.com
Origin: https://example-frontend.com
```

Then server responed with data

```json
{
  "data": "Here is the data you requested."
}
```

NOTE - CORS is to protect backend resource from unknown front-end domain who is trying to access that resource.

It can also protect user from requesting unknown backend, at that point backend not allow, the request and brower rejects the user's request.

CORS are rules enforced by browser, so every backend should implement it, if any backend did not have any CORS rules, browser just reject the request for that backend.

If any malicious backend allows all domain to access its resource like `Access-Control-Allow-Origin: *` then at this case if front-end access this resource broswer won't block it, becuase it is valid rule set by backend, but here intent is malicious.
To protect the user from this, front-end should sanitize every response which we get from backend to avoid sql-injection type attack. Also front-end can enforce "Content Security Policy" to allow only trusted backend response.

```html
<meta
  http-equiv="Content-Security-Policy"
  content="default-src 'self'; connect-src 'self' https://trusted-backend.com;"
/>
```

How to set rules for CORS ->

Headers availble to set rules for CORS are:

1. Access-Control-Allow-Origin (only from domain the requests are allowed, \* for all domains)
   for ex -

```
Access-Control-Allow-Origin: https://example-frontend.com

Access-Control-Allow-Origin: *
```

2. Access-Control-Allow-Methods (only http methods are allowed, \* for all methods)
   for ex -

```
Access-Control-Allow-Methods: GET, POST, PUT

Access-Control-Allow-Methods: *
```

3. Access-Control-Allow-Headers (only http headers are allowed, \* for all headers)
   for ex -

```
Access-Control-Allow-Headers: Content-Type, Authorization

Access-Control-Allow-Headers: *
```

The rules are set from backend side, for example in express.js server

```js
const express = require("express");
const cors = require("cors");
const app = express();

const corsOptions = {
  origin: "https://example-frontend.com", // Allow this origin
  methods: "GET,POST", // Allow these methods
  allowedHeaders: "Content-Type,Authorization", // Allow these headers
};

app.use(cors(corsOptions));

app.get("/data", (req, res) => {
  res.json({ data: "Here is the data you requested." });
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

## Virtual DOM in React, how it works? and its benefits

Virtual DOM is in-memory representation of actual DOM, it is helpful for updating actual DOM without interacting with actual DOM directly.

How it works:

1. Initially Virtual DOM will be created, it is the exact same as actual DOM.
2. Whenever state updates, new Virtual DOM gets created in memory, the current Virtual DOM will be compaired with previous version of Virtual DOM. Finding the difference with the help of Diffing algorithm.
3. At last only the updated DOM element gets repainted in actual DOM.

Benefits:

1. Virtual DOM, reduces the effort of updating the actual DOM, which can be slow and inefficient.
2. With the help of Virtual DOM, only the specific part which is changed, that gets updated and not entire DOM gets repainted again.
3. Virtual DOM, makes update faster.

## How Reconciliation algorithm works

In React, reconciliation is the process through which React updates the DOM to match the desired state of the application. It ensures efficient updates by minimizing direct DOM manipulations, which can be costly in terms of performance.

React's Reconciliation algorithm updates the UI efficiently with the help of different steps.

1. Virtual DOM:

Initially Virtual DOM of actual DOM is created in memory, next time whenever the state updates, A seperate Virtual DOM is created for that.

2. Diffing Algorithm:

The comparison happened between new Virtual DOM with the previous one, with the help of Diffing alogorithm it finds the changes to update the DOM.

3. Batch phase:

React batches all the changes and update the UI, it reduces number of DOM updates.

3. Commit phase:

At last React updates actual DOM, matching with Virtual DOM, only updates the part of element that actually changed, instead of full actual DOM repaint.
For lists React uses 'key' prop which accepts unique keys for list items, this helps React to keep track of each list items for updating.

## Difference between class component and functional component

1. Syntax: class component uses JavaScript's class syntax introduced in ES6, function component uses JavaScript's function syntax.

2. Syntax Complexity: class component is generally considered as complex to write then function component.

3. State management: class component manages its own state using this.state and function component manages its state using useState hook.

4. Lifecycle methods: class component manages its lifecycle using method like componentDidMount() and componentDidUpdate() and function component manages its lifecycle using useEffect hook.
