# 🌎 The Earth App

> Go outside. 🌱

The Earth App is a social platform for discovering activities, sharing experiences,
and building a habit of getting out into the world. Users log activities, respond to
daily prompts, RSVP to events, earn badges, run quests with real-world evidence
capture, and follow curated science journalism - all in one place, on the web and on
mobile.

🔗 Explore it at **[earth-app.com](https://earth-app.com)**.

---

## 🧩 Products

The Earth App ships as a set of coordinated surfaces, each in its own repository so
they can move independently:

### 🖥️ Consumer surfaces

- **[crust](https://github.com/earth-app/crust)** - the Nuxt 4 web frontend at
  `earth-app.com`. Hybrid SSR/ISR/SWR, edge-deployed via NuxtHub on Cloudflare
  Workers. It also publishes as a library so the mobile shell can extend it.
- **[sky](https://github.com/earth-app/sky)** - the Ionic Vue + Capacitor mobile app
  for iOS and Android. Extends `@earth-app/crust` and adds native tab navigation,
  deep links, push notifications, offline mode, and Capacitor-backed preferences.
- **[website](https://github.com/earth-app/website)** - the top-level marketing
  landing surface.
- **[blog](https://github.com/earth-app/blog)** - the official Earth App blog,
  powered by [NuxtPress](https://github.com/gmitch215/nuxtpress) on Cloudflare D1
  and KV.
- **[moon](https://github.com/earth-app/moon)** - public API documentation and
  technical specifications.

### ⚙️ Backend services

- **[mantle2](https://github.com/earth-app/mantle2)** - the core REST API. A custom
  Drupal 11 module on PHP 8.4 with 200+ endpoints, bearer-token auth, OAuth
  provider sign-in (Google, Microsoft, Discord, GitHub, Facebook, Apple), rate
  limiting, Redis-backed caching, and OpenAPI / Swagger UI docs.
- **[cloud](https://github.com/earth-app/cloud)** - the Hono.js Cloudflare Workers
  service behind the automation. Runs AI-driven content generation,
  recommendations, semantic ranking, quest validation, real-time WebSocket
  notifications, image scoring, and scheduled jobs. Uses KV, R2, Durable Objects,
  Cloudflare Images, and Workers AI.
- **[ocean](https://github.com/earth-app/ocean)** - the shared Kotlin
  Multiplatform library for recommendation algorithms and cross-surface types
  (also published to npm and Maven).

### 🛠️ Content and tooling

- **[verdant](https://github.com/earth-app/verdant)** - Virtual Garden algorithm
  and a Compose Multiplatform companion application.
- **[recess](https://github.com/earth-app/recess)** - "Go Outside" tooling around
  the core experience.
- **[rain](https://github.com/earth-app/rain)** - the social media content
  generator. Turns Earth App data into vertical short-form videos (Remotion,
  Cloudflare TTS, Whisper) and photo posts.
- **[moho](https://github.com/earth-app/moho)** - the curated calendar library
  (birthdays, holidays, recurring observances) that drives scheduled event
  generation.
- **[shovel](https://github.com/earth-app/shovel)** - Kotlin Multiplatform
  scraping framework used to standardize public sources.

### 📦 Libraries born here

- **[CollegeDB](https://github.com/earth-app/CollegeDB)** - a horizontal-sharding
  router for Cloudflare D1 / KV, Redis / Valkey, and Postgres / MySQL / SQLite,
  with Drizzle ORM interop.
- **[doc2lora](https://github.com/earth-app/doc2lora)** - turns a folder of
  documents (Markdown, PDF, DOCX, audio, video, images with OCR, and more) into
  a LoRA adapter for Workers AI.
- **[smoke](https://github.com/earth-app/smoke)** - the self-hostable, serverless
  customer-support desk that powers **support.earth-app.com**. Nuxt 4 on
  Cloudflare Workers with D1 + KV + R2, envelope-encrypted PII, email-native
  ticket threading, and one-click Cloudflare deploy.

---

## 🧱 Technology

We pick vanilla, boring tech and lean hard on the edge. ☁️

- **Frontend**: Nuxt 4, Vue 3, Nuxt UI v4, Tailwind CSS v4, Pinia, Zod, Luxon,
  Iconify. TypeScript strict mode everywhere.
- **Mobile**: Ionic Vue, Capacitor, native plugins for push, filesystem,
  geolocation, camera, haptics, and preferences.
- **Backend**: Drupal 11, PHP 8.4, Symfony 7, PostgreSQL / MySQL, Redis,
  OpenID Connect.
- **Edge / Automation**: Hono.js on Cloudflare Workers, KV, R2, Durable Objects,
  Cloudflare Images, Workers AI.
- **Cross-cutting**: Kotlin Multiplatform for `ocean` and `shovel`, Bun for
  package management and script running, Prettier + Husky for style, PHPUnit and
  Vitest for tests.
- **Deployment**: Cloudflare Workers via NuxtHub, Cloudflare Pages, and native
  iOS / Android builds via Capacitor.

### 🤖 A note on AI

Content on The Earth App is generated with AI. Cloud runs Meta Llama, Mistral,
OpenAI OSS, BAAI reranking and embedding models, Stable Diffusion XL Lightning,
LLaVA, ResNet-50, DETR, and OpenAI Whisper - all through Cloudflare Workers AI -
to draft article topics and summaries, generate quizzes and prompts, score and
caption user-submitted images, transcribe quest audio, generate profile photos,
enrich activity metadata, and rank recommendations. Human moderation and
validation gates sit in front of anything user-visible; suspicious device,
media, or metadata combinations are rejected rather than trusted. Everything
AI-generated is disclosed as such on the surface where it appears. See our
[Privacy Policy](https://earth-app.com/privacy-policy) for the specifics on how
we use and disclose AI.

---

## 📬 Support and legal

- **Support platform**: [support.earth-app.com](https://support.earth-app.com),
  powered by our open-source [smoke](https://github.com/earth-app/smoke) desk.
- **Support email**: [support@earth-app.com](mailto:support@earth-app.com)
- **Terms of Service**: [earth-app.com/terms-of-service](https://earth-app.com/terms-of-service)
- **Privacy Policy**: [earth-app.com/privacy-policy](https://earth-app.com/privacy-policy)
- **Refund Policy**: [earth-app.com/refund-policy](https://earth-app.com/refund-policy)
- **Security**: [SECURITY.md](./SECURITY.md)
- **Code of Conduct**: [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)
- **Contributing**: [CONTRIBUTING.md](./CONTRIBUTING.md)

The Earth App is registered in Cook County, Illinois, USA. Accounts require
users to be 13 or older. Optional paid subscriptions unlock additional features;
refunds are handled per the [Refund Policy](https://earth-app.com/refund-policy).

---

## 👤 Ownership

The Earth App is founded and owned by **Gregory Mitchell** 🧑‍💻
([@gmitch215](https://github.com/gmitch215),
[gregory@earth-app.com](mailto:gregory@earth-app.com)).

Individual repositories name their contributors in their own `CONTRIBUTORS`
files or Git history.

---

## 🪪 Open source

The Earth App's technology is open source. 💚 Most repositories ship under Apache
2.0 or MIT; check each repository's `LICENSE` file for the specific terms.

The Earth App (c) 2025 🌍
