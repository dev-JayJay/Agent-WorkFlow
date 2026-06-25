# Frontend Engineering & UI/UX Skill

## Purpose

Use this skill when designing, implementing, or reviewing frontend features.

This skill defines reusable frontend engineering and UI/UX principles for building clean, responsive, accessible, and product-aligned interfaces.

It should be combined with project-specific context from:

* `AGENT.md`
* `.agents/reference/`
* `.agents/memory/`
* `.agents/plans/`
* Existing design system or component library

---

# Core Principle

Frontend is not just about displaying data.

Frontend must deliver:

* Clear user flow
* Beautiful visual design
* Fast interactions
* Mobile responsiveness
* Accessibility
* Product-aligned experience
* Maintainable component architecture

Every frontend decision should support the product goal and user journey.

---

# UI/UX Philosophy

Always design with the user first.

Prioritize:

* Clarity over decoration
* Flow over isolated screens
* Consistency over random creativity
* Mobile-first responsiveness
* Accessibility by default
* Fast perceived performance
* Visual hierarchy
* Product personality

Avoid:

* Cluttered layouts
* Random colors
* Inconsistent spacing
* Weak contrast
* Desktop-only thinking
* Overly complex interactions
* Beautiful UI with poor usability

---

# Product-Aligned Design

Before designing UI, understand:

* What product is this?
* Who is the user?
* What action should the user take?
* What emotion should the UI communicate?
* What is the business goal of this screen?

Examples:

## Finance / Wallet Product

Design should feel:

* Trustworthy
* Secure
* Clear
* Professional

Avoid playful or noisy visuals.

## Education Product

Design should feel:

* Encouraging
* Focused
* Clean
* Progress-oriented

## Healthcare Product

Design should feel:

* Calm
* Clean
* Reassuring
* Professional

## Admin Dashboard

Design should feel:

* Structured
* Efficient
* Data-focused
* Scannable

## Social / Chat Product

Design should feel:

* Fast
* Friendly
* Conversational
* Lightweight

---

# Design Styles / Visual Directions

When creating UI, choose a design direction that matches the product.

Common frontend design directions include:

## Minimalist

Clean, simple, lots of whitespace.

Best for:

* SaaS
* Dashboards
* Productivity tools
* Professional apps

## Corporate / Enterprise

Structured, serious, reliable.

Best for:

* Admin systems
* HRMS
* Finance dashboards
* B2B SaaS

## Modern SaaS

Polished cards, gradients, clean icons, strong CTAs.

Best for:

* Landing pages
* SaaS products
* Edtech platforms
* Creator platforms

## Japanese-Inspired Minimalism

Calm, balanced, precise, whitespace-heavy, subtle colors.

Best for:

* Wellness
* Premium products
* Clean productivity tools
* Focused learning apps

Principles:

* Use whitespace generously
* Avoid visual noise
* Use subtle dividers
* Use calm color palettes
* Keep typography clean

## Neumorphism / Soft UI

Soft shadows and raised surfaces.

Use carefully.

Best for:

* Concept apps
* Experimental interfaces

Avoid for serious dashboards or accessibility-sensitive apps.

## Glassmorphism

Blurred panels, transparency, layered depth.

Best for:

* Hero sections
* Premium landing pages
* Creative apps

Avoid overusing it in data-heavy screens.

## Brutalist / Bold Editorial

Strong typography, sharp contrast, bold layout.

Best for:

* Creative brands
* Portfolios
* Campaign pages

Avoid for sensitive finance, health, or admin interfaces.

## Mobile App Style

Large touch targets, bottom navigation, simple flows.

Best for:

* Mobile-first web apps
* PWAs
* User dashboards
* Booking apps

---

# Mobile-First Design

Always design mobile first unless the project specifically says otherwise.

Mobile rules:

