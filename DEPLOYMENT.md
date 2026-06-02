# 🚀 Deployment Guide for RecipeCloud

This guide will help you deploy your RecipeCloud application to production using **Vercel** and **Supabase**.

## 1. Supabase Production Setup

Before deploying the frontend, ensure your Supabase project is ready for production:

### Database Schema
Ensure all tables (`users`, `recipes`) and Row-Level Security (RLS) policies are correctly set up as described in `SETUP.md`.

### Google OAuth Configuration
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create **OAuth client ID** for a **Web application**.
3. Add your production URL (e.g., `https://recipecloud-yourname.vercel.app`) to **Authorized JavaScript origins**.
4. Add your Supabase callback URL to **Authorized redirect URIs** (Found in Supabase Dashboard > Auth > Providers > Google).
5. In Supabase Dashboard, go to **Auth > Providers > Google**, enter the Client ID and Secret, and Save.

### Site URL & Redirects
In Supabase Dashboard > **Auth > URL Configuration**:
- **Site URL**: `https://recipecloud-yourname.vercel.app`
- **Redirect URLs**: Add `https://recipecloud-yourname.vercel.app/auth/callback`

---

## 2. Deploying to Vercel

Vercel is the recommended platform for deploying Next.js applications.

### Option A: Using Vercel CLI (Quickest)
1. Install Vercel CLI: `npm i -g vercel`
2. Run `vercel` in the project root.
3. Follow the prompts to link your project.
4. When asked for environment variables, add the following in the Vercel Dashboard:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `GEMINI_API_KEY`

### Option B: Using GitHub Integration (Recommended)
1. Push your code to a GitHub repository.
2. Go to [Vercel](https://vercel.com) and click **New Project**.
3. Import your repository.
4. In the **Environment Variables** section, add:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `GEMINI_API_KEY`
5. Click **Deploy**.

---

## 3. Post-Deployment Check

Once deployed, verify the following:
1. **Authentication**: Try signing in with Google. If it fails, check the "Authorized redirect URIs" in Google Cloud Console.
2. **Image Uploads**: Upload a recipe image to ensure Supabase Storage is working.
3. **Nutrition Analysis**: Ensure the Gemini API is correctly analyzing recipe data.

---

## 🛠 Troubleshooting

- **Auth Redirect Issues**: Ensure the `NEXT_PUBLIC_SUPABASE_URL` in Vercel matches your Supabase project.
- **Build Errors**: Ensure you are using `pnpm` or `npm` consistently. Vercel usually detects this automatically.
- **Environment Variables**: If features aren't working, double-check that all keys in Vercel Dashboard are correct and have no trailing spaces.
