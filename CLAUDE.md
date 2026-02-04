# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

JC Consultant is a template-based system for generating showcase websites ("sites vitrines") for auto-entrepreneurs in France who don't yet have a web presence. Target businesses have 10+ Google reviews but no website. Each client site is cloned from the template, customized, and deployed on Vercel with a temporary free URL for demo purposes (1-2 weeks).

## Tech Stack

- **Framework**: Astro (static site generator)
- **Styling**: Tailwind CSS
- **Hosting**: Vercel (free tier, auto-deploy on git push)
- **Forms**: Tally Forms (free, unlimited)
- **Booking/Reservations**: Cal.com widget (free tier) or Google Calendar API
- **Maps**: Google Maps Embed API
- **Language**: French (all client-facing content is in French)

## Development Commands

```bash
npm install          # Install dependencies
npm run dev          # Local dev server (http://localhost:4321)
npm run build        # Production build to dist/
npm run preview      # Preview production build locally
```

## Deployment Workflow

1. Clone this template repo for each new client
2. Customize content, images, and colors
3. Create a new GitHub repo: `gh repo create client-name --public --source=. --remote=origin --push`
4. Import the repo on Vercel (auto-detects Astro) or run `vercel --prod`
5. Share the `client-name.vercel.app` URL with the client
6. Any subsequent `git push` triggers automatic redeployment

## Architecture

```
src/
├── components/       # Reusable Astro components
│   ├── Header.astro
│   ├── Hero.astro
│   ├── Services.astro
│   ├── Gallery.astro
│   ├── Reviews.astro  # Google reviews display
│   ├── Map.astro      # Google Maps embed
│   ├── Booking.astro  # Cal.com widget integration
│   ├── Contact.astro  # Tally Forms embed
│   └── Footer.astro
├── layouts/
│   └── Layout.astro   # Base HTML layout with SEO meta tags
├── pages/
│   └── index.astro    # Single-page site entry point
└── data/
    └── site.json      # Client-specific data (name, address, services, colors, etc.)
public/
└── images/            # Client photos and assets
```

## Key Design Decisions

- **Single-page sites**: Each client site is a single `index.astro` page composed of section components. No multi-page routing needed.
- **Data-driven customization**: All client-specific content (business name, services, phone, address, colors) lives in `src/data/site.json`. Components read from this file, so creating a new client site means editing one JSON file and dropping in photos.
- **No backend**: Sites are fully static. Forms go through Tally, bookings through Cal.com widget. No server-side code.
- **Mobile-first responsive**: Target clients are local service providers whose customers search on mobile.
- **Performance**: Aim for Lighthouse 100/100. Astro outputs zero JS by default.

## Customization per Client

Edit `src/data/site.json` with:
- Business name, tagline, description
- Address and phone number
- List of services with descriptions and prices
- Brand colors (primary, secondary, accent)
- Google Maps place ID or coordinates
- Cal.com booking link (if applicable)
- Social media links

Then add client photos to `public/images/`.
