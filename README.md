# What's New — Winsupply eCommerce Platform

**Live page:** https://yagozardo.github.io/winsupply-whats-new/

---

## About

This is a proof-of-concept landing page for a **"What's New"** release announcement feature on the Winsupply eCommerce platform, built as part of the AMVS-26 release campaign.

The concept is inspired by [Dia Browser's release notes pages](https://diabrowser.com) — a clean, editorial-style page that greets users with the highlights of a new release: what changed, what's better, and why it matters to them. The goal is to bring that same experience to Winsupply.com, so customers are informed and excited each time a meaningful update ships.

## Concept

Instead of a generic changelog, the **What's New** page is designed to:

- Welcome customers to a new version of the platform with a clear headline and date
- Walk through the key improvements in a scannable, visually engaging layout
- Feel like a product moment, not a patch note

This proof of concept covers the March 2025 release of Winsupply.com — a major platform upgrade focused on speed, smarter ordering, and a cleaner experience.

## Stack

No build step, no framework. The page is intentionally lightweight:

- Plain HTML + CSS
- [Tailwind CSS](https://tailwindcss.com) via CDN (with custom design tokens)
- [Satoshi](https://fontshare.com/fonts/satoshi) (headings) + [Inter](https://fonts.google.com/specimen/Inter) (body) from Google Fonts / Fontshare
- Design tokens from the Winsupply design system, mapped as CSS custom properties in `styles.css`

## Files

```
WhatsNew/
├── index.html          # Page markup and Tailwind config
├── styles.css          # Design tokens (CSS custom properties) + base styles
└── assets/
    ├── logo-winsupply.png
    └── icon-arrow.svg
```

## Running locally

Just open `index.html` in a browser — no server required.