* Use responsive layouts from the beginning.
* Avoid horizontal scrolling.
* Use large enough touch targets.
* Keep primary actions visible.
* Prefer stacked layouts on small screens.
* Use bottom sheets/drawers where appropriate.
* Avoid dense tables on mobile.
* Convert tables into cards on small screens.
* Keep forms short and readable.
* Use sticky CTA buttons when helpful.

Minimum touch target:

```txt
44px × 44px
```

Common responsive breakpoints:

```txt
sm: mobile
md: tablet
lg: desktop
xl: large desktop
```

---

# Layout Principles

Every screen should have:

* Clear page title
* Clear primary action
* Strong visual hierarchy
* Logical grouping
* Consistent spacing
* Empty states
* Loading states
* Error states
* Success states

Preferred layout structure:

```txt
Page
  ↓
Header / Page Title
  ↓
Primary Action Area
  ↓
Main Content
  ↓
Supporting Content
  ↓
Feedback / Status
```

---

# Visual Hierarchy

Guide the user's eyes.

Use:

* Font size
* Font weight
* Spacing
* Color contrast
* Card grouping
* Icons
* Positioning

Important content should look important.

Secondary content should not compete with primary actions.

---

# Design Direction Selection

Before designing any screen, choose the correct visual direction based on the product.

Do not randomly apply an aesthetic.

The selected design style must match:

- Product category
- User trust needs
- User technical level
- Primary action flow
- Brand personality
- Amount of information on screen
- Mobile usage expectations

## Common Design Directions

### Japanese Minimalist

Use for calm, premium, focused products.

Best for:

- Wellness
- Healthcare
- Premium education
- Productivity
- Focus apps

Characteristics:

- Intentional whitespace
- Calm typography
- Nature-inspired balance
- Decluttered layouts
- Subtle hierarchy
- Elegant restraint

### Japanese Information-Dense

Use for content-heavy, trust-building commercial products.

Best for:

- Marketplaces
- News portals
- Product catalogs
- Link-heavy platforms
- Commerce dashboards

Characteristics:

- Dense information
- Many visible options
- Banners/cards/links
- Reassurance through visibility
- Prioritizes access over minimalism

Use carefully on mobile.

### Scandinavian / Nordic

Use for clean, calm, trustworthy products.

Best for:

- Healthcare
- Finance
- SaaS
- Lifestyle
- Productivity

Characteristics:

- Soft colors
- Natural light backgrounds
- Simple layouts
- Functional clarity
- Warm minimalism

### Japandi

Blend of Japanese minimalism and Scandinavian warmth.

Best for:

- Premium SaaS
- Healthcare
- Wellness
- Education
- Calm productivity tools

Characteristics:

- Warm whitespace
- Soft neutral colors
- Clean lines
- Human-centered calm

### Cyberpunk / Neo-Tokyo

Use for futuristic, high-energy products.

Best for:

- Gaming
- AI tools
- Developer tools
- Trading dashboards
- Crypto products
- Experimental brands

Characteristics:

- Dark background
- Neon accents
- Glowing UI
- High contrast
- Futuristic panels

Use carefully for serious finance or healthcare.

### Bento Grid

Use for structured landing pages and dashboards.

Best for:

- SaaS landing pages
- Feature showcases
- Product dashboards
- Education platforms
- Analytics summaries

Characteristics:

- Modular cards
- Asymmetrical grid
- Strong visual grouping
- Easy scanning
- Excellent for responsive design

### Minimalist UI

Use for serious, clear, task-focused products.

Best for:

- SaaS
- Banking
- Wallets
- Portfolios
- Admin panels

Characteristics:

- Large whitespace
- Few colors
- Thin borders
- Clear CTA
- No distractions

### Modern SaaS

Use for polished web products.

Best for:

- SprintTest-style platforms
- Creator tools
- Dashboards
- Landing pages
- Subscription products

Characteristics:

- Cards
- Clean typography
- Strong CTA
- Subtle gradients
- Nice icons
- Clear empty/loading states

