---
title: Shadcn
type: docs
---

# Shadcn

[Shadcn](https://ui.shadcn.com/) offers a collection of beautifully designed, accessible, and customizable React components that you can copy and paste directly into your project.

## Installation

1. Initialize your Next.js project with TypeScript, Tailwind CSS, and ESLint

   ```sh
   npx create-next-app@latest my-app --typescript --tailwind --eslint
   ```

2. Utilize the Shadcn CLI to configure your environment

   ```sh
   npx shadcn-ui@latest init
   ```

   ```
   √ Which style would you like to use? » Default
   √ Which color would you like to use as base color? » Slate
   √ Would you like to use CSS variables for colors? ... yes
   ```

## Component

### Button

1. Add the Button component to your project using the Shadcn CLI

   ```sh
   npx shadcn-ui@latest add button
   ```

2. Implement the Button component within your application

   ```tsx
   import { Button } from "@/components/ui/button";

   <Button variant="outline">Button</Button>;
   ```

## Documentation

For in-depth guides, further component usage examples, and additional resources, please visit the [Shadcn Documentation](https://ui.shadcn.com/docs).
