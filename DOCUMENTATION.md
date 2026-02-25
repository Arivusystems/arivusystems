# Arivu Systems — Project Documentation

## 1. Project Overview

**Arivu Systems** is a static marketing website for **Arivu Systems**, a creative agency based in Bengaluru, India. The site presents the studio’s services (branding, UI/UX, digital marketing, web development), company info, Vtiger solutions, and contact details.

The project is a **client-side only** site: plain HTML, CSS, and JavaScript. There is no build step (no Node/npm). Styling is done via precompiled CSS and optional SCSS sources. The site is suitable for hosting on any static host (e.g. GitHub Pages, Netlify, or a simple web server).

---

## 2. Tech Stack

| Layer        | Technology |
|-------------|------------|
| **Markup**  | HTML5      |
| **Styles**  | CSS3, SCSS (source in `assets/scss/`, output in `assets/css/`) |
| **Scripts** | JavaScript (ES5-style), jQuery 3.6.x |
| **Animation** | GSAP (GreenSock), ScrollTrigger, ScrollSmoother |
| **UI/Plugins** | Bootstrap (via `plugins.css`), Swiper, Parallax, Magnific Popup, etc. |
| **Fonts**   | Google Fonts (Poppins, Sora, Playfair Display, Epilogue) |

---

## 3. Repository Structure

```
ArivuSystems/
├── index.html          # Home
├── about.html          # About Us
├── services.html       # Services
├── solutions.html      # Vtiger Solutions
├── contact.html        # Contact
├── local.html          # Local / alternate version (e.g. dev)
├── index.css           # Page-specific overrides (used by all pages)
├── style.css           # Root-level style (if used)
├── CNAME               # Custom domain for GitHub Pages (e.g. arivusystems.com)
├── README.md
├── DOCUMENTATION.md    # This file
├── LICENSE             # MIT
│
├── assets/
│   ├── css/            # Compiled/global styles
│   │   ├── style.css   # Main theme (from SCSS)
│   │   ├── plugins.css # Third-party (Bootstrap, icons, etc.)
│   │   ├── base.css
│   │   └── layout/     # Layout-specific CSS
│   │
│   ├── scss/           # SCSS source (optional to recompile)
│   │   ├── style.scss  # Main entry
│   │   ├── utility/    # Variables, mixins, responsive
│   │   ├── components/ # Buttons, cursor, preloader, etc.
│   │   └── layout/    # Header, footer, hero, services, etc.
│   │
│   ├── js/
│   │   ├── scripts.js       # Main app logic, nav, animations, forms
│   │   ├── smoother-script.js # GSAP ScrollSmoother setup
│   │   ├── hscroll.js       # Horizontal scroll / marquee
│   │   ├── metro-scroll.js  # Metro-style layout
│   │   ├── map.js           # Map (e.g. contact)
│   │   ├── jquery-3.6.0.min.js
│   │   ├── jquery-migrate-3.4.0.min.js
│   │   ├── gsap.min.js
│   │   ├── ScrollTrigger.min.js
│   │   ├── ScrollSmoother.min.js
│   │   ├── parallax.min.js
│   │   ├── plugins.js       # Bundled plugins (Swiper, etc.)
│   │   └── imgReveal/       # Image reveal effects
│   │
│   └── imgs/            # Images and assets
│       ├── favicon_io/   # Favicons and manifest
│       ├── logo/         # Logos
│       ├── illustrations/ # Hero/illustrations
│       ├── serv-icons/   # Service icons
│       ├── patterns/     # Background patterns
│       ├── social/       # Social icons
│       └── ...
```

---

## 4. Pages and Features

| Page           | Purpose |
|----------------|--------|
| **index.html** | Home: hero, “About Studio” intro, services marquee, service cards, call-to-action, footer |
| **about.html** | About Us: studio story, team/values |
| **services.html** | Services: detailed service offerings |
| **solutions.html** | Vtiger Solutions |
| **contact.html** | Contact: form (optional backend), map, contact info |
| **local.html** | Local/alternate variant (e.g. different paths or content) |

