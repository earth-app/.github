# 🤝 Contributing to The Earth App

Thanks for your interest in contributing! 🌱 The Earth App is a multi-repository
project and each repository has its own build and test tooling, but the
policies, workflow, and expectations below apply everywhere in the
[earth-app](https://github.com/earth-app) organization.

If this is your first time contributing here, please read this document from
top to bottom before opening a pull request.

## Table of Contents

- [Ways to Contribute](#ways-to-contribute)
- [Before You Start](#before-you-start)
- [Repository Map](#repository-map)
- [Development Environment](#development-environment)
- [Branches and Commits](#branches-and-commits)
- [Pull Requests](#pull-requests)
- [Code Style](#code-style)
- [Testing](#testing)
- [Documentation](#documentation)
- [Cross-Repository Changes](#cross-repository-changes)
- [AI-Assisted Contributions](#ai-assisted-contributions)
- [Security Issues](#security-issues)
- [License and Ownership](#license-and-ownership)
- [Getting Help](#getting-help)

---

## ✨ Ways to Contribute

There are many valuable ways to help:

- **Report bugs** in an issue on the affected repository. Include steps to
  reproduce, expected vs. actual behavior, and environment details (browser,
  OS, mobile OS version, app build).
- **Suggest features or improvements** in an issue. Explain the user problem
  first; propose the feature second.
- **Fix bugs** or **implement features** in a pull request.
- **Improve documentation**, including READMEs, `CLAUDE.md` files, code
  comments, and public docs at [moon](https://github.com/earth-app/moon).
- **Improve tests**, coverage, or CI ergonomics.
- **Triage** existing issues by reproducing them and adding useful context.

## 🚦 Before You Start

- Read this document.
- Read our [Code of Conduct](./CODE_OF_CONDUCT.md).
- For anything security-sensitive, follow our [Security Policy](./SECURITY.md)
  and **do not open a public issue**.
- For non-trivial changes, open an issue first so we can align on the
  approach before you invest time in a PR.

## 🗺️ Repository Map

Pick the right home for your change. A one-line summary of each repository is
in [ABOUT.md](./ABOUT.md); high-level pointers:

- User-facing bug or UI feature on the web -> `crust`.
- User-facing bug or UI feature on iOS / Android -> `sky`.
- Shared frontend logic used by both web and mobile -> `crust` (published as
  a library; `sky` consumes it via `@earth-app/crust`).
- API endpoint, data model, authentication, moderation, or business logic ->
  `mantle2`.
- AI generation, recommendations, quest validation, WebSocket notifications,
  scheduled automation -> `cloud`.
- Recommendation algorithms and shared types used across surfaces -> `ocean`.
- Marketing / landing pages -> `website`; blog posts -> `blog`; public API
  docs -> `moon`; support desk -> `smoke`.

When a change spans repositories, see [Cross-Repository Changes](#cross-repository-changes).

## 🧰 Development Environment

Common tooling across the org:

- **[Bun](https://bun.sh/)** for package management and running scripts in
  the JavaScript / TypeScript repos.
- **[Prettier](https://prettier.io/)** as the source of truth for
  formatting. Husky and lint-staged run it automatically on commit in most
  repos.
- **TypeScript strict mode** where applicable.

Per-repository specifics:

| Repository       | Runtime / Language          | Package Manager | Test Runner        |
| ---------------- | --------------------------- | --------------- | ------------------ |
| `crust`, `sky`, `blog`, `website`, `smoke` | Nuxt 4 / TypeScript | Bun         | Vitest             |
| `cloud`          | Cloudflare Workers / TypeScript | Bun         | Vitest + `@cloudflare/vitest-pool-workers` |
| `mantle2`        | PHP 8.4 / Drupal 11         | Composer + Bun  | PHPUnit 11         |
| `ocean`, `shovel` | Kotlin Multiplatform       | Gradle          | Gradle (`jvmTest`, `jsTest`) |
| `verdant`        | Kotlin / Compose Multiplatform | Gradle       | Gradle             |
| `moho`, `CollegeDB`, `doc2lora`, `rain` | TypeScript / Node | Bun / npm | Vitest             |

Each repository's `README.md` and, when present, `CLAUDE.md` document the
canonical local development commands. Follow those. Do not add new build tools
without discussion.

## 🌿 Branches and Commits

- The default branch is **`master`** (or the repository's stated default).
- Create a feature branch off `master`. Suggested names: `feat/<slug>`,
  `fix/<slug>`, `docs/<slug>`, `refactor/<slug>`, `chore/<slug>`.
- Keep branches focused. One logical change per pull request.
- Use [Conventional Commits](https://www.conventionalcommits.org/) for
  commit subjects:
  - `feat: add daily quest chip to navbar`
  - `fix: prevent cache poisoning in mantle2 user quests`
  - `docs: clarify sky OAuth callback flow`
  - `refactor: consolidate user helpers into UsersHelper`
- Wrap subjects at ~72 characters. Explain the *why* in the body when it is
  not obvious from the diff.
- Do not force-push to `master` under any circumstance. Force-push on your
  own feature branch is fine.

## 🚀 Pull Requests

Before opening a PR, verify:

- The branch is up to date with `master`.
- `bun run prettier:check` (or the repo's equivalent) passes.
- The relevant test suite passes locally.
- Types are complete: no `any` sprinkled in, no `@ts-ignore` without a
  written justification.
- Docs are updated: README sections, TSDoc / JSDoc on any new public API,
  the appropriate `CLAUDE.md` if a workflow or tooling assumption changed.

Then open the PR against `master` and:

- Fill in the PR template. If the repo doesn't have one, include a short
  **Summary**, a **Motivation** (link the issue if any), and a **Test Plan**
  as a checklist.
- Reference related PRs in sibling repositories with `earth-app/<repo>#<pr>`.
- Keep PRs reviewable. If a change grows past ~500 lines of diff, split it
  or explain why it can't be split.
- Respond to review comments in the PR thread; don't rewrite history in ways
  that lose that discussion until the PR is ready to merge.

We typically squash-merge PRs unless the branch was authored as a clean
series of commits.

## 🎨 Code Style

### General

- Prefer editing existing files over creating new ones.
- Consolidate related logic into the owning file (e.g., new user logic goes
  into the existing `UsersHelper` in `mantle2`, new user composables go into
  `useUser.ts` in `crust`) rather than spreading it across parallel files.
- Follow the comment house style: short, lowercase, no trailing period; only
  when the *why* is non-obvious. Don't add file-header comments.
- Use plain ASCII in code, strings, and comments (no smart quotes, em
  dashes, arrows).

### Frontend (Nuxt / Vue)

- `<template>` precedes `<script setup>` in `.vue` files; Prettier will
  reorder if not.
- Title Case for UI titles (buttons, tabs, headings, dropdowns); sentence
  case for body copy.
- Nuxt-auto-imported components live in `components/`; nested folders use
  the shorthand file name (`user/Card.vue`, not `user/UserCard.vue`).
- Tailwind v4: use `wrap-break-word` (not the deprecated `break-words`);
  prefer bare-number utilities where they're equivalent (`flex-2` not
  `flex-[2]`).

### Backend (mantle2 / PHP)

- Keep changes local to the owning controller, helper, or YAML config.
- Keep `mantle2.routing.yml`, `mantle2.services.yml`, and
  `mantle2.caching.yml` in sync with the code and their unit tests.
- Use PHPStan and PHP CodeSniffer clean.

### Cloud (Workers / TypeScript)

- Do not change API shapes on `/v1/*` without checking the corresponding
  Mantle2 call sites and shared schemas.
- Prefer targeted tests near the touched behavior. Keep AI output sanitizers
  strict.

## 🧪 Testing

Every feature and bug fix should ship with tests in the same PR.

- **Unit / integration tests** run in CI on every push and PR.
- **Manual verification** is expected for anything user-visible on `crust`
  and `sky`. Note in the PR description what you tested and on which
  platforms.
- For contract changes that span `mantle2` <-> `cloud` <-> `crust` /
  `sky`, add or update tests on both sides of the contract.

## 📚 Documentation

Documentation is part of the change, not a follow-up:

- Update the affected repository's `README.md` when public workflow,
  environment variables, or scripts change.
- Update `CLAUDE.md` when a project convention or workflow assumption
  changes.
- Update [moon](https://github.com/earth-app/moon) when the public API
  surface (`/v1/*` on Cloud, `/v2/*` on Mantle2) changes.
- Update this file if the contribution workflow itself changes.

## 🔀 Cross-Repository Changes

When a change spans repositories (contract changes, shared types, deploy
coordination):

1. Land the source-of-truth change first (usually `ocean` for shared types,
   `mantle2` or `cloud` for API surfaces).
2. Open sibling PRs in the affected consumer repositories that reference the
   source PR by URL.
3. In the source PR description, list the consumer PRs and their status.
4. Merge in dependency order: shared library / contract first, then
   consumers.
5. If the change is backwards-incompatible, coordinate deploy timing and
   note it in each PR description.

Crust web changes usually need a matching Sky change. Contract changes usually
span Mantle2, Cloud, and both frontends.

## 🤖 AI-Assisted Contributions

Using AI tools to help write code is fine. That said:

- **You are responsible for what you submit.** Read every line of AI-produced
  code before opening a PR. Confirm it compiles, passes tests, and does what
  you claim.
- **Do not submit code you don't understand.** Reviewers will ask, and
  "the model wrote it" is not an acceptable answer.
- **Do not paste proprietary code, secrets, or user data into an AI tool.**
- **Disclose when it's material.** For substantial AI-assisted contributions
  (large features, refactors), a one-line note in the PR description is
  appreciated.
- **Follow The Earth App's AI content policy** for anything user-facing.
  AI-generated user-visible content is disclosed as such at the surface
  where it appears, in line with our
  [Privacy Policy](https://earth-app.com/privacy-policy).

## 🔒 Security Issues

**Never open a public issue or PR for a security vulnerability.** Follow the
[Security Policy](./SECURITY.md) and report privately. Coordinated
disclosure via a GitHub Security Advisory on the affected repository is our
preferred channel.

## 🪪 License and Ownership

By contributing to any Earth App repository, you agree that your
contributions are licensed under the same license as that repository
(typically Apache 2.0 or MIT; see each repo's `LICENSE`). You retain
copyright to your contributions but grant The Earth App the right to
redistribute them under the same terms.

The Earth App is founded and owned by **Gregory Mitchell**
([gregory@earth-app.com](mailto:gregory@earth-app.com),
[@gmitch215](https://github.com/gmitch215)). The organization is registered
in Cook County, Illinois, USA.

## 💬 Getting Help

- **General questions**: open a discussion or issue on the relevant
  repository.
- **Support requests**: [support@earth-app.com](mailto:support@earth-app.com)
  or the portal at
  [support.earth-app.com](https://support.earth-app.com).
- **Security**: see the [Security Policy](./SECURITY.md).
- **Sensitive concerns for ownership**:
  [gregory@earth-app.com](mailto:gregory@earth-app.com).

Thanks for helping build The Earth App. 🌎💚
