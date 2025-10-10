# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **static marketing website** for Frost Roofing, a Brisbane & Gold Coast roofing company specializing in Colorbond roof replacements. The site was built using **Webflow** and exported as static HTML/CSS/JS files.

**Business Focus**: The site is designed to generate leads through a multi-step application form that collects roofing replacement requirements and schedules in-person quotes.

## Architecture

### Technology Stack
- **Webflow** (exported static site)
- **Static HTML/CSS/JavaScript** (no build process)
- **Typeform** integration for lead capture form
- **Webflow.js** for interactions and animations
- **jQuery 3.5.1** (bundled with Webflow)

### File Structure
```
frost-roofing.webflow/
├── index.html           # Main homepage
├── apply.html           # Application/quote form page
├── styleguide.html      # Style guide (design reference)
├── css/
│   ├── normalize.css              # CSS reset
│   ├── webflow.css                # Webflow framework styles
│   └── frost-roofing.webflow.css  # Custom project styles
├── js/
│   └── webflow.js       # Webflow interactions library
└── images/              # All image assets (SVG, PNG, AVIF)
```

### Page Structure

**index.html** - Single-page marketing site with sections:
- Header/Navigation with logo, nav links, and CTA buttons
- Hero section highlighting Colorbond roof replacement services
- Services section (Replacements, New Roofs, Architectural Cladding, Skylights)
- Partners logo section
- Testimonials/reviews section
- Process steps (3-step process explanation)
- Recent projects showcase (Norman Park, Alexandra Hills, Broadbeach)
- Benefits section ("Protect Your Home" with 4 feature cards)
- About Us section (company story)
- Final CTA section
- Footer with contact info and quick links

**apply.html** - Lead generation page:
- Back button to return to homepage
- Three-step process explanation
- "Continue" button that reveals embedded Typeform
- Typeform embed (ID: `01K6QEV7RX98J10R9PCX8AE440`)

## Key Implementation Details

### Webflow Interactions
- Elements with `data-w-id` attributes have Webflow-powered animations/interactions
- Project showcase section uses custom animations to toggle between 3 projects (Norman Park, Alexandra Hills, Broadbeach Water)
- Recent projects have opacity animations controlled via inline styles and Webflow interactions

### Typeform Integration
- Form is embedded in `apply.html` using Typeform's embed script
- Initially hidden with `display:none`
- Revealed when user clicks "Continue" button
- Collects roofing requirements for personalized quotes

### Responsive Design
- Mobile navigation toggle (hamburger menu)
- Responsive images with srcset for different viewport sizes
- `.hide-mobile` class hides elements on mobile devices
- Container max-width: 82rem (1312px) with 2rem padding

### Custom Color Classes
Typography and color modifiers use combo classes:
- `.cc-text-primary` - Dark green (#14301a)
- `.cc-text-secondary` - For highlighted text in headings
- `.cc-text-tertiery` - Light green with opacity
- `.cc-text-white` / `.cc-text-black`
- `.cc-weight-medium` / `.cc-weight-semibold` / `.cc-weight-bold`

### Fonts
Loaded from Google Fonts:
- **Roboto** (body text)
- **Inter Tight** (headings)
- **Inter** (UI elements)

## Working with This Site

### Making Content Changes
1. Edit HTML files directly - no build process needed
2. Changes to text, images, or links can be made in the HTML
3. Test by opening HTML files in a browser

### Updating Styles
- Custom styles are in `css/frost-roofing.webflow.css`
- Webflow framework styles in `css/webflow.css` (usually shouldn't be edited)
- Typography scale: text-14, text-16, text-18, text-20, text-24, text-32
- Heading scale: h1, h2, h3, h4, h5

### Adding/Changing Images
- Place images in `/images/` directory
- Use responsive image patterns with srcset for different sizes
- Format: `-p-500`, `-p-800`, `-p-1080`, `-p-1600`, `-p-2000`, `-p-2600` suffixes

### Deployment
This is a static site - upload all files to any static hosting service:
- Netlify
- Vercel
- AWS S3 + CloudFront
- GitHub Pages
- Traditional web hosting

No build commands or server-side processing required.

### Form/Lead Management
- The Typeform embed on `apply.html` handles all form submissions
- To change the form, update the Typeform ID in the `data-tf-live` attribute
- Form responses are managed in Typeform dashboard (not in this codebase)

## Important Notes

- **Do not modify** `webflow.js` or `webflow.css` - these are Webflow's framework files
- **Webflow interactions** are controlled by `data-w-id` attributes - removing these will break animations
- The site uses **hash-based navigation** (`#services`, `#projects`, `#reviews`, `#about-us`) for smooth scrolling on the homepage
- **No backend** - this is purely static HTML/CSS/JS

## Contact Information in Site
- Phone: 0406 643 290 / 0412 517 411
- Email: admin@frostroofing.com.au
- Service Area: Brisbane & Gold Coast, Queensland

## Common Edits
- **Update phone/email**: Search for phone numbers and email in HTML files
- **Change CTA button text**: Search for "Apply For An In-Person Quote"
- **Update testimonials**: Edit content in testimonial-card divs
- **Modify project showcases**: Update recent-item sections with new project details/images
- **Change partner logos**: Replace SVG files in images/ directory and update references