**Common behavior across pages:**

- SVG-based preloader (“Loading” text + path animation)
- Custom cursor
- Progress ring (scroll-to-top)
- Smooth scrolling (GSAP ScrollSmoother on desktop)
- Responsive navbar with collapse
- Shared header/footer and nav links

---

## 5. How to Run the Project

The site is static: no install or build is required to view it. You only need to serve the project root over HTTP (or open files locally, with the caveats below).

### Option A: Dev server with live reload (recommended for development)

Changes to HTML, CSS, and JS **auto-refresh** in the browser. From the project root:

```bash
cd /path/to/arivu-systems
npm install
npm run dev
```

This starts **live-server** on port 8000, opens the site in your browser, and reloads when you save any file. Use this while editing.

### Option B: Local HTTP server (no auto-refresh)

Serving over `http://` avoids CORS/`file://` issues. From the project root:

**Python 3:**

```bash
cd /path/to/arivu-systems
python3 -m http.server 8000
```

Then open: **http://localhost:8000**

**Python 2:**

```bash
python -m SimpleHTTPServer 8000
```

**PHP:**

```bash
php -S localhost:8000
```

**Node (if you have `npx`):**

```bash
npx serve .
# or
npx http-server -p 8000
```

Then open the URL shown in the terminal (e.g. http://localhost:8000).

### Option C: Open HTML files directly

You can open `index.html` (or any `.html`) directly in the browser (`file:///...`). Some features may not work correctly (e.g. strict CORS, paths, or scripts that expect a server). Prefer **Option A** or **B** for full behavior.

### Option D: Deploy to GitHub Pages

For a **detailed step-by-step guide** (creating repo, enabling Pages, custom domain (e.g. arivusystems.com), DNS, HTTPS, troubleshooting), see **[GITHUB_PAGES.md](./GITHUB_PAGES.md)**.

Summary:

1. Push the repo to GitHub.
2. **Settings → Pages** → Source: **Deploy from a branch**.
3. Choose branch (e.g. `main`) and folder **/ (root)**.
4. Save. The site will be at `https://<username>.github.io/<repo>/`.
5. Optional: use custom domain (e.g. arivusystems.com via CNAME file) — see **GITHUB_PAGES.md** for DNS and verification.

---

## 6. Optional: Rebuilding CSS from SCSS

The repo already contains compiled `assets/css/style.css`. If you change files in `assets/scss/`, you need to recompile.

1. Install Sass (one of):
   - **Node:** `npm install -g sass`
   - **Ruby:** `gem install sass` (or use Bundler)
   - Or use an editor/IDE with SCSS support.

2. From the project root:

```bash
sass assets/scss/style.scss assets/css/style.css
```

For watch mode during development:

```bash
sass --watch assets/scss/style.scss:assets/css/style.css
```

---

## 7. Contact Form (Backend)

The contact form in `contact.html` may be commented out. When enabled, `scripts.js` submits it via AJAX to **`contact.php`**. This repo does **not** include `contact.php`. To make the form work you need to:

- Add a `contact.php` (or another server-side script) that accepts POST and sends email or stores messages, or  
- Replace the form action with a third-party service (e.g. Formspree, Netlify Forms).

Until then, the form will 404 or do nothing when submitted.

---

## 8. Browser Support

- Modern desktop and mobile browsers (Chrome, Firefox, Safari, Edge).
- Depends on jQuery, GSAP, and modern CSS; older browsers (e.g. IE11) may need polyfills or fallbacks.

---

## 9. License

MIT License. See **LICENSE** in the repository.

---

## 10. Quick Reference — Run Locally

```bash
# 1. Clone or navigate to the project
cd /path/to/arivu-systems

# 2. Start a local server (choose one)
python3 -m http.server 8000
# or: npx serve .
# or: php -S localhost:8000

# 3. Open in browser
# http://localhost:8000   (or the URL printed by the server)
```

No `npm install` or build step is required for the default static site.
