# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

This is a **Next.js-based developer portfolio** template built with React 18, Tailwind CSS, and Material-UI. It's designed to be easily customizable for developers to showcase their skills, projects, experience, education, and blog posts.

## Development Commands

### Run Development Server
```bash
npm run dev
```
Starts Next.js development server on http://localhost:3000 with hot-reloading enabled.

### Build for Production
```bash
npm run build
```
Creates an optimized production build.

### Start Production Server
```bash
npm start
```
Runs the production server (requires `npm run build` first).

### Install Dependencies
```bash
npm install
```

## Architecture

### Next.js Pages Structure
- **`src/pages/_app.js`**: Root application wrapper that provides ThemeContext to all pages
- **`src/pages/index.js`**: Main homepage that composes all portfolio sections and fetches blog data from dev.to API via `getStaticProps`
- **`src/pages/blog/index.js`**: Dedicated blog listing page
- **`src/pages/project/index.js`**: Dedicated projects listing page

### Component Organization
Components are organized by feature in `src/components/`:
- Each major section (About, Blog, Contacts, Education, Experience, Landing, Navbar, Projects, Skills) has its own folder
- `src/components/index.js` provides centralized exports for all components
- Card components follow a pattern: `<Feature>Card.js` for individual items within sections

### Data-Driven Content
All portfolio content is configured through plain JavaScript data files in `src/data/`:
- **`about-data.js`**: Personal description and profile image
- **`blog-data.js`**: Blog configuration (posts fetched dynamically from dev.to)
- **`contacts-data.js`**: Contact information (email, phone, location)
- **`education-data.js`**: Education history array
- **`experience-data.js`**: Work experience array
- **`header-data.js`**: Landing page header content
- **`projects-data.js`**: Projects array with demo/code links
- **`skills-data.js`**: Array of skill names (must match available skills)
- **`socials-data.js`**: Social media profile links

To customize the portfolio, edit these data files. Do NOT modify component files for content changes.

### Theme System
- **`src/contexts/theme-context.js`**: React Context providing theme state, dark/light mode toggle, and drawer state
- **`src/theme/theme.js`**: Defines `theLightTheme` and `theDarkTheme` color schemes
- Theme properties: `primary`, `secondary`, `tertiary`, `quaternary`, `quaternaryLight`, `buttonColor`, `contactsimg`, `type`
- Users can toggle between light and dark themes using the ChangeTheme component

### Skills System
- **`src/utils/skills-image.js`**: Maps skill names to SVG imports from `src/assets/svg/skills/`
- When adding skills in `skills-data.js`, use exact names that match the switch cases in `skills-image.js`
- Available skills are documented in comments at the bottom of `skills-data.js`
- Skill names are case-insensitive (converted to lowercase in the utility)

### Contact Form Integration
The Contacts component uses **EmailJS** for form submissions:
- Environment variables required: `REACT_APP_YOUR_SERVICE_ID`, `REACT_APP_YOUR_TEMPLATE_ID`, `REACT_APP_YOUR_PUBLIC_KEY`
- Copy `.env.example` to `.env` and configure with your EmailJS credentials
- Form validates email addresses using the `validator` library

### Styling Approach
- **Tailwind CSS** for utility-first styling (configured in `tailwind.config.js`)
- **CSS Modules** for component-specific styles (e.g., `contacts.module.css`)
- **Material-UI** components used selectively (Snackbar, IconButton, etc.)
- Tailwind scans `src/pages/**/*.{js,ts,jsx,tsx}` and `src/components/**/*.{js,ts,jsx,tsx}`

## Image Configuration

- External images allowed from domain: `i.ibb.co` (configured in `next.config.js`)
- To add more external image domains, update the `images.domains` array in `next.config.js`
- SVG assets stored in `src/assets/svg/` organized by feature folders

## Environment Setup

1. Copy `.env.example` to `.env`
2. Register at [EmailJS](https://www.emailjs.com/) and obtain credentials
3. Add your EmailJS service ID, template ID, and public key to `.env`

## Key Dependencies

- **Next.js 13**: React framework for SSR/SSG
- **React 18**: UI library
- **Tailwind CSS**: Utility-first CSS framework
- **Material-UI v4**: Component library for specific UI elements
- **EmailJS**: Email service for contact form
- **react-icons**: Icon library (FontAwesome, Material Design, etc.)
- **validator**: Email validation
- **lottie-react**: Animated illustrations

## Deployment Considerations

- Portfolio is static-exportable and can be deployed to Netlify, Vercel, GitHub Pages, Firebase, or Heroku
- Blog posts are fetched at build time from dev.to API (configured in `src/pages/index.js:29`)
- Change the username in the API URL to fetch your own dev.to articles
- Environment variables must be configured in your deployment platform

## Common Customization Tasks

### Adding a New Project
Edit `src/data/projects-data.js` and add an object to the array with required fields: `id`, `projectName`, `projectDesc`, `tags`, `code`, `demo`, `image`

### Adding a Skill
1. Check available skills in the comments of `src/data/skills-data.js`
2. Add the exact skill name to the `skillsData` array
3. If the skill is not available, the corresponding SVG must exist in `src/assets/svg/skills/`

### Changing Theme Colors
Edit color values in `src/theme/theme.js` for both `theLightTheme` and `theDarkTheme` objects

### Updating Personal Information
- About section: `src/data/about-data.js`
- Landing/header: `src/data/header-data.js`
- Social links: `src/data/socials-data.js`
- Contact info: `src/data/contacts-data.js`
