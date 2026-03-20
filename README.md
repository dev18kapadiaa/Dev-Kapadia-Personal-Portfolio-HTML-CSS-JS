# Dev Kapadia's Personal Portfolio Website using HTML, CSS, Javascript and PHP

This project is a **responsive single-page personal portfolio website** built primarily with **HTML + CSS + JavaScript**, with a small **PHP** backend script (`data.php`) used for saving contact form submissions into a MySQL database (local setup).

It contains sections for **Home**, **About**, **Skills**, **Accomplishments (Portfolio)**, **Extras**, and **Contact**, along with interactive UI features like a **preloader**, **portfolio filtering**, a **lightbox gallery**, a **mobile sidebar toggle**, and a **style/theme switcher**.

---

## Live / Run Locally

### Option A — Run as a static site (no PHP backend)
1. Download or clone the repository.
2. Open `index.html` in your browser.

> In this mode, the UI works (navigation, portfolio, themes, etc.), but the contact form backend (PHP + database) will not save submissions.

### Option B — Run with PHP + MySQL backend (for the contact form)
You need a local server stack (XAMPP/WAMP/MAMP or similar) and MySQL.

1. Put the project folder inside your server root:
   - Example (XAMPP): `htdocs/DK/`
2. Create a MySQL database named: `details`
3. Create a table named: `register`
4. Update credentials in `data.php` if needed (defaults are `root` and empty password).
5. Open in browser through localhost:
   - `http://localhost/DK/`

---

## Project Structure (high-level)

Key files (from repository root):
- `index.html` — Main single-page portfolio website
- `script.js` — Main interactions (preloader, nav, portfolio filter, lightbox, sidebar toggler)
- `styleSwitcher.js` — Theme color switching + dark/light mode
- `style.css` + `css/style.css` — Base styling (layout + responsiveness)
- `pink.css`, `blue.css`, `orange.css`, `yellow.css`, `green.css` — Alternate color themes (skins)
- `styleSwitcher.css` — UI styles for the style switcher component
- `data.php` — Backend handler for contact form submissions (MySQL insert)
- `DevResume.pdf` — Resume/CV document
- Various images (`.png`, `.jpg`) — used in portfolio cards, profile, extras/blog section, etc.

---

## Main Website Sections

### 1) Home (`#home`)
- Profile image + name + short tagline.
- Social links (Twitter, Instagram, Snapchat, LinkedIn).

### 2) About (`#about`)
- About text + personal information (birthday, city, email, etc.).
- Skill bars (C, C++, Web Dev, Python).
- Buttons:
  - **Open CV** opens `DevResume.pdf`
  - **Hire Me** jumps directly to the Contact section

### 3) Skills (`#services`)
- A list of skills/services with icons and external links (Coursera, Wikipedia, etc.).

### 4) Accomplishments (`#portfolio`)
- A portfolio grid of items (images + titles).
- Includes filtering and a lightbox preview experience (details below).

### 5) Extras (`#blog`)
- “Blog-style” cards with images and short messages/quotes.
- Each card has tags linking to external resources.

### 6) Contact (`#contact`)
- Contact info (phone, location, email).
- A contact form that can post to the PHP backend.

---

## Functionality & Features (in detail)

## 1) Preloader animation (on page load)
**Goal:** Show a loading screen until the page is ready.

How it works:
- `index.html` contains a `.preloader` element.
- On `window.load`, JavaScript:
  1. Adds `opacity-0` to fade out the preloader
  2. After ~1 second, sets `display: none` to remove it visually

**Implemented in:** `script.js`

---

## 2) Single-page navigation (SPA-like section switching)
**Goal:** Navigate between sections without reloading the page.

How it works:
- Sidebar navigation links use hashes like `#home`, `#about`, etc.
- JavaScript listens for nav link clicks and:
  - Removes `active` class from all sections
  - Adds `active` class to the targeted section
  - Updates the active state in the sidebar navigation
  - Adds a `back-section` class to the previous section for smoother transitions

**Implemented in:** `script.js`  
Key functions:
- `showSection(element)`
- `updateNav(element)`
- `addBackSectionClass(num)`
- `removeBackSectionClass()`

---

## 3) Responsive sidebar + hamburger toggler (mobile support)
**Goal:** Make the sidebar collapsible on smaller screens.

