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
    /* ./src/index.css */
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```
### prettier
1. Install prettier
    ```sh
    npm install --save-dev prettier
    ```
2. 

### react-router-dom
1. Install react-router-dom
    ```sh
    npm install react-router-dom
    ```

### react-helmet
1. Install react-helmet
    ```sh
    npm install react-helmet
    ```

## Files template