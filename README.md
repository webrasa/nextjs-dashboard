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

