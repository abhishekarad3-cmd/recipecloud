# 🌿 RecipeCloud — Cloud Recipe App

Full-stack recipe community: Next.js 15 + Supabase + Tailwind CSS.

---

## 📁 Project Structure

```
src/
├── app/
│   ├── layout.tsx          ← Root layout (AuthProvider)
│   ├── page.tsx            ← Main page — all sections assembled
│   └── not-found.tsx
├── components/
│   ├── Navbar.tsx          ← Sticky, auth-aware
│   ├── RecipeCard.tsx      ← Rating + favorites
│   ├── Footer.tsx
│   └── sections/
│       ├── HeroSection.tsx
│       ├── RecipesSection.tsx   ← Live + search/filter
│       ├── CategoriesSection.tsx
│       ├── UploadSection.tsx    ← Image upload + points
│       ├── ProfileSection.tsx   ← Profile + delete recipes
│       └── LeaderboardSection.tsx
├── context/AuthContext.tsx ← Global Supabase auth state
├── lib/supabase.ts         ← Supabase init
└── services/
    ├── recipes.ts          ← Supabase database + Storage
    └── users.ts            ← User CRUD + leaderboard
```

---

## ⚙️ Setup

### 1. Create Supabase Project
→ [supabase.com](https://supabase.com) → New Project

### 2. Enable Services
- **Authentication** → Providers → Enable **Google**
- **Database** → Create tables as defined in `SETUP.md`
- **Storage** → Create `recipe-images` bucket (Public)

### 3. Get Config Keys
Project Settings → API → copy `URL` and `anon public` key

### 4. Add Environment Variables
```bash
cp .env.example .env.local
# Fill in your Supabase keys
```

### 5. Apply Security Rules (RLS)
Follow the policies outlined in `SETUP.md` for `users` and `recipes` tables.

### 6. Run
```bash
pnpm install
pnpm dev
# → http://localhost:4028
```

---

## 🔒 Security
- Read: Public
- Write recipe: Auth required
- Delete: Author only
- Rate: Once per user

## 🚀 Deploy
```bash
npx vercel
# Add env vars in Vercel dashboard
```

## Project Status

All features have been implemented, and the Supabase environment (database schema, storage buckets, and RLS policies) has been fully configured.
