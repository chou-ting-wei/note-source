---
title: Next.js
type: docs
---

# Next.js

## Create Next.js Project

1. Create your project
   ```sh
   npx create-next-app@latest
   ```
   ```
    √ What is your project named? ... my-project
    √ Would you like to use TypeScript? ... Yes
    √ Would you like to use ESLint? ... Yes
    √ Would you like to use Tailwind CSS? ... Yes
    √ Would you like to use `src/` directory? ... No
    √ Would you like to use App Router? (recommended) ... Yes
    √ Would you like to customize the default import alias (@/*)? ... No
   ```
2. Start your build process
   ```sh
   cd my-project
   npm run dev
   ```

## Component

### Link

In Next.js, you can use the `Link` Component `next/link` to link between pages in your application.

```tsx
import Link from "next/link";

export default function FirstPost() {
  return (
    <>
      <h1>First Post</h1>
      <h2>
        <Link href="/">Back to home</Link>
      </h2>
    </>
  );
}
```

### Image

Next.js has support for Image Optimization by default. This allows for resizing, optimizing, and serving images in modern formats like `WebP` when the browser supports it.

```tsx
import Image from "next/image";

const YourComponent = () => (
  <Image src="/images/profile.jpg" height={144} width={144} alt="Your Name" />
);
```

### Head

`<Head>` is a React Component that is built into Next.js. It allows you to modify the `<head>` of a page.

```tsx
import Head from "next/head";

export default function FirstPost() {
  return (
    <>
      <Head>
        <title>First Post</title>
      </Head>
      <h1>First Post</h1>
      <h2>
        <Link href="/">Back to home</Link>
      </h2>
    </>
  );
}
```

### Script

The `<Script>` component is a way to include external scripts or libraries in your application.

```tsx
import Script from "next/script";

export default function FirstPost() {
  return (
    <>
      <Head>
        <title>First Post</title>
      </Head>
      <Script
        src="https://connect.facebook.net/en_US/sdk.js"
        strategy="lazyOnload"
        onLoad={() =>
          console.log(`script loaded correctly, window.FB has been populated`)
        }
      />
      <h1>First Post</h1>
      <h2>
        <Link href="/">Back to home</Link>
      </h2>
    </>
  );
}
```

## Favicon

1. Use the [Favicon Generator](https://favicon.io/favicon-converter/) to create your favicon files
   ```txt
   android-chrome-192x192.png
   android-chrome-512x512.png
   apple-touch-icon.png
   favicon-16x16.png
   favicon-32x32.png
   favicon.ico
   site.webmanifest
   ```
2. Rename and organize the downloaded favicon files as follows

   ```txt
   \app
       icon.ico (renamed from favicon.ico)
       apple-icon.png (renamed from apple-touch-icon.png)
   \public\images
       android-chrome-192x192.png
       android-chrome-512x512.png
   ```

3. Configure the manifest file

   ```tsx
   // app/manifest.tsx
   import { MetadataRoute } from "next";

   export default function manifest(): MetadataRoute.Manifest {
     return {
       name: "My Application",
       icons: [
         {
           src: "/images/android-chrome-192x192.png",
           sizes: "192x192",
           type: "image/png",
         },
         {
           src: "/images/android-chrome-512x512.png",
           sizes: "512x512",
           type: "image/png",
         },
       ],
       theme_color: "#ffffff",
       background_color: "#ffffff",
       display: "standalone",
     };
   }
   ```

## Metadata

### Static Metadata

To define static metadata, export a Metadata object from a `layout.tsx` or static `page.tsx` file.

```tsx
// app/layout.tsx | app/page.tsx
import type { Metadata } from "next";

export const metadata = {
  title: "Acme",
  openGraph: {
    title: "Acme",
    description: "Acme is a...",
  },
};

export default function Page() {}
```

### Sitemap

You can use the `sitemap.tsx` file convention to programmatically generate a sitemap by exporting a default function that returns an array of URLs.

```tsx
// app/sitemap.tsx
import { MetadataRoute } from "next";

export default function sitemap(): MetadataRoute.Sitemap {
  return [
    {
      url: "https://acme.com",
      lastModified: new Date(),
      changeFrequency: "yearly",
      priority: 1,
    },
    {
      url: "https://acme.com/about",
      lastModified: new Date(),
      changeFrequency: "monthly",
      priority: 0.8,
    },
    {
      url: "https://acme.com/blog",
      lastModified: new Date(),
      changeFrequency: "weekly",
      priority: 0.5,
    },
  ];
}
```

### Opengraph

Add `opengraph-image.(jpg|jpeg|png|gif)` and `twitter-image.(jpg|jpeg|png|gif)` to `app` directory. Next.js will evaluate the file and automatically add the appropriate tags to your project's `<head>` element.

```tsx
// output
<meta property="og:image" content="<generated>" />
<meta property="og:image:type" content="<generated>" />
<meta property="og:image:width" content="<generated>" />
<meta property="og:image:height" content="<generated>" />

<meta name="twitter:image" content="<generated>" />
<meta name="twitter:image:type" content="<generated>" />
<meta name="twitter:image:width" content="<generated>" />
<meta name="twitter:image:height" content="<generated>" />
```

## Google Analytics

To load Google Analytics for all routes, include the component directly in your root layout and pass in your measurement ID:

```tsx
// app/layout.tsx
import { GoogleAnalytics } from "@next/third-parties/google";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
      <GoogleAnalytics gaId="G-XXXXXXXXXX" />
    </html>
  );
}
```

> If you encounter an error, it may be because `GoogleAnalytics` was introduced in a canary release.
> To resolve this, upgrade `@next/third-parties` to the latest canary version.
>
> ```sh
> npm i @next/third-parties@14.0.5-canary.59
> ```

## Handling Errors

The not-found file is used to render UI when the notFound function is thrown within a route segment. Along with serving a custom UI, Next.js will return a 200 HTTP status code for streamed responses, and 404 for non-streamed responses.

```tsx
// app/not-found.tsx
import Link from "next/link";

export default function NotFound() {
  return (
    <div>
      <h2>Not Found</h2>
      <p>Could not find requested resource</p>
      <Link href="/">Return Home</Link>
    </div>
  );
}
```
