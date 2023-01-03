1. what is nextjs ?
2. features of nextjs ?
3. example to demonstrate how to create a custom error page in Next.js?
4. Data Fetching Methods in Next.js

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua1. what is nextjs ? </div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. =>  Next.js is an open-source, lightweight React.js framework that facilitates developers to build static and server-side rendering web applications. It was created by Zeit. Next.js framework is based on React, Webpack, and Babel and allows us to write server-rendered React apps easily. It doesn't require any webpack configuration and only needs npm run dev start building your next feature-filled web application.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua2. features of nextjs ? </div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => 
 Reasons why the world's leading companies prefer Next.js:

1. Zero Setup: Next.js provides automatic code-splitting, filesystem-based routing, hot code reloading, and universal rendering; that's why the world's leading companies prefer it.
2. Fully Extensible: Next.js is fully extensible and has complete control over Babel and Webpack. It provides a customizable server, routing, and next plugins.
3. Ready for Production: Next.js is optimized for smaller build sizes, faster dev compilation, and many other improvements, making it a popular choice.
4. Next.js can Deploy Anywhere: Next.js is an open-source, lightweight React.js framework that facilitates developers to build static and server-side rendering web applications.
5. js provides the by default and easy server rendering.
6. js supports static exporting.
7. It provides a Webpack-based dev environment which supports Hot Module Replacement (HMR)
8. It seaports automatic code-splitting for faster page loads.
9. It supports simple client-side routing (page-based) or file system-based routing.
10. It provides complete Webpack and Babel control.
11. It provides a faster and optimized development compilation.
12. It can be implemented with Express or any other Node.js HTTP server.
13. You can easily customize it with your own Babel and Webpack configurations.
14. It supports hot code reloading.
</div>
<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. example to demonstrate how to create a custom error page in Next.js? ?</div>
<div style="color:white;font-size:18px;text-transform: Capitalize;">Ans. =>

```javascript
import React from "react";
class Error extends React.Component {
  static getInitialProps({ res, err }) {
    const statusCode = res ? res.statusCode : err ? err.statusCode : null;
    return { statusCode };
  }
  render() {
    return (

        {this.props.statusCode
          ? `An error ${this.props.statusCode} has occurred on the server`
          : "An error occurred on client-side"}

    );
  }
}
export default Error;
```

</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua4. Data Fetching Methods in Next.js ? </div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. =>

