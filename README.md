# React SPA with Private Routes – Azure Static Web App 404 Fix

This project demonstrates how to set up private routes in a React Single Page Application (SPA) and how to fix the common 404 error that occurs on page refresh when deploying to **Azure Static Web Apps**.
The app features:
- Public and private routes
- Login/Logout toggle using a hardcoded flag
- Protected Dashboard route
- Project structure with `components/`, `pages/`, and `routes/` folders

## ❗ The Issue

When you refresh a route like `/about`, Azure tries to fetch that path directly from the server. Since it's an SPA, the route is handled client-side by React Router — but Azure returns a **404 Not Found** instead.

![image](https://github.com/user-attachments/assets/989c0b88-4e8c-48a6-8dbf-3b54946ee660)

## ✅ The Solution

✅ 1. Add routes.json to public/
Create a file at public/routes.json:
```
{
  "routes": [
    {
      "route": "/*",
      "serve": "/index.html",
      "statusCode": 200
    }
  ]
}
```
This tells Azure to serve index.html for any unknown route, so React Router can take over.

✅ 2. Add staticwebapp.config.json to the root
Create a file at the root of your project: staticwebapp.config.json
```
{
  "navigationFallback": {
    "rewrite": "index.html",
    "exclude": ["/static/images/*.{png,jpg,gif}", "/static/css/*"]
  },
  "mimeTypes": {
    ".json": "text/json"
  }
}
```
This config ensures proper routing and fallback behavior for your SPA on Azure.
