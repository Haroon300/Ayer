# NOCTRA STUDIO — React + Vite

A responsive dark-fantasy creative studio portfolio starter built with React, Vite, Tailwind CSS, React Router, Framer Motion and Lucide icons.

## Run locally

1. Install Node.js (LTS).
2. Extract this project and open its folder in VS Code.
3. In the VS Code terminal run:

   ```bash
   npm install
   npm run dev
   ```

4. Open the local URL Vite prints, usually `http://localhost:5173`.

## Demo admin

The admin dashboard is at `/admin`. To enable the *local demo gate*, create a `.env` file in the project root:

```env
VITE_DEMO_ADMIN_PASSWORD=change-this-demo-password
```

Restart `npm run dev`, then use that value on the login page.

**Security warning:** `VITE_*` variables are exposed to the browser. This gate is only for local UI demonstration and is NOT secure authentication. Do not deploy it as real access control.

## Current demo behavior

- Portfolio category filters and artwork detail modal work.
- Admin add/delete artwork works in the current browser using localStorage.
- Contact form saves inquiries to localStorage in the current browser.
- Uploaded demo images are stored as base64 in localStorage and limited to 3 MB. This is not suitable for production.
- Starter artwork photos use remote Unsplash URLs as placeholders. Replace them with licensed/owned artwork before launch.

## Production checklist

- Configure Supabase project, Auth, database tables, Storage bucket and Row Level Security policies.
- Only allow authenticated admin users to insert/update/delete portfolio records and upload files.
- Send commission inquiries to a server-side endpoint, Supabase Edge Function, or trusted form provider; never rely on localStorage for customer leads.
- Replace sample artwork and contact details with studio-owned content.
- Add privacy policy, terms, accessibility review, image optimization, SEO metadata and error states.
- Test build with `npm run build`.
- Deploy the frontend to Vercel; configure environment variables and SPA routing as needed.

## Suggested Supabase tables

`artworks`: `id uuid primary key`, `title text`, `category text`, `type text`, `year text`, `image_url text`, `description text`, `created_at timestamptz`.

`inquiries`: `id uuid primary key`, `name text`, `email text`, `project_type text`, `budget text`, `deadline text`, `brief text`, `created_at timestamptz`.

Enable RLS. Public users should only be able to read published artwork and submit inquiries through a controlled insert policy or server-side function. Admin write access should require a verified authenticated role.
