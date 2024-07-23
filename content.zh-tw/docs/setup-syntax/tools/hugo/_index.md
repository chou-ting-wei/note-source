---
title: Hugo
type: docs
---

# Hugo

## Favicon

Set up a favicon for your website that is ready for various devices and platforms.

1. Use the [Favicon Generator](https://favicon.io/favicon-converter/) to create your favicon files
2. Place the downloaded favicon files in your Hugo project's `static` directory

   - `favicon.ico`
   - `apple-touch-icon.png`
   - `favicon-32x32.png`
   - `favicon-16x16.png`
   - `android-chrome-192x192.png`
   - `android-chrome-512x512.png`
   - `site.webmanifest`

3. Edit the `baseof.html` file located in your Hugo project's `layouts/_default` directory. Insert the following link tags within the `<head>` section to reference your favicon files

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <!-- Existing head content -->

       <!-- Favicon links -->
       <link rel="icon" href="/favicon.ico" />
       <link rel="shortcut icon" type="image/x-icon" href="/favicon.ico" />
       <link rel="icon" href="/favicon.ico" />
       <link rel="shortcut icon" type="image/x-icon" href="/favicon.ico" />
       <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
       <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
       <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
       <link rel="manifest" href="/site.webmanifest" />
     </head>
     <body>
       <!-- Existing body content -->
     </body>
   </html>
   ```

4. Edit the `site.webmanifest` file in the `static` directory

   ```json
   {
     "name": "My Application",
     "icons": [
       {
         "src": "/android-chrome-192x192.png",
         "sizes": "192x192",
         "type": "image/png"
       },
       {
         "src": "/android-chrome-512x512.png",
         "sizes": "512x512",
         "type": "image/png"
       }
     ],
     "theme_color": "#ffffff",
     "background_color": "#ffffff",
     "display": "standalone"
   }
   ```

## Google Analytics

Enable [Google Analytics](https://analytics.google.com/) tracking on your Hugo website, allowing you to monitor traffic and user interactions.

1. Get Your Tracking ID
   > It should look like G-XXXXXXXXXX.
2. Edit the `baseof.html` file to include the Google Analytics script within the `<head>` section

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <!-- Existing head content -->

       <!-- Google Analytics -->
       <script
         async
         src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"
       ></script>
       <script>
         window.dataLayer = window.dataLayer || [];
         function gtag() {
           dataLayer.push(arguments);
         }
         gtag("js", new Date());

         gtag("config", "G-XXXXXXXXXX");
       </script>
       {{ end }}
     </head>
     <body>
       <!-- Existing body content -->
     </body>
   </html>
   ```
