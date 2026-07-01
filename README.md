# Hamza — Cinematic Developer Portfolio

An immersive, scroll-driven 3D developer portfolio built with Next.js, React Three Fiber, GSAP, and Lenis. Features a cinematic camera that flies through 6 scenes, post-processing bloom, adaptive performance tiers, a full case study modal, and a working contact form that delivers messages to your inbox via Resend.

---

## 📧 Contact Form Setup (IMPORTANT — read before deploying)

The contact form sends emails to **hamzaa77005@gmail.com** using [Resend](https://resend.com). You need to add ONE environment variable for it to work:

### Get your free Resend API key
1. Go to [resend.com](https://resend.com) → sign up (free, no credit card)
2. Dashboard → **API Keys** → **Create API Key** → copy the `re_...` key
3. That's it — you get 100 emails/day free

### Add the key to Vercel
- **Vercel dashboard** → your project → **Settings** → **Environment Variables**
- Add:
  ```
  RESEND_API_KEY = re_your_key_here
  ```
- **Redeploy** (Settings → Environment Variables won't take effect until next deploy)

### Verify it works
After deploying, fill out the contact form on your live site. The message should arrive in `hamzaa77005@gmail.com` within seconds. Reply directly to that email to respond to the sender.

### Optional env vars
| Variable | Default | Description |
|----------|---------|-------------|
| `RESEND_API_KEY` | _(required)_ | Your Resend API key |
| `CONTACT_EMAIL` | `hamzaa77005@gmail.com` | Where messages are delivered |
| `RESEND_FROM_EMAIL` | `Portfolio <onboarding@resend.dev>` | Sender address. For production, verify your domain in Resend and use `noreply@yourdomain.com` |

> **Note:** The default `onboarding@resend.dev` sender works on the free plan for testing. For a production portfolio, verify your domain in Resend to use a custom sender address.

---

## 🚀 Deploy to Vercel (3 options)

### Option A — Drag & Drop (fastest)
1. Unzip this folder.
2. Go to [vercel.com/new](https://vercel.com/new).
3. Drag the unzipped folder onto the page.
4. Vercel auto-detects Next.js. Click **Deploy**.
5. **Then** add `RESEND_API_KEY` in Settings → Environment Variables and redeploy.

### Option B — GitHub (recommended for updates)
1. Unzip this folder.
2. Create a new GitHub repository (e.g. `hamza-portfolio`).
3. Push the files:
   ```bash
   cd hamza-portfolio
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/hamza-portfolio.git
   git push -u origin main
   ```
4. Go to [vercel.com/new](https://vercel.com/new) → **Import Git Repository**.
5. Select your repo → add `RESEND_API_KEY` env var → click **Deploy**.
6. Every future `git push` auto-deploys.

### Option C — Vercel CLI
```bash
npm i -g vercel
cd hamza-portfolio
vercel
```
Follow the prompts. Then `vercel --prod` to deploy to production.

---

## 💻 Run Locally

```bash
npm install
cp .env.example .env.local
# Edit .env.local and add your RESEND_API_KEY
npm run dev
```
Open [http://localhost:3000](http://localhost:3000).

> Requires Node.js 18.18+ (Node 20 recommended).

---

## 🛠 Tech Stack

| Layer | Tech |
|-------|------|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript 5 |
| Styling | Tailwind CSS 4 + shadcn/ui |
| 3D | React Three Fiber + Three.js + Drei |
| Post-processing | @react-three/postprocessing |
| Animation | Framer Motion + GSAP |
| Smooth Scroll | Lenis |
| Email | Resend (serverless API route) |
| Icons | Lucide React + React Icons |

---

## 📁 Project Structure

```
hamza-portfolio/
├── src/
│   ├── app/
│   │   ├── layout.tsx              # Root layout + fonts + SEO
│   │   ├── page.tsx                # Main page (assembles all scenes)
│   │   ├── globals.css             # Theme, palette, utilities
│   │   └── api/
│   │       └── contact/
│   │           └── route.ts        # Email API route (Resend)
│   ├── components/
│   │   ├── portfolio/
│   │   │   ├── three/              # 3D canvas, camera rig, particles, PostFX
│   │   │   ├── scenes/             # 6 scene pairs (3D + DOM overlay)
│   │   │   ├── LoadingScreen.tsx
│   │   │   ├── CursorGlow.tsx
│   │   │   ├── MagneticButton.tsx
│   │   │   ├── TiltCard.tsx
│   │   │   ├── TopNav.tsx
│   │   │   ├── ScrollProvider.tsx
│   │   │   ├── SmoothScroll.tsx
│   │   │   ├── SceneTransitionFlash.tsx
│   │   │   └── CaseStudyModal.tsx
│   │   └── ui/                     # shadcn/ui components
│   └── lib/
│       ├── utils.ts
│       └── hooks.ts
├── public/
│   ├── logo.svg
│   └── robots.txt
├── next.config.ts
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── postcss.config.mjs
├── components.json
├── eslint.config.mjs
├── vercel.json
├── .env.example
└── .gitignore
```

---

## 🎨 Customization

### Update content
All text content lives in `src/components/portfolio/scenes/`:
- `HeroSection.tsx` — headline, description, CTAs
- `AboutSection.tsx` — 4 glass panels (About Me, Journey, Current Focus, Goals)
- `SkillsSection.tsx` — skill groups + 3D orbiting icons
- `ProjectsSection.tsx` — project cards + case study trigger
- `LearningSection.tsx` — timeline milestones
- `ContactSection.tsx` — social links (LinkedIn, WhatsApp, Email) + contact form
- `CaseStudyModal.tsx` — full Davaam case study content

### Update contact info
Edit `src/components/portfolio/scenes/ContactSection.tsx`:
```ts
const EMAIL = "hamzaa77005@gmail.com";
const WHATSAPP_NUMBER = "03182772524";
const WHATSAPP_INTL = "923182772524"; // for wa.me link
```

### Update colors
Edit `src/app/globals.css` → `:root` variables.

---

## ⚡ Performance

The site includes an adaptive performance tier system (`src/components/portfolio/three/usePerfTier.ts`) that automatically adjusts quality based on hardware:

| Tier | PostFX | Reflector | Particles | DPR |
|------|--------|-----------|-----------|-----|
| Low  | Off    | Off       | 200       | 0.6–0.85 |
| Medium | On   | Off       | 400       | 0.75–1.0 |
| High | On     | On        | 600       | 1.0–1.5 |

---

## 📝 Notes

- **Contact form:** Messages go to `hamzaa77005@gmail.com` via Resend. Requires `RESEND_API_KEY` env var (see setup above).
- **WhatsApp link:** Clicking the WhatsApp card opens `https://wa.me/923182772524` (international format).
- **Davaam Live Demo:** Links to `https://davaam.vercel.app`.
- **LinkedIn link:** Currently `https://www.linkedin.com/` — update with your profile URL in `ContactSection.tsx`.

---

## 📄 License

MIT — free to use and modify.
