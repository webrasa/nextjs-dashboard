## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

# Chapter 2 CSS Styling
How to add a global CSS file to your application.

Two different ways of styling: Tailwind and CSS modules.

How to conditionally add class names with the clsx utility package.

## Global styles
If you look inside the /app/ui folder, you'll see a file called global.css.
You can import global.css in any component in your application, but it's usually good practice to add it to your top-level component. In Next.js, this is the root layout (more on this later).

## Tailwind
https://nextjs.org/learn/dashboard-app/css-styling#tailwind

## CSS Modules
https://nextjs.org/learn/dashboard-app/css-styling#css-modules

Using the clsx library to toggle class names
https://nextjs.org/learn/dashboard-app/css-styling#using-the-clsx-library-to-toggle-class-names
import clsx from 'clsx';
 
export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}

# Chapter 3 Optimizing Fonts and Images
https://nextjs.org/learn/dashboard-app/optimizing-fonts-images

How to add custom fonts with next/font.

How to add images with next/image.

How fonts and images are optimized in Next.js.

# Chapter 4 Creating Layouts and Pages

Create the dashboard routes using file-system routing.

Understand the role of folders and files when creating new route segments.

Create a nested layout that can be shared between multiple dashboard pages.

Understand what colocation, partial rendering, and the root layout are.

Creating the dashboard page

Creating the dashboard layout
https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages#creating-the-dashboard-layout

One benefit of using layouts in Next.js is that on navigation, only the page components update while the layout won't re-render. This is called partial rendering:

Root layout
In Chapter 3, you imported the Inter font into another layout: /app/layout.tsx.

