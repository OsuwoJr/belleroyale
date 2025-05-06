# BelleRoyale Hair Salon Website

A modern, responsive website for oyale Hair salon built with SvelteKit, focusing on sustainable luxury hair services.

## Features

- **Responsive Design**: Fully responsive design that works on mobile, tablet, and desktop
- **Service Showcase**: Detailed information about salon services organized by categories
- **Online Booking System**: 3-step booking process with service, stylist, and date/time selection
- **Gallery**: Filterable gallery showcasing the salon's work
- **About Section**: Team information, salon story, and values
- **Contact Form**: Easy way for clients to reach out
- **Error Handling**: Robust error handling for missing assets and server errors

## Pages

- **Homepage**: Services overview, AR color try-on feature, and calls-to-action
- **Services**: Detailed service information organized by category
- **Gallery**: Filterable gallery of styles and transformations
- **About**: Team information, salon story, timeline, and values
- **Contact**: Contact information, form, map, and social links
- **Booking**: 3-step booking system with confirmation

## Tech Stack

- **Framework**: SvelteKit
- **Styling**: TailwindCSS
- **Typography**: Playfair Display (headings) and Lato (body text)
- **Icons**: Heroicons (SVG)
- **Deployment**: Adapter auto (configurable for various deployment targets)

## Design System

- **Colors**:
  - Gold: #D4AF37 (primary accent color)
  - Black: #000000 (background for sections)
  - Eco Green: #5D8C66 (sustainable branding accent)
  - Light Gray: #F5F5F5 (section backgrounds)
  - White: #FFFFFF (text and backgrounds)

- **Typography**:
  - Headings: Playfair Display (serif)
  - Body: Lato (sans-serif)

## Getting Started

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start development server:
   ```bash
   npm run dev
   ```
4. Add required images to the `/static/images/` directory (see `/static/images/README.md` for details)

## Building for Production

To create a production version of the site:

```bash
npm run build
```

You can preview the production build with:

```bash
npm run preview
```

## Customization

- Update salon information in each component
- Replace placeholder images with actual salon photos in `/static/images/`
- Adjust services, team members, and pricing as needed in each page component

## Image Requirements

See `/static/images/README.md` for detailed image requirements and organization.