How it works:
- Clicking `.nav-toggler` toggles `open` on:
  - `.aside`
  - `.nav-toggler`
  - each `.section`

This allows the layout to adapt for mobile/tablet widths.

**Implemented in:** `script.js` (`asideSectionTogglerBtn()`)

---

## 4) Portfolio filtering (Accomplishments section)
**Goal:** Filter portfolio items by category.

HTML structure:
- Filter buttons have `data-filter` values:
  - `all`, `web-design`, `project`, `courses`, `workshops`
- Each portfolio card has:
  - `class="portfolio-item"`
  - `data-category="..."`

How it works:
- When a filter button is clicked:
  - the previously active filter button loses `.active`
  - clicked button gets `.active`
  - matching items get `.show` and remove `.hide`
  - non-matching items get `.hide` and remove `.show`
  - if filter is `all`, everything is shown

**Implemented in:** `script.js` (portfolio item filter block)

---

## 5) Portfolio lightbox (image preview overlay)
**Goal:** Show a larger preview of a portfolio item when clicked, with navigation.

How it works:
- Clicking any `.portfolio-item`:
  - sets an `itemIndex`
  - opens the `.lightbox` overlay (toggles `open`)
  - updates:
    - image source (`.lightbox-img`)
    - caption text (`.caption-text`) from item’s `<h4>`
    - counter (`.caption-counter`) like `3 of 12`

Controls:
- Clicking the close button (`.lightbox-close`) closes the lightbox
- Clicking the overlay background also closes it
- There are next/prev controls:
  - `nextItem()`
  - `prevItem()`

**Implemented in:** `script.js`  
Key functions:
- `toggleLightbox()`
- `changeItem()`
- `nextItem()`
- `prevItem()`

---

## 6) “Hire Me” quick navigation
**Goal:** A shortcut button to the Contact section.

How it works:
- The “Hire Me” button is an anchor with:
  - `href="#contact"`
  - `data-section-index="1"` (used for back-section transitions)
- JavaScript handles click to:
  - switch to the contact section
  - update nav state
  - manage animation transition classes

**Implemented in:** `script.js`

---

## 7) Theme color switcher (alternate style skins)
**Goal:** Allow changing the primary theme color.

How it works:
- `index.html` includes multiple `<link>` tags with:
  - `class="alternate-style"`
  - a `title` like `pink`, `blue`, etc.
  - and `disabled` attribute by default
- `setActiveStyle(color)`:
  - enables the matching stylesheet by removing `disabled`
  - disables all others by setting `disabled="true"`

Theme files:
- `pink.css`, `blue.css`, `orange.css`, `yellow.css`, `green.css`

**Implemented in:** `styleSwitcher.js`

---

## 8) Dark / Light mode
**Goal:** Toggle the entire UI between dark and light modes.

How it works:
- Two radio inputs with class `.body-skin`:
  - `value="light"`
  - `value="dark"`
- When changed:
  - dark mode sets `document.body.className = "dark"`
  - light mode clears the class

**Implemented in:** `styleSwitcher.js`

---

## 9) Style switcher panel open/close
**Goal:** A UI panel to choose themes and interface mode.

How it works:
- Clicking `.toggle-style-switcher` toggles `.open` on `.style-switcher`

**Implemented in:** `styleSwitcher.js`

---

# Backend (PHP): Contact form submission

## data.php — What it does
`data.php` reads POST form fields:
- `username`
- `email`
- `topic`
- `message`

Then it connects to MySQL:
- host: `localhost`
- user: `root`
- password: *(empty)*
- database: `details`

And inserts into table `register`:
- columns: `username`, `email`, `topic`, `message`

On success it prints:
> "Hola !!! Your Details Have Been Successfully Saved At Backend....."

**File:** `data.php`

## Important note about the form action
In `index.html`, the contact form action points to:
`http://localhost/data.php`

If your project is inside a folder like `http://localhost/DK/`, you may want to update it to:
- `action="data.php"`
or
- `action="http://localhost/DK/data.php"`

So the form actually reaches the correct script.

---

## Tech Stack
- **HTML** — content and structure
- **CSS** — styling + responsive layout + theme skins
- **JavaScript** — UI interactions and dynamic behavior
- **PHP + MySQL** — (optional) contact form data storage

---
