# Contributing to Minerva Connect

Thanks so much for wanting to help! ✨ This is a small, fun project and I'd love to have you involved. Before you dive in, just give the [README](README.md) a quick skim so you know what we're building here.

## Hey, I'm Emmanuel 👋

I'm an incoming second-year student at Minerva University, and this is my first solo project here on GitHub. This is a *small* project—no pressure, no corporate bureaucracy. Most of the issues are beginner-friendly, so whether you're just getting started with open source or you've got more experience, this is a great place to contribute and learn together. If you get stuck, just ask. I'm here to help.

## Quick note on usage rights

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

Forking, cloning, and using the code is permitted under the terms of the MIT license, including contributions via pull request.

## What this project is

Minerva Connect matches Minerva University applicants with current students for verified Q&A. It's a vanilla HTML, CSS, and JavaScript static site backed by [Supabase](https://supabase.com). See the [README](README.md) for the full picture.

## Setup 🛠️

1. **Fork and clone** this repository (for contribution purposes, per the note above).

2. **Run the app.** It's a static site that talks to a shared Supabase backend. The connection details are already in `js/jsconfig.js`, so there's nothing to configure. Just serve the folder:
   ```bash
   python3 -m http.server 8000
   ```
   Open http://localhost:8000.

That's it. You're connected to the same database the live app uses.

### Testing the Minervan side locally 🔐

The student-facing dashboard normally requires a `@uni.minerva.edu` magic-link login. So contributors can see that side without a Minerva email, there's a local-only dev login:

- Click **Minervan Login**, enter **`login@login.com`**, and submit. No email or magic link is sent. You're taken straight into the Minervan dashboard.
- This bypass **only works on `localhost`**. It does nothing on the live site, so it's safe.

If `login@login.com` doesn't log you in, the shared test user may need to be (re)created in Supabase. Open an issue and I'll sort it out.

> 🔑 **Note on the Supabase key:** the `SUPABASE_ANON_KEY` in `js/jsconfig.js` is a *public* key. It's meant to ship in browser code, so committing it is expected and safe. Data is protected by Row Level Security policies on the database, not by hiding the key. **Please don't commit any other secrets** (`.env` files, service keys, and similar). Those are gitignored for a reason.

## Brand and guardrails standards 🎨

This is a Minerva-aligned project, so contributions need to respect two things:

**Brand standards**: the official Minerva Fall 2025 look. The full guide is in [MU Branding Guidelines/](MU%20Branding%20Guidelines/), and the palette is defined as CSS variables in [css/styles.css](css/styles.css). When you add or change UI:
- Use the existing `--mu-*` color tokens (such as `--mu-obsidian`, `--mu-bone`, `--mu-clay`). Don't hardcode new hex values.
- Keep serif for headings, sans-serif for body.
- Maintain WCAG AA contrast and responsive layouts.

**AI Guardrails** 🤖: see [Guardrails Docs/](Guardrails%20Docs/). In short: keep humans accountable, minimize the personal data we collect (no sensitive PII), and preserve the in-app "AI-Assisted" disclosure. If your change uses AI features, disclose it.

## Making changes 💪

- Branch off `main`, make your change, and test it locally against the shared backend.
- Keep things consistent with the brand and guardrails above.
- Open a pull request with a description of **what** you changed and **how** you tested it. That's it!

## Got questions?

Just open an issue! I genuinely enjoy helping people get unstuck, so don't hesitate. Thanks for being here, and excited to work with you 🚀
