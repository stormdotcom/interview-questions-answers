### Next.js Questions and Answers

#### 1. **What is the use of the `getInitialProps` function in Next.js?**

`getInitialProps` is a function used in Next.js to asynchronously fetch data before rendering a page. It can run on both the server and client sides and allows you to make initial data available to the component during the initial rendering process.

#### 2. **What are the drawbacks of `getInitialProps`?**

The drawbacks of `getInitialProps` include its impact on performance due to blocking data fetching during page rendering, which can lead to slower load times. Additionally, it complicates server-side rendering logic and can make it harder to optimize for static generation.

#### 3. **How do you perform client-side navigation in a Next.js app?**

Client-side navigation in a Next.js app can be done using the `next/link` component or the `useRouter` hook from the `next/router` module. The `next/link` component wraps around anchor tags to handle client-side navigation, while the `useRouter` hook provides programmatic navigation capabilities.

#### 4. **How do you share state between pages in Next.js?**

To share state between pages in Next.js, you can use React's context API, global state management libraries like Redux or Zustand, or URL query parameters and cookies for persistence across pages.

#### 5. **How can you add environment variables that will be available only on the server side in Next.js?**

In Next.js, server-side environment variables can be added to a `.env.local` file and prefixed with `NEXT_PUBLIC_` to make them available only on the server side. Variables without this prefix will not be exposed to the client.

#### 6. **What does `fallback: 'blocking'` do in the `getStaticPaths` function in Next.js?**

In the `getStaticPaths` function, `fallback: 'blocking'` tells Next.js to serve a static page generated on-demand for a path that wasn’t generated at build time. The first request to such a path will wait until the page is generated and cached, while subsequent requests will serve the cached version.

#### 7. **How can you make a Next.js application fully server-rendered?**

To make a Next.js application fully server-rendered, you can use the `getServerSideProps` function. This function fetches data on each request, ensuring that the pages are always rendered on the server.

#### 8. **How can you generate a static site with data that needs to be fetched from an API in Next.js?**

To generate a static site with data fetched from an API in Next.js, you can use the `getStaticProps` function. This function runs at build time and allows you to fetch data from an API, passing it as props to your page component.

#### 9. **How can you pass data from `getServerSideProps` or `getStaticProps` to your page in Next.js?**

Data fetched in `getServerSideProps` or `getStaticProps` is returned as an object with a `props` key. This data is then passed as props to the page component, allowing you to access and use it within the component.

### Next.js Questions and Answers

#### 10. **What is the difference between `getStaticProps` and `getServerSideProps`?**

`getStaticProps` is used to generate static pages at build time, making them highly optimized for performance. `getServerSideProps`, on the other hand, fetches data on each request, which can handle dynamic content but at the cost of slower response times compared to static pages.

#### 11. **How can you enable TypeScript in a Next.js project?**

To enable TypeScript in a Next.js project, create a `tsconfig.json` file in the root directory of your project. Next.js will automatically detect it and install the necessary TypeScript dependencies. You can then start writing TypeScript code in your project.

#### 12. **What is `getStaticPaths` used for in Next.js?**

`getStaticPaths` is used with `getStaticProps` to generate dynamic routes at build time. It allows you to specify which paths should be pre-rendered based on data fetched from an external source.

#### 13. **How do you handle redirects in Next.js?**

Redirects in Next.js can be handled in the `next.config.js` file using the `redirects` method, where you specify the source, destination, and whether the redirect is permanent or not.

#### 14. **How can you optimize images in a Next.js application?**

Next.js provides an `Image` component for optimizing images. It automatically optimizes images for faster load times and supports lazy loading, responsive images, and other optimizations out of the box.

#### 15. **What is the `next/head` component used for?**

The `next/head` component allows you to modify the `<head>` section of your HTML document. You can use it to add meta tags, link tags, title tags, and other elements that should be included in the `<head>` section of your pages.

#### 16. **How do you create a custom `_app.js` in Next.js?**

To create a custom `_app.js` in Next.js, add a file named `_app.js` in the `pages` directory. This file allows you to override the default App component, enabling you to persist layout between page changes, maintain state, or inject additional data into pages.

#### 17. **What is `next.config.js` and what can you configure in it?**

`next.config.js` is a configuration file used to customize the behavior of a Next.js application. You can configure settings such as environment variables, custom webpack configurations, redirects, rewrites, headers, and more.

#### 18. **How can you handle API routes in Next.js?**

API routes in Next.js can be created inside the `pages/api` directory. Each file in this directory becomes an API endpoint, allowing you to build full-featured APIs alongside your Next.js pages.

#### 19. **What is the purpose of the `_document.js` file in Next.js?**

The `_document.js` file in Next.js is used to augment the application's HTML and body tags. It allows you to customize the entire HTML document structure, including the addition of custom styles, scripts, and meta tags that should be applied globally.

#### 20. **How do you deploy a Next.js application?**

Next.js applications can be deployed to various platforms such as Vercel, which is the default and recommended platform. You can also deploy to other hosting providers like AWS, Netlify, or any platform that supports Node.js applications by following the specific deployment instructions provided by Next.js.

#### 21. **What is the purpose of `next/link` in Next.js?**

The `next/link` component is used for client-side navigation in Next.js. It allows you to create links between pages in your application without causing a full page reload, thereby improving performance and user experience.

#### 22. **How can you handle CSS in a Next.js project?**

Next.js supports various ways to handle CSS, including global CSS, CSS Modules, and styled-jsx. You can also use third-party libraries like styled-components or emotion for more advanced styling solutions.

#### 23. **What is Incremental Static Regeneration (ISR) in Next.js?**

Incremental Static Regeneration (ISR) allows you to update static content after a Next.js site has been built and deployed. With ISR, you can revalidate static pages in the background, ensuring your content remains up-to-date without requiring a full rebuild.

#### 24. **How do you create a custom 404 page in Next.js?**

To create a custom 404 page in Next.js, add a file named `404.js` to the `pages` directory. This file will automatically be used to render a custom 404 error page when a user navigates to a non-existent route.

#### 25. **What is `next/image` and how does it differ from the standard HTML `img` tag?**

The `next/image` component is an optimized image component in Next.js that provides built-in performance benefits such as automatic resizing, lazy loading, and serving images in modern formats like WebP. It differs from the standard HTML `img` tag by offering these optimizations out of the box.

### Interview Questions

#### 26. What is `next.config.js` and how is it used?

`next.config.js` is the central configuration file for Next.js. It exports an object where you can customize settings such as:

- Custom webpack configuration
- Environment variables (server-only and client-exposed)
- Redirects, rewrites, headers
- Internationalization (i18n)

#### 27. How can you fetch data without using `useEffect` on the client side?

Use `getServerSideProps` to fetch data on the server at request time and pass it as props to your page, eliminating the need for client-side data fetching with `useEffect`.

#### 28. How do you perform SSR using dynamic imports?

Use `dynamic()` from `next/dynamic` with `{ ssr: true }`, for example:

```js
import dynamic from "next/dynamic";
const Component = dynamic(() => import("../components/Component"), {
  ssr: true,
});
```

#### 29. What are new features introduced in Next.js 14 and 15?

- App Router enhancements (Next.js 14)
- Streaming SSR support with React 18+
- Turbopack integration and speed improvements
- Enhanced image and font optimization modules
- Middleware and Edge Functions optimizations
- Next.js 15 (anticipated): further performance boosts, advanced caching strategies, and refined API routing

---