### Glassmorphism

Use for premium hero sections or creative dashboards.

Best for:

- Landing pages
- AI products
- Creative portfolios
- Futuristic sections

Characteristics:

- Frosted glass panels
- Blur
- Transparency
- Layered backgrounds

Avoid heavy use in forms and dense dashboards.

### Neumorphism / Soft UI

Use sparingly.

Best for:

- Experimental concepts
- Simple widgets
- Soft dashboards

Avoid for accessibility-sensitive apps because contrast can be weak.

### Brutalism

Use for bold, rebellious, editorial brands.

Best for:

- Creative studios
- Experimental portfolios
- Campaign pages

Avoid for healthcare, finance, admin systems, and trust-heavy products.

---

# Product-to-Design Matching Guide

## Finance / Wallet / Payments

Recommended:

- Minimalist UI
- Corporate / Enterprise
- Scandinavian
- Bento Grid for dashboards

Avoid:

- Brutalism
- Heavy Cyberpunk
- Overused Glassmorphism

## Education / Exam / Learning

Recommended:

- Modern SaaS
- Bento Grid
- Japandi
- Minimalist UI

Avoid:

- Overly dense UI
- Dark cyberpunk unless brand requires it

## Healthcare / Dental / Clinic

Recommended:

- Scandinavian
- Japanese Minimalist
- Japandi
- Calm Corporate

Avoid:

- Cyberpunk
- Brutalism
- Dense commercial UI

## Marketplace / Commerce

Recommended:

- Bento Grid
- Modern SaaS
- Japanese Information-Dense when many categories/products exist

Avoid:

- Extreme minimalism if users need many choices

## Admin Dashboard

Recommended:

- Minimalist UI
- Corporate / Enterprise
- Bento Grid

Avoid:

- Excessive decoration
- Large hero-style marketing sections

## AI / Developer Tools

Recommended:

- Modern SaaS
- Cyberpunk / Neo-Tokyo
- Bento Grid
- Minimalist UI

Avoid:

- Overly playful design if trust is required

---

# shadcn/ui Preference

For React or Next.js projects, prefer `shadcn/ui` when available or appropriate.

Use shadcn/ui for:

- Button
- Card
- Dialog
- Sheet
- Drawer
- Tabs
- Accordion
- Form
- Input
- Select
- Dropdown Menu
- Table
- Badge
- Alert
- Toast/Sonner
- Skeleton
- Command
- Popover

Rules:

- Reuse existing shadcn components before creating custom ones.
- Customize with Tailwind tokens instead of inline random styles.
- Keep components accessible.
- Preserve keyboard navigation and focus states.
- Do not over-customize until the design system becomes inconsistent.
- Use `cn()` utility for class composition where available.

---

# Component Architecture

Prefer reusable components.

Suggested component structure:

```txt
components/
  ui/
    Button.tsx
    Input.tsx
    Modal.tsx
    Card.tsx
    Badge.tsx

  layout/
    AppShell.tsx
    Sidebar.tsx
    Header.tsx
    PageHeader.tsx

  features/
    wallet/
    auth/
    dashboard/
```

Rules:

* Keep components small.
* Keep business logic out of presentational components.
* Reuse existing UI components before creating new ones.
* Keep state close to where it is used.
* Extract reusable patterns only when repeated.

---

# Page Design Rules

Each page should answer:

```txt
Where am I?
What can I do here?
What should I do next?
What is the current status?
```

Good pages include:

* Title
* Description
* Primary CTA
* Content sections
* State feedback
* Navigation clarity

Avoid pages that feel like random components placed together.

---

# Forms

Forms should be clear and forgiving.

Rules:

* Group related fields.
* Show validation messages near fields.
* Mark required fields clearly.
* Disable submit during loading.
* Show success/error feedback.
* Preserve user input on error.
* Avoid long forms where possible.
* Use step forms for complex flows.

---

# Tables and Lists

