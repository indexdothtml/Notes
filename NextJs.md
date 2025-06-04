# Next.js Notes

## What is Next.js

Next.js is a JavaScript framework, which is used to create full-stack web applications. It is built on the top of React.

## How it renders the pages.

In React components are compiled/processed in client side like browser and then broswer renders it.
In Next.js components are compiled/processed in server side by default and then generated HTML page is sent to client side, then client side browser renders it.

## How routing works

In React, another library called react-router is used to route to different pages.
In Next.js no any external library is used, Next.js itself handles routing of the pages.
Next.js uses one of App router OR Page router concept to route between pages.
App router OR Page router both uses file-based routing, starts with "app" folder in your project root section.
Next.js looks for this folder to define the route.
For ex - If i want to navigate to http://localhost:3000/about then I will stucture my project folder like this.

```
app/
|__ about/
    |__ page.js
```

page.js is reserved file name by Next.js, it defines the new route "about" is created with the content, whatever defined inside the page.js.
The folder name you choose becomes the route path, here in this case "about"

## page.js file

page.js file is reserved file name in Next.js which defines the new route and its content, Next.js looks for this file name to create new path.

## layout.js file

In every Next.js project there should be one layout.js file as immediate child of "app" folder OR root of "app" folder.
For ex -

```
app/
|__ about/
|   |__ page.js
|__ layout.js
```

layout.js file works as a wrapper to in sibling routes or children routes, whatever you define layout in layout.js file that will wrap around the other route files.

Root layout.js files usually defines the basic starting <html> structure and metadata tags.

## metadata keyword

"metadata" is reserved keyword in Next.js, defines the meta tag in html structure, usually we define inside head tag. This metadata works same but Next.js automatically sets that meta tag inside head tag for us.
For ex - How to define meta tags. Above your Root component in layout.js file export this metadata keyword.

```js
export const metadata = {
  title: "...",
  description: "...",
};
```

## icon, favicon and apple-icon

These are the special reserved file names like other by Next.js to add favicon to your application. It should be created under app/ directory.
For ex - icon.png (this will add favicon to your project)

## @ alice

Next.js setup alice for us named with @ symbol, you can choose any other symbol but by default it is @.
So you can access files from import using @ symbol, this symbol will target project root.
For ex - If you want to access any component which is at same level app directly or at root level.

```js
import Header from "@/components/header";
```

## How to create dynamic route

In any project only static route will be not useful, in some cases like we have to show data which is fetched from database dynamically.
For ex - If you are creating Blog website so you will show different types of blogs.

To show different blogs it is not possible to create endpoint for every blog user adds into our database, like below example. So we can access.
localhost:3000/blogs/blog1
localhost:3000/blogs/blog2 and so on..

```
app/
├── blogs/
│   ├── blog1/
│   │   └── page.js
│   ├── blog2/
│   │   └── page.js
│   ├── blog3/
│   │   └── page.js
│   └── page.js
├── layout.js
└── page.js
```

Instead we create dynamic route, so will define route once and that will be used for all, which comes under that, dynamically handled by Next.js
You define dynamic route by create folder with its name enclosed in square bracket "[slug]".
any name you give inside square bracket considered as placeholder for dynamic endpoints, which user wants to access.

For ex -

```
app/
├── blogs/
│   ├── [slug]/
│   │   └── page.js
│   └── page.js
├── layout.js
└── page.js
```

Here [slug] creates dynamic route with page.js file, [] square brackets indicates dynamic route, so Next.js understands and "slug" the name given to folder, by the way you can give any name, but it will be considered as placefolder and we can access the value under it (the value will be endpoint which user wants to access) using params object, which we are going to see next.

## How to access dynamic route endpoint inside component.

```
app/
├── blogs/
│   ├── [slug]/
│   │   └── page.js
│   └── page.js
├── layout.js
└── page.js
```

Inside [slug]/page.js file, will create component, normally how we create in React same like that. Inside component's props will have access to params object which Next.js provides to us, Next.js passes this params object in every component.
Inside params object the placeholder which we given as a name to the folder will be stored inside params object as a key of the object.
And with the help of params object and the key inside it, we can access value of endpoint which user has entered.

So, if user tries to access localhost:3000/blogs/nextjs-blog
below component will log into the console with the endpoint "nextjs-blog", because when user searched it inside blogs/ endpoint, that got stored inside "slug" key which we given as placeholder under blogs/ endpoint, and that will be accessible using params object's slug key.

```js
//[slug]/page.js

export default function BlogPost({ params }) {
  console.log(params.slug); // nextjs-blog
  return <div></div>;
}
```

Then you can use this endpoint name to query the database and find the data regarding this endpoint and show it to user.
