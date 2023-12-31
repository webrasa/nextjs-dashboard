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