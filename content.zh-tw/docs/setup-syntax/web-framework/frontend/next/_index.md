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

```ts
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

```ts
import Image from "next/image";

const YourComponent = () => (
  <Image src="/images/profile.jpg" height={144} width={144} alt="Your Name" />
);
```

### Head

`<Head>` is a React Component that is built into Next.js. It allows you to modify the `<head>` of a page.

```ts
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