For desktop:

* Use tables for dense structured data.
* Add search, filters, pagination where needed.
* Keep columns meaningful.

For mobile:

* Convert tables into cards.
* Show only the most important information first.
* Hide secondary metadata behind details/expand actions.

---

# Empty States

Every empty state should explain:

* What is missing?
* Why it matters?
* What should the user do next?

Example:

```txt
No transactions yet.
Your wallet activity will appear here after your first deposit.
[Make Deposit]
```

---

# Loading States

Use loading states that match the UI.

Prefer:

* Skeletons for pages/cards
* Button spinners for actions
* Progress indicators for uploads/imports
* Optimistic UI only when safe

Avoid blank screens.

---

# Error States

Error states should be helpful.

Good error messages:

* Explain what happened
* Avoid blaming the user
* Give next action

Example:

```txt
We could not load your wallet balance.
Please check your connection and try again.
[Retry]
```

---

# Accessibility

Frontend must be accessible by default.

Check:

* Semantic HTML
* Proper labels
* Keyboard navigation
* Focus states
* Color contrast
* ARIA only when necessary
* Buttons are buttons
* Links are links
* Modals trap focus
* Forms have accessible errors

Never remove focus outlines without replacing them.

---

# Performance

Frontend should feel fast.

Rules:

* Avoid unnecessary re-renders.
* Split large components.
* Lazy load heavy sections.
* Optimize images.
* Use pagination/infinite loading carefully.
* Avoid huge client-side bundles.
* Use server-side rendering where useful.
* Cache API data when appropriate.

---

# State Management

Choose the simplest state solution.

Use local state for local UI behavior.

Use server-state tools for API data, such as:

* React Query
* RTK Query
* SWR

Use global state only when truly shared across many screens.

Avoid putting everything in global state.

---

# Design Consistency

Use consistent:

* Spacing
* Radius
* Shadows
* Typography
* Button styles
* Card styles
* Icon style
* Color usage
* Form behavior

Do not create a new style for every screen.

---

# Color Rules

Use colors intentionally.

Common roles:

* Primary
* Secondary
* Accent
* Success
* Warning
* Danger
* Muted
* Background
* Surface
* Border

Avoid too many colors.

For serious products, prefer calm and trustworthy palettes.

---

# Typography Rules

Good typography improves quality immediately.

Rules:

* Use clear hierarchy.
* Avoid too many font sizes.
* Use readable line heights.
* Keep paragraphs scannable.
* Use font weight intentionally.

Typical scale:

```txt
Page title
Section title
Card title
Body text
Muted text
Caption
```

---

# Animation and Interaction

Use animation to clarify, not distract.

Good use cases:

* Modal entry
* Drawer opening
* Button feedback
* Loading transitions
* Step transitions

Avoid:

* Slow animations
* Excessive bouncing
* Motion that blocks usability
* Animation on every element

---

# Frontend Security

Never expose secrets in frontend code.

Check:

* No API keys unless public-safe
* No admin-only data rendered for normal users
* No trust in frontend permissions alone
* Sanitize dangerous HTML
* Avoid leaking tokens in URLs
* Store tokens safely according to project standards

---

# Review Checklist

Before finishing frontend work, verify:

* UI matches product idea
* Screen flow is clear
* Mobile layout works
* Tablet layout works
* Desktop layout works
* Loading states exist
* Empty states exist
* Error states exist
* Forms validate properly
* Accessibility is considered
* Components follow project conventions
* No unnecessary duplicated components
* No random design direction
* No broken spacing or visual hierarchy

---

# Definition of Done

Frontend work is complete only when:

* The UI is visually polished.
* The user flow is clear.
* The design matches the product personality.
* Mobile responsiveness is excellent.
* Empty/loading/error states are handled.
* Accessibility basics are satisfied.
* Components are reusable where appropriate.
* Existing design patterns are respected.
* Validation/build commands pass.
