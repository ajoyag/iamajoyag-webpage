# Cybersecurity Portfolio

This repository contains the code for a modern and interactive Cybersecurity Portfolio website. Designed with a dark/light mode toggle, dynamic background patterns, and a terminal-style preloader, it aims to provide a sleek and engaging experience for showcasing cybersecurity skills, projects, and certifications.

---

### Table of Contents
* Features
* Technologies Used
* Working Principle
    * HTML Structure
    * CSS Styling
    * JavaScript Functionality
* Future Enhancements
* License

---

### Features

* **Responsive Design:** Optimized for various screen sizes, from mobile to desktop.
* **Dark/Light Mode Toggle:** Seamlessly switch between dark and light themes.
* **Dynamic Terminal Preloader:** An engaging loading screen with a progress bar and a unique "dissolve" animation as it disappears.
* **Animated Background Patterns:** Subtle, moving neon-inspired patterns in the background for a futuristic and dynamic feel.
* **Typing Animation:** A dynamic typing effect in the hero section for a personalized touch, cycling through different professional roles.
* **Interactive Sections:** Dedicated, clearly defined sections for About Me, Skills & Tools, Certifications, Projects/Case Studies, Blog, and Contact.
* **Project Modals:** Detailed pop-up modals for showcasing individual projects with images, descriptions, and direct GitHub links.
* **Smooth Scrolling:** Enhanced navigation with smooth scroll effects when clicking on internal links.
* **Hideable Navigation:** The navigation bar intelligently hides on scroll down and reappears on scroll up, optimizing screen real estate for content.
* **Back to Top Button:** A convenient, floating button that appears as you scroll down, allowing for quick return to the top of the page.
* **Aesthetic Font Styling:** Utilizes a combination of Google Fonts (Source Code Pro, Space Mono, Orbitron) for a distinct, tech-inspired, and visually appealing look.

---

### Technologies Used

* **HTML5:** For structuring the web content.
* **CSS3:** For styling and visual presentation, including animations, transitions, and responsive design.
* **JavaScript (ES6+):** For interactive elements, dynamic content loading, client-side logic, and all custom effects.
* **Google Fonts:**
    * **Source Code Pro:** Main body font, a classic monospace choice.
    * **Space Mono:** Used for general monospace elements, offering a clean, modern code-like aesthetic.
    * **Orbitron:** Applied specifically to the "Ajoyag" name for a futuristic and digital aesthetic.
* **Font Awesome:** For various icons used throughout the website (e.g., theme toggle, social media links).

---

### Working Principle

#### HTML Structure

The website is built as a single-page application (SPA), logically segmented into semantic section elements. Each section is assigned a unique id to facilitate smooth internal navigation.

* `<head>`: Contains essential metadata, the site's favicon, and links to external resources like Google Fonts and the Font Awesome CDN.
* `<div class="bg-effect">`: A full-viewport div responsible for rendering the animated background patterns, positioned behind all main content.
* `<div id="preloader">`: The initial loading screen, designed in a terminal style, which is displayed until the content is ready.
* `<header class="nav">`: The fixed navigation bar, featuring the site logo, navigation links, and a theme toggle button.
* `<section class="hero">`: The primary introductory section, showcasing the main title, the portfolio owner's name, a dynamic typing animation, and prominent call-to-action buttons.
* `<div class="section-gap">`: Small, transparent div elements strategically placed to provide visual spacing and separation between major content sections.
* **Content Sections** (`<section id="about">`, `<section id="skills">`, etc.): These are the core content areas, each dedicated to presenting specific information about the portfolio owner.
* `<footer>`: Located at the bottom of the page, containing copyright information.
* `<div id="projectModal">`: A hidden modal structure that is dynamically activated and populated when a user clicks on a project card.

#### CSS Styling

The CSS is meticulously crafted to achieve a clean, modern, and cybersecurity-themed aesthetic, with full responsiveness and robust dark/light mode support.

* **CSS Variables:** Extensive use of root-level CSS variables (`:root`) defines a comprehensive set of design tokens (colors, shadows, borders). This architecture enables effortless theme switching by simply toggling the `dark-mode` class on the `<body>` element.
* **Dark/Light Mode Implementation:** The `body.dark-mode` selector specifically overrides the default CSS variables, providing a distinct and visually appealing dark theme.
* **Global Background Effect** (`.bg-effect`):
    * Utilizes `position: fixed; inset: 0; z-index: -2;` to ensure it covers the entire viewport and remains in the background.
    * The `animation: moveMatrix 60s linear infinite;` creates a subtle, continuous vertical scrolling effect for the background patterns.
    * Multiple `bg-pattern-X` classes define various neon-colored patterns using `radial-gradient` and `linear-gradient` with low `rgba` opacity. This allows the primary background color to subtly show through, creating a vibrant, glowing effect.
* **Terminal Preloader** (`#preloader`):
    * Its initial state is `opacity: 1; transform: scale(1); filter: blur(0px);`.
    * The `dissolve-out` class (dynamically added by JavaScript) triggers a transition to `opacity: 0; transform: scale(0.5); filter: blur(20px);`, resulting in a smooth, shrinking, blurring, and fading "dissolve" animation.
