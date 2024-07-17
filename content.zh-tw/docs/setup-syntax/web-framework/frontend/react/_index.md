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
   ```
   > Framework: React  
   > Variant: TypeScript
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
2. Import and use `Helmet` in your component

   ```ts
   // src/pages/Home.tsx
   import { Helmet } from "react-helmet";

   const Home: React.FC = () => {
     return (
       <div>
         <Helmet>
           <title>Home Page</title>
           <meta
             name="description"
             content="This is the home page description"
           />
         </Helmet>
         <h1>Welcome to the Home Page</h1>
       </div>
     );
   };

   export default Home;
   ```