Next.js provides three data fetching methods and based on these methods, it renders content differently. (You can learn about different rendering methods here.

1. getStaticProps
2. getStaticPaths
3. getServerSideProps

getStaticProps: It preloads all of the data needed for a given page and renders pages ahead of the user’s request at build time. For speedier retrieval, all of the data is cached on a headless CMS. For better SEO performance, the page is pre-rendered and cached. If no other data fetching method is specified, Next.js will use this by default. It is used to implement Static Site Generation and Incremental Site Regeneration.

Properties of getStaticProps:

It can only be exported from the page file, not the component file.
It only runs on build time.
It runs on every subsequent request in development mode.
Its code is completely excluded from the client-side bundle.

getStaticPaths: If a page uses getStaticProps and has dynamic routes, it must declare a list of paths that will be statically generated. Next.js will statically pre-render all the paths defined by getStaticPaths when we export a function named getStaticPaths from a page.

Properties of getStaticPaths:

It can only be exported from a page file.
It is meant for dynamic routes.
Page must also implement getStaticProps.
It runs only at build time in production.
It runs on every request in development mode.

getServerSideProps: It will pre-render the page on every subsequent request. It is slower as compared to getStaticProps as the page is being rendered on every request. getServerSideProps props return JSON which will be used to render the page all this work will be handled automatically by Next.js. It could be used for calling a CMS, database, or other APIs directly from getServerSideProps. It is used to implement Server Side Rendering.

Properties of getServerSideProps:

It runs on every subsequent request in development as well as production mode.
Its code is excluded from the client-side bundle.
It can only be exported from page file.
When to use which data fetching method: If your page’s content is static or doesn’t change frequently then you should go for getStaticProps as it builds pages on build time hence increasing performance. If your page has dynamic routes then getStaticPaths should be used along with getStaticProps.

But if your website contains a page whose data changes very frequently then you must use getServerSideProps as it fetches fresh data on every request.

Example: We will build a simple Next Js application with three pages of albums, posts, and a users page with dynamic routes. All three pages will implement different data fetching methods. For this example, we will use JSONPlaceholder API to fetch random data.

```javascript
import React from "react";
import Link from "next/link";
const Home = () => {
  // This is the home page which will
  // contain links to all other pages
  return (
    <>
      <h1>Hello Geeks</h1>
      <ul>
        <li>
          getStaticProps :<Link href={"/about"}>About Page</Link>
        </li>
        <li>
          getStaticPaths :<Link href={"/users/1"}>User 1</Link>
        </li>
        <li>
          getServerSideProps :<Link href={"/posts"}>Posts Page</Link>
        </li>
      </ul>
    </>
  );
};

export default Home;
```

/pages/albums.jsx – Albums page will implement static site generation using getStaticProps, we will export the data fetching method along with the page component. We can send fetched data to the page component using props. Next Js will fetch all the albums at build time before the user’s request.

```javascript
import React from "react";

export const getStaticProps = async () => {
  // Fetching data from jsonplaceholder.
  const res = await fetch("https://jsonplaceholder.typicode.com/albums");
  let allAlbums = await res.json();

  // Sending fetched data to the page component via props.
  return {
    props: {
      allAlbums: allAlbums.map((album) => album.title),
    },
  };
};

const Albums = ({ allAlbums }) => {
  return (
    <div>
      <h1>All Albums</h1>
      {allAlbums.map((album, idx) => (
        <div key={idx}>{album}</div>
      ))}
    </div>
  );
};

export default Albums;
```

/pages/posts.jsx – Posts page will implement server-side rendering using getServerSideProps. It’ll fetch posts data and build page at each request made by user., and send fetched data to the component using props.

```javascript
import React from "react";

export const getServerSideProps = async (ctx) => {
  // ctx is the context object which contains the request,
  // response and props passed to the page.

  // fetching data from jsonplaceholder.
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  let allPosts = await res.json();

  // Sending fetched data to the page component via props.
  return {
    props: {
      allPosts: allPosts.map((post) => post.title),
    },
  };
};

const Posts = ({ allPosts }) => {
  return (
    <div>
      <h1>All Posts</h1>
      {allPosts.map((post, idx) => (
        <div key={idx}>{post}</div>
      ))}
    </div>
  );
};

export default Posts;
```

/pages/users/[id].jsx – Because this is a dynamic page, we must pre-define all of the user Ids so that Next Js can retrieve their data at build time. As a result, we use getStaticPaths and define ten user Ids.

```javascript
import React from "react";

export const getStaticProps = async (ctx) => {
  // ctx will contain request parameters
  const { params } = ctx;

  // We will destructure id from the parameters
  const userId = params.id;

  // Fetching user data
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/users/${userId}`
  );
  const userData = await res.json();

  // Sending data to the page via props
  return {
    props: {
      user: userData,
    },
  };
};

export const getStaticPaths = () => {
  // Specifying all the routes to be
  // pre-rendered by next js
  return {
    paths: [
      { params: { id: "1" } },
      { params: { id: "2" } },
      { params: { id: "3" } },
      { params: { id: "4" } },
      { params: { id: "5" } },
      { params: { id: "6" } },
      { params: { id: "7" } },
      { params: { id: "8" } },
      { params: { id: "9" } },
      { params: { id: "10" } },
    ],
    fallback: false,
  };
};

const User = ({ user }) => {
  return (
    <>
      <h1>User {user.id}</h1>
      <h2>Name : {user.name}</h2>
      <h2>Email : {user.email}</h2>
    </>
  );
};

export default User;
```

</div>
