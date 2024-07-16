---
title: React
type: docs
---

# React

## Create Vite Project

1. Create project folder
   ```sh
   npm install -g create-vite
   npm create vite@latest my-react-app -- --template react-ts
   # Framework: React
   # Variant: TypeScript
   ```
2. Install dependencies and run
   ```sh
   cd my-react-app
   npm install
   npm run dev
   ```

## Dependencies

### Tailwind CSS

1. Install Tailwind CSS and other dependencies
   ```sh
   npm install -D tailwindcss postcss autoprefixer
   ```
2. Generate the configuration files
   ```sh
   npx tailwindcss init -p
   ```
3. Configure source paths
   ```js
   // tailwind.config.js
   /** @type {import('tailwindcss').Config} */
   export default {
     content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
     theme: {
       extend: {},
     },
     plugins: [],
   };
   ```
4. Add tailwind directives to your CSS
   ```css
   /* src/index.css */
   @tailwind base;
   @tailwind components;
   @tailwind utilities;
   ```

### react-router-dom

1. Install react-router-dom
   ```sh
   npm install react-router-dom
   ```
2. Implementing routing in your application

   ```ts
   // src/App.tsx
   import { BrowserRouter as Router, Routes, Route } from "react-router-dom";

   import Home from "./pages/Home";
   import NotFound from "./pages/NotFound";

   function App() {
     return (
       <Router>
         <Routes>
           <Route path="/" element={<Home />} />
           <Route path="*" element={<NotFound />} />
         </Routes>
       </Router>
     );
   }

   export default App;
   ```

### react-helmet

1. Install react-helmet
   ```sh
   npm install react-helmet
   ```
2. Implementing routing in your application

   ```ts
   // src/App.tsx
   import { Helmet } from "react-helmet";

   function App() {
     return (
       <Helmet>
         <title>My Application</title>
         <meta
           name="description"
           content="This is an example application demonstrating the use of React Helmet."
         />
         <meta property="og:title" content="My Application" />
         <meta
           property="og:description"
           content="An example application demonstrating the use of React Helmet for managing document head."
         />
         <meta property="og:url" content="https://example.com" />
         <meta property="og:site_name" content="My Application" />
         <meta property="og:type" content="website" />
         <meta property="og:updated_time" content="2024-07-16T00:00:00+00:00" />
       </Helmet>
     );
   }

   export default App;
   ```