* **Navigation** (`.nav`): Employs `position: fixed; backdrop-filter: blur(10px);` to create a modern frosted glass effect. It also incorporates `transform: translateY()` for the smooth hide/show animation based on scroll direction.
* **Hero Section Title** (`.glow-title`): Features `animation: pulsateGlow 3s ease-in-out infinite;` which applies a dynamic, pulsating neon glow, enhancing its visual impact.
* **Name Styling** (`.name` - "Ajoyag"):
    * `font-family: 'Orbitron', sans-serif;` applies the distinctive futuristic typeface.
    * `color: black;` sets the text color to black.
    * `text-shadow: 0 0 5px var(--accent-color), 0 0 10px var(--accent-color), 0 0 15px var(--accent-color);` creates a prominent external glow effect. The glow color dynamically changes based on the `--accent-color` variable (blue in light mode, neon green in dark mode).
    * `body.dark-mode .name` further enhances the glow intensity for optimal visibility and aesthetic appeal in dark mode.
* **Interactive Elements:** All interactive components such as buttons, skill bars, tools, certifications, and project cards are styled with `transition` properties for fluid hover and active states, often including `transform: translateY()` for subtle lift animations and `box-shadow` changes.
* **Responsive Media Queries:** `@media (max-width: 768px)` is extensively used to adjust layout, navigation behavior, and element sizing, ensuring an optimal user experience on smaller screens.

#### JavaScript Functionality

The JavaScript code orchestrates all the dynamic and interactive behaviors of the website.

* **Theme Toggle:**
    * An event listener on `#themeToggle` detects user clicks.
    * The `applyTheme(theme)` function dynamically adds or removes the `dark-mode` class from the `<body>` element and updates the theme toggle icon (sun/moon).
    * `localStorage` is utilized to persist the user's selected theme preference across Browse sessions.
* **Terminal Preloader:**
    * Manages the visual progression of the `loadingBar` and updates the `loadingPercent` text.
    * `currentProgressInterval` and `currentAccessGrantedDelay` are dynamically adjusted based on `window.location.hash`. This provides a "faster re-load" experience if the user navigates directly to a specific section (e.g., `#about`) or a "normal first-load" experience otherwise.
    * Upon reaching 100% progress, it displays "Access Granted", then triggers the `dissolve-out` class on the `#preloader` to initiate the dissolve animation.
    * Finally, after the CSS transition completes, `preloader.style.display = "none";` hides the preloader, and `document.body.style.overflow = "auto";` re-enables page scrolling.
* **Dynamic Background Pattern:**
    * An array `allPatterns` stores the CSS classes for various background patterns.
    * The `shuffleArray` utility ensures a random order of pattern selection.
    * The `getNextPattern()` function selects a random pattern, moves it from the `availablePatterns` pool to `usedPatterns`, and replenishes `availablePatterns` if all patterns have been used.
    * The chosen pattern class is then applied to the `#bgEffect` div.
* **Typing Animation:**
    * The `typingText` array holds the phrases to be animated.
    * The `type()` function iteratively appends characters to the `#typingText` element, simulating real-time typing, complete with a blinking cursor.
    * Includes carefully timed delays for typing speed and a brief pause after each word is fully typed before transitioning to the next phrase.
* **Data Loading and Rendering:**
    * `skillsData`, `toolsData`, `certificationsData`, and `projectsData` are JavaScript arrays containing the content for their respective sections.
    * The script dynamically generates and appends appropriate HTML elements (e.g., list items, spans, divs) to populate these sections, ensuring content is rendered efficiently.
* **Project Modal Interaction:**
    * `showProject(project)`: Populates the modal with specific data from the clicked project object and applies the `active` class to make it visible.
    * `hideProject()`: Removes the `active` class to conceal the modal.
    * Event listeners are implemented for the Escape key and clicks outside the modal content to facilitate easy closing.
* **Navigation and Scroll Logic:**
    * `toggleMenu()`: Toggles the `active` class on `#navLinks` to control the visibility of the mobile navigation menu.
    * A scroll event listener on the window dynamically hides or shows the fixed navbar based on the user's scroll direction, and automatically collapses the mobile menu if it's open during scrolling.
    * The `backToTop` button's visibility is controlled based on the scroll position, and it provides a smooth scroll-to-top functionality when clicked.
    * All internal anchor links (`a[href^="#"]`) are configured for smooth scrolling behavior.
* **Touch Event Handling:** Basic `touchstart` and `touchend` listeners are included on elements with the `.hover-only-on-hover` class. This helps manage hover states more effectively on touch devices, mitigating issues like "ghost clicks" or persistent hover styles.

---

### Future Enhancements

* **Backend Integration:** Implement a simple backend solution (e.g., Node.js with Express, Firebase Functions) to enable the contact form to send emails or store messages, moving beyond client-side alerts.
* **Dynamic Blog Content:** Transition from hardcoded blog posts to fetching them dynamically from a headless CMS, a simple JSON file, or a markdown parser.
* **Advanced Project Filtering/Sorting:** Introduce interactive options to filter or sort projects by categories, technologies used, or other criteria.
* **Enhanced Animations:** Explore adding more subtle and performance-optimized animations on scroll or element visibility using the Intersection Observer API for a more polished feel.
* **Comprehensive Accessibility:** Further enhance ARIA attributes, improve keyboard navigation, and ensure optimal color contrast ratios across all elements for better accessibility.
* **Automated Testing:** Implement unit tests and end-to-end tests for critical functionalities to ensure code reliability and prevent regressions.

---

### License

View the LICENCE file to learn more.
