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

## Link component from Next.js

Link component from "next/link" is used to define hyperlink to other resource like pages.
It is similar like anchor tag in HTML but adds some functionality to cache the pages and gives the feel of single page application.
If you are adding any hyperlink to another page use "Link" component instead of anchor tag.

For ex -

```js
<Link href="/about">About page</Link>
```

## Difference between image import and usage in React and Next.js

In React, if you want to use image you just import it store it in any name and then use it inside the "src" attribute of "img" tag.
For ex -

```js
import MealIcon from "./assets/meal.png";

<img src={MealIcon} alt="meal" />;
```

In Next.js, if you want to use image you need to extract "src" key from object.
Next.js create an object of imported image and you need to access property of image to show it.
For ex -

```js
import MealIcon from "@/assets/meal.png";

console.log(MealIcon);
```

If you try to print this in console it will look like this

```js
//console.log(MealIcon) will show below object.
{
  src: '/_next/static/media/meal.8ae1685e.png',
  height: 600,
  width: 600,
  blurDataURL: '/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fmeal.8ae1685e.png&w=8&q=70',
  blurWidth: 8,
  blurHeight: 8
}
```

So, In Next.js if you want to show image on screen you need to access "src" property from this object and pass it to "src" attribute of <img> tag.

```js
<img src={MealIcon.src} alt="meal" />
```

NOTE: This is for the information, but we don't use this approch to show image on our website, instead we use <Image /> component from "next/image", which Next.js provide to us.

## Styling Next.js project

https://nextjs.org/docs/app/getting-started/css

There are different methods of styling the Next.js project.

1. globals.css file
   With globals.css file you can add style globally to all pages. This file will be created inside app/ directory.

2. {fileName}.module.css file
   This file is used to add css styles with scoped to component.
   The styles defined with this file name will be scoped to perticular component, It will be scoped to component in which we are importing this style.
   This file creates the object of style and we can access styles with the properties of that object.
   For ex -

```js
// app/blog/blog.module.css

.blog {
  padding: 24px;
}
```

```js
// app/blog/page.js

import styles from "./blog.module.css";

export default function Layout() {
  return <main className={styles.blog}></main>;
}
```

You can check how we are accessing styles from the file like "styles.blog" and this style and all the styles from module.css file will be scoped to this component only after that import. So if you add same name style in other file and import it in other component it will not create name conflict and overwrite the style.

3. Tailwind CSS

You can use Tailwind CSS to style the pages.

https://nextjs.org/docs/app/guides/tailwind-css

## Image component in Next.js

like Link component Next.js provide Image component to show the images on our website.
Image component extends the HTML <img> tag to automatically optimize the image for better performance as per the browser support.
Image component provides lots of functionality you can see all the props which we can pass to the Image component. https://nextjs.org/docs/app/api-reference/components/image
But more useful one are src, alt, fill, priority etc.

Basic use

```js
import Image from "next/image";

export default function Page() {
  return (
    <Image
      src="/profile.png"
      width={500}
      height={500}
      alt="Picture of the author"
    />
  );
}
```

Or if you are importing image then you can pass imported image object directly without accessing src propertiy from it. Image component will use that imported image object to optimize and infer the dimentions of image as well.

```js
import Image from "next/image";

import MealsIcon from "@/assets/meals.png";

export default function Page() {
  return (
    <Image
      src={MealsIcon}
      width={500}
      height={500}
      alt="Picture of the author"
    />
  );
}
```

Image component also convert image into best supported image by the browser, for example if client opens the website in chrome then Image component convert it into ".webp" format instead of using ".png". So ".webp" is most supported by chrome browser.

Instead of lazy load if you want image to be load with priority then set priority prop.

```js
import Image from "next/image";

import MealsIcon from "@/assets/meals.png";

export default function Page() {
  return (
    <Image
      src={MealsIcon}
      width={500}
      height={500}
      alt="Picture of the author"
      priority
    />
  );
}
```

## "use client"; in Next.js

Next.js can run component in server-side as well as client-side, some of the features used in components only runs in browser, is it made for client-side and not server-side like "useState" and "useEffect" hook so you have to tell Next.js to compile that file on client-side using `"use client";` at top of the file. Although Next.js still after adding "use client" it first pre-compile that component in server-side then on client-side.

## usePathname hook in Next.js

`usePathname()` hook in Next.js provides the current active url path.
It is a client component hook, so "use client" declarative required in the component file.

For ex -

1. If current url path is http://localhost:3000/about
   then it will return `/about`

2. If current url path is http://localhost:3000/dashboard?v=2
   then it will return `/dashboard`

3. If current url path is http://localhost:3000/blogs/hello-world
   then it will return `/blogs/hello-world`
