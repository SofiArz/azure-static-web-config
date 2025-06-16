# React SPA with Private Routes – Azure Static Web App 404 Fix

This project demonstrates how to set up private routes in a React Single Page Application (SPA) and how to fix the common 404 error that occurs on page refresh when deploying to **Azure Static Web Apps**.

## ❗ The Issue

When you refresh a route like `/dashboard`, Azure tries to fetch that path directly from the server. Since it's an SPA, the route is handled client-side by React Router — but Azure returns a **404 Not Found** instead.