# Infrastructure Overview

Let's present it step by step per component :

---

## General components

- **Vnet**  
- **Managed identity / RBAC roles**

---

## Cloudflare WAF

The website is protected by **Cloudflare**, including domain name hosting, CDN service and Web Application Firewall.  
The WAF represents the first step into the website.

---

## Domain name

**ivaninho.pro** is currently hosted on **Cloudflare DNS** and is answering for my web app.  
To replace its *azurewebsites.net* domain.

---

## Web app

The web app contains the **Next.js server** that serves the website pages.  
The Next.js server also centralize every actions with its own API endpoint.  
Then redirects it to the **reverse proxy**.

---

## Cloudflare Turnstile

The turnstile is the little Cloudflare card that initiate a challenge to verify the humanity of the users.  
It generates a token that is sent through multiple steps to verify its authenticity against **Cloudflare API**.

---

## Nginx reverse proxy

This service acts as a **load balancing instance**.  
It retrieves and redirects every requests to the different services.

---

## Auth-service

This service contains the backend logic for authentication and authorization.  
In the 1st place it authenticate the user by password → db  
or by checking the credentials with **Google OAuth** service.  
Once authentication is successful it issues a signed **JWT** through the **NextAuth.js** module.  
This signed JWT is then sent into the user's browser as a cookie.

---

## Google connection service

Hosted on an **Azure App Function**.  
This service is connected to **auth-service** and redirects user's Google social connection credentials to the **Google OAuth** service for identity verification.
