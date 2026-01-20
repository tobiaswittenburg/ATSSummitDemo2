# Copilot Instructions for Vocabulary Trainer

## Project Overview
This is a responsive vocabulary trainer web application built with Astro, TypeScript, and Tailwind CSS. The application helps students learn English vocabulary through an interactive, mobile-friendly interface.

## Core Principles

### 1. Quality Standards

#### TypeScript & Type Safety
- **ALWAYS** use TypeScript for all `.ts` and `.astro` files
- **ALWAYS** define proper interfaces for component props using the `interface Props` pattern
- **ALWAYS** use Zod schemas for content validation in `src/content/config.ts`
- **NEVER** use `any` type - use proper types or `unknown` if type is truly unknown
- Leverage Astro's built-in TypeScript support and type checking
- Use `astro check` before building to ensure type safety

#### Code Quality
- Write clean, readable, and self-documenting code
- Follow the existing code style and patterns in the repository
- Use meaningful variable and function names
- Keep components small and focused on a single responsibility
- Extract reusable logic into separate components or utilities
- Add comments only when necessary to explain complex logic or business rules

#### Content Schema Validation
- When adding or modifying vocabulary entries, ensure they conform to the schema in `src/content/config.ts`
- Required fields: `word` (string), `translation` (string)
- Optional fields: `category` (enum: 'verbs', 'adjectives', 'nouns', 'adverbs'), `difficulty` (enum: 'beginner', 'intermediate', 'advanced')
- Markdown body should include `# Example` and `# Notes` sections

### 2. Mobile-First Responsive Design

#### Tailwind CSS Best Practices
- **ALWAYS** design mobile-first, then enhance for larger screens using responsive prefixes (`md:`, `lg:`, `xl:`)
- Use Tailwind's responsive grid system: `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`
- Ensure proper spacing and padding on mobile devices (minimum touch target size: 44x44px)
- Use responsive text sizes: `text-sm md:text-base lg:text-lg`
- Use responsive spacing: `px-4 md:px-6 lg:px-8`

#### Mobile Optimization
- Ensure all interactive elements are easily tappable on mobile (minimum 44x44px)
- Use `hover:` effects that don't interfere with touch interactions
- Test layout on various screen sizes (mobile: 320px+, tablet: 768px+, desktop: 1024px+)
- Use `viewport` meta tag (already configured in Layout.astro)
- Optimize images with proper alt text and responsive sizing

#### Accessibility
- Use semantic HTML elements (`header`, `main`, `footer`, `nav`, `article`)
- Ensure proper heading hierarchy (`h1`, `h2`, `h3`)
- Add `aria-labels` for interactive elements when needed
- Ensure sufficient color contrast (WCAG AA minimum: 4.5:1 for normal text)
- Make sure all functionality is keyboard accessible

### 3. Testability & Maintainability

#### Component Design
- Keep components pure and predictable
- Props should be clearly defined with TypeScript interfaces
- Components should be stateless when possible (Astro's default)
- Separate presentation from data fetching logic
- Use Astro's `getCollection()` for content queries at build time

#### File Organization
- Follow the established project structure:
  - `src/components/` - Reusable Astro components
  - `src/layouts/` - Page layouts
  - `src/pages/` - Route pages (file-based routing)
  - `src/content/` - Content collections and schemas
- Keep components modular and self-contained
- Extract complex logic into utility functions in a `src/utils/` directory if needed

#### Content Management
- All vocabulary content should be in `src/content/vocabulary/` as markdown files
- Use consistent frontmatter format across all vocabulary files
- Validate content schema changes with `astro check`

### 4. Astro-Specific Best Practices

#### Static Site Generation
- Leverage Astro's static site generation for optimal performance
- Use `getCollection()` to fetch content at build time
- Minimize client-side JavaScript - keep components static when possible
- Use `client:*` directives only when interactivity is truly needed

#### Component Patterns
- Use `.astro` files for static components
- Follow the Astro component structure: frontmatter (---), then template
- Access props with `Astro.props` in the frontmatter
- Use named exports for TypeScript interfaces

#### Performance
- Keep bundle size minimal - Astro ships zero JS by default
- Optimize images using Astro's image optimization features when needed
- Use Tailwind's production build to purge unused CSS
- Leverage browser caching through static asset hashing

### 5. Development Workflow

#### Commands
- `npm run dev` - Start development server (http://localhost:4321)
- `npm run build` - Build for production (includes type checking with `astro check`)
- `npm run preview` - Preview production build locally
- `npm run astro` - Run Astro CLI commands

#### Before Committing
- Run `npm run build` to ensure no TypeScript errors
- Test responsive layout on mobile and desktop viewports
- Verify all vocabulary content loads correctly
- Check that new components follow existing patterns

## Common Patterns

### Adding a New Component
```astro
---
interface Props {
  title: string;
  description?: string;
}

const { title, description } = Astro.props;
---

<div class="component-container">
  <h2 class="text-xl md:text-2xl font-semibold">{title}</h2>
  {description && <p class="text-sm md:text-base">{description}</p>}
</div>
```

### Adding New Vocabulary
```markdown
---
word: "example"
translation: "Beispiel"
category: "nouns"
difficulty: "beginner"
---

# Example
This is an example sentence using the word.

# Notes
Additional context or usage tips.
```

### Responsive Grid Layout
```astro
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
  <!-- Card items -->
</div>
```

## What to Avoid
- ❌ Avoid using `any` type in TypeScript
- ❌ Don't add client-side JavaScript unless absolutely necessary
- ❌ Don't break the mobile-first responsive design
- ❌ Don't modify the content schema without careful consideration
- ❌ Don't add external dependencies without justification
- ❌ Don't use inline styles - use Tailwind classes
- ❌ Don't create components that are too large or do too many things

## Educational Context
This application is designed for students learning English vocabulary. Keep the user experience simple, intuitive, and focused on learning. Features should enhance the learning experience without adding unnecessary complexity.