This is called a root layout and is required. Any UI you add to the root layout will be shared across all pages in your application. You can use the root layout to modify your <html> and <body> tags, and add metadata (you'll learn more about metadata in a later chapter).

Since the new layout you've just created (/app/dashboard/layout.tsx) is unique to the dashboard pages, you don't need to add any UI to the root layout above.

Root layout: https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#root-layout-required

Since the new layout you've just created (/app/dashboard/layout.tsx) is unique to the dashboard pages, you don't need to add any UI to the root layout above.

# Chapter 5. Navigating Between Pages

How to use the next/link component.

How to show an active link with the usePathname() hook.

How navigation works in Next.js.

Why optimize navigation?
https://nextjs.org/learn/dashboard-app/navigating-between-pages#why-optimize-navigation

Full page refresh on each page navigation!

The <Link> component
In Next.js, you can use the <Link /> Component to link between pages in your application. <Link> allows you to do client-side navigation with JavaScript.
client-side navigation: https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#how-routing-and-navigation-works

### Automatic code-splitting and prefetching
To improve the navigation experience, Next.js automatically code splits your application by route segments. This is different from a traditional React SPA, where the browser loads all your application code on initial load.

Splitting code by routes means that pages become isolated. If a certain page throws an error, the rest of the application will still work.

Futhermore, in production, whenever <Link> components appear in the browser's viewport, Next.js automatically prefetches the code for the linked route in the background. By the time the user clicks the link, the code for the destination page will already be loaded in the background, and this is what makes the page transition near-instant!

Learn more about how navigation works: https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#how-routing-and-navigation-works

### Pattern: Showing active links
usePathname() - https://nextjs.org/docs/app/api-reference/functions/use-pathname

## Since usePathname() is a hook, you'll need to turn nav-links.tsx into a Client Component. Add React's "use client" directive to the top of the file, then import usePathname() from next/navigation:

# Chapter 7 Fetching Data

Learn about some approaches to fetching data: APIs, ORMs, SQL, etc.

How Server Components can help you access back-end resources more securely.

What network waterfalls are.

How to implement parallel data fetching using a JavaScript Pattern.

#### API Layer
In Next.js, you can create API endpoints using Route Handlers. https://nextjs.org/docs/app/building-your-application/routing/route-handlers

Database queries
When you're creating a full-stack application, you'll also need to write logic to interact with your database. For relational databases like Postgres, you can do this with SQL, or an ORM like Prisma.

### Using Server Components to fetch data
https://nextjs.org/learn/dashboard-app/fetching-data#using-server-components-to-fetch-data

### What are request waterfalls?
https://nextjs.org/learn/dashboard-app/fetching-data#what-are-request-waterfalls

Current limitations
1. The data requests are creating an unintentional waterfall.
2. The dashboard is static, so any data updates will not be reflected on your application.

# Chapter 8 Static and Dynamic Rendering

What static rendering is and how it can improve your application's performance.

What dynamic rendering is and when to use it.

Different approaches to make your dashboard dynamic.

Simulate a slow data fetch to see what happens.

## What is Static Rendering?
With static rendering, data fetching and rendering happens on the server at build time (when you deploy) or during revalidation.
Faster Websites
Reduced Server Load
SEO
### Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page.

## What is Dynamic Rendering?
With dynamic rendering, content is rendered on the server for each user at request time (when the user visits the page). There are a couple of benefits of dynamic rendering:

Real-Time Data
User-Specific Content
Request Time Information - Dynamic rendering allows you to access information that can only be known at request time, such as cookies or the URL search parameters.

## Making the dashboard dynamic
https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering#making-the-dashboard-dynamic
Note: unstable_noStore is an experimental API and may change in the future. If you prefer to use a stable API in your own projects, you can also use the Segment Config Option export const dynamic = "force-dynamic".

## Simulating a Slow Data Fetch
Here, you've added an artificial 3-second delay to simulate a slow data fetch. The result is that now your whole page is blocked while the data is being fetched.

Which brings us to a common challenge developers have to solve:

With dynamic rendering, your application is only as fast as your slowest data fetch.

# Chapter 9 Streaming

What streaming is and when you might use it.

How to implement streaming with loading.tsx and Suspense.

What loading skeletons are.

What route groups are, and when you might use them.

Where to place Suspense boundaries in your application.

### What is streaming?
Streaming is a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.

There are two ways you implement streaming in Next.js:

At the page level, with the loading.tsx file.
For specific components, with <Suspense>.

### Streaming a whole page with loading.tsx
In the /app/dashboard folder, create a new file called loading.tsx

A few things are happening here:

1. loading.tsx is a special Next.js file built on top of Suspense, it allows you to create fallback UI to show as a replacement while page content loads.
2. Since <Sidebar> is static, so it's shown immediately. The user can interact with <Sidebar> while the dynamic content is loading.
3. The user doesn't have to wait for the page to finish loading before navigating away (this is called interruptable navigation).

### Adding loading skeletons
A loading skeleton is a simplified version of the UI. Many websites use them as a placeholder (or fallback) to indicate to users that the content is loading. Any UI you embed into loading.tsx will be embedded as part of the static file, and sent first. Then, the rest of the dynamic content will be streamed from the server to the client.

### Fixing the loading skeleton bug with route groups
Right now, your loading skeleton will apply to the invoices and customers pages as well.

Since loading.tsx is a level higher than /invoices/page.tsx and /customers/page.tsx in the file system, it's also applied to those pages.

We can change this with Route Groups. Create a new folder called /(overview) inside the dashboard folder. Then, move your loading.tsx and page.tsx files inside the folder

Route groups allow you to organize files into logical groups without affecting the URL path structure. When you create a new folder using parentheses (), the name won't be included in the URL path. So /dashboard/(overview)/page.tsx becomes /dashboard.

## Streaming a component
If you remember the slow data request, fetchRevenue(), this is the request that is slowing down the whole page. Instead of blocking your page, you can use Suspense to stream only this component and immediately show the rest of the page's UI.

To do so, you'll need to move the data fetch to the component.

### Grouping components
Great! You're almost there, now you need to wrap the <Card> components in Suspense. You can fetch data for each individual card, but this could lead to a popping effect as the cards load in, this can be visually jarring for the user.

So, how would you tackle this problem?

To create more of a staggered effect, you can group the cards using a wrapper component. This means the static <Sidebar/> will be shown first, followed by the cards.

### Deciding where to place your Suspense boundaries
Where you place your Suspense boundaries will depend on a few things:

How you want the user to experience the page as it streams.
What content you want to prioritize.
If the components rely on data fetching.
Take a look at your dashboard page, is there anything you would've done differently?

Don't worry. There isn't a right answer.

You could stream the whole page like we did with loading.tsx... but that may lead to a longer loading time if one of the components has a slow data fetch.
You could stream every component individually... but that may lead to UI popping into the screen as it becomes ready.
You could also create a staggered effect by streaming page sections. But you'll need to create wrapper components.
Where you place your suspense boundaries will vary depending on your application. In general, it's good practice to move your data fetches down to the components that need it, and then wrap those components in Suspense. But there is nothing wrong with streaming the sections or the whole page if that's what your application needs.

Don't be afraid to experiment with Suspense and see what works best, it's a powerful API that can help you create more delightful user experiences.