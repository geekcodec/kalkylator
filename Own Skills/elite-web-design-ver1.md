---
name: elite-web-design
description: Creates premium, agency-grade web designs and applications with exceptional quality, modern aesthetics, mobile-first responsive design, and sophisticated user experiences. Use when building websites, web apps, or interfaces that require the highest level of design excellence, polish, and technical sophistication.
---

# Elite Web Design

This skill guides the creation of world-class web experiences that rival the work of top-tier design agencies. Every element should feel intentional, polished, and sophisticated.

## When to use this skill

- Building landing pages, websites, or web applications that require premium quality
- Creating user interfaces that need to stand out from typical AI-generated designs
- Developing mobile-responsive designs that work flawlessly across all devices
- When the user requests "high-end," "professional," "agency-quality," or "premium" web design
- Building marketing sites, SaaS applications, portfolios, or any web presence requiring visual excellence

## Core Principles

### 1. Design Philosophy
- **Intentional minimalism**: Every element serves a purpose. Remove anything that doesn't add value.
- **Sophisticated restraint**: Use white space generously. Resist the urge to fill every pixel.
- **Premium aesthetics**: Favor refined typography, subtle animations, and carefully chosen color palettes over flashy effects.
- **Content hierarchy**: Guide the user's eye naturally through the page with clear visual hierarchy.
- **Brand coherence**: Maintain consistent design language throughout the entire experience.

### 2. Typography Excellence
```css
/* Premium Typography System */
--font-display: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
--font-body: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;

/* Type Scale - Use mathematical ratios */
--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */
--text-4xl: 2.25rem;   /* 36px */
--text-5xl: 3rem;      /* 48px */
--text-6xl: 3.75rem;   /* 60px */
--text-7xl: 4.5rem;    /* 72px */

/* Line Heights */
--leading-tight: 1.25;
--leading-normal: 1.5;
--leading-relaxed: 1.75;

/* Font Weights */
--font-light: 300;
--font-normal: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;
```

**Typography Rules**:
- Use a maximum of 2-3 font families per project
- Prefer modern system fonts or premium web fonts (Inter, Helvetica Neue, SF Pro)
- Maintain consistent line-height ratios (1.5 for body, 1.2-1.3 for headings)
- Use proper font weights: 300-400 for body, 600-700 for emphasis
- Implement responsive typography that scales smoothly across breakpoints
- Pay attention to kerning and letter-spacing on large headings

### 3. Color System Architecture
```css
/* Premium Color Palette Structure */
--color-primary-50: #...;   /* Lightest tint */
--color-primary-100: #...;
--color-primary-200: #...;
--color-primary-300: #...;
--color-primary-400: #...;
--color-primary-500: #...;  /* Base color */
--color-primary-600: #...;
--color-primary-700: #...;
--color-primary-800: #...;
--color-primary-900: #...;  /* Darkest shade */

/* Neutral Palette */
--color-gray-50: #FAFAFA;
--color-gray-100: #F5F5F5;
--color-gray-200: #E5E5E5;
--color-gray-300: #D4D4D4;
--color-gray-400: #A3A3A3;
--color-gray-500: #737373;
--color-gray-600: #525252;
--color-gray-700: #404040;
--color-gray-800: #262626;
--color-gray-900: #171717;

/* Semantic Colors */
--color-success: #10B981;
--color-warning: #F59E0B;
--color-error: #EF4444;
--color-info: #3B82F6;

/* Surface Colors */
--color-background: #FFFFFF;
--color-surface: #FAFAFA;
--color-border: #E5E5E5;
```

**Color Rules**:
- Use a 50-900 scale for primary and neutral colors
- Limit primary colors to 1-2 per project
- Use neutral grays for 80% of the interface
- Ensure WCAG AAA contrast ratios (7:1 for text, 4.5:1 minimum)
- Implement dark mode with inverted color scales
- Use color purposefully to guide attention and hierarchy

### 4. Spacing & Layout System
```css
/* 8-Point Grid System */
--spacing-1: 0.25rem;  /* 4px */
--spacing-2: 0.5rem;   /* 8px */
--spacing-3: 0.75rem;  /* 12px */
--spacing-4: 1rem;     /* 16px */
--spacing-5: 1.25rem;  /* 20px */
--spacing-6: 1.5rem;   /* 24px */
--spacing-8: 2rem;     /* 32px */
--spacing-10: 2.5rem;  /* 40px */
--spacing-12: 3rem;    /* 48px */
--spacing-16: 4rem;    /* 64px */
--spacing-20: 5rem;    /* 80px */
--spacing-24: 6rem;    /* 96px */
--spacing-32: 8rem;    /* 128px */

/* Container Widths */
--container-sm: 640px;
--container-md: 768px;
--container-lg: 1024px;
--container-xl: 1280px;
--container-2xl: 1536px;

/* Responsive Breakpoints */
--screen-sm: 640px;
--screen-md: 768px;
--screen-lg: 1024px;
--screen-xl: 1280px;
--screen-2xl: 1536px;
```

**Layout Principles**:
- Use consistent spacing multiples (4px, 8px, 16px, 24px, 32px, 48px, 64px)
- Employ generous white space—more than feels comfortable
- Create clear visual groupings with space
- Use max-widths to prevent content from becoming unwieldy on large screens
- Implement responsive padding and margins that scale with viewport

### 5. Mobile-First Responsive Design

**Mobile-First Approach**:
```css
/* Start with mobile styles */
.component {
  /* Mobile styles (default) */
}

/* Then add larger breakpoints */
@media (min-width: 768px) {
  .component {
    /* Tablet styles */
  }
}

@media (min-width: 1024px) {
  .component {
    /* Desktop styles */
  }
}
```

**Responsive Rules**:
- Design for 375px width first (iPhone SE minimum)
- Test at: 375px, 768px, 1024px, 1440px, 1920px
- Use fluid typography with clamp(): `font-size: clamp(1rem, 2vw, 1.5rem);`
- Implement responsive images with srcset and proper aspect ratios
- Use CSS Grid and Flexbox for flexible layouts
- Ensure touch targets are minimum 44px × 44px
- Stack elements vertically on mobile, horizontally on desktop
- Hide/show elements strategically based on viewport

### 6. Modern Component Architecture

**Button Design**:
```jsx
// Premium Button Component
<button className="
  px-8 py-4
  bg-gradient-to-r from-blue-600 to-indigo-600
  text-white font-semibold text-base
  rounded-xl
  shadow-lg shadow-blue-500/30
  hover:shadow-xl hover:shadow-blue-500/40
  hover:-translate-y-0.5
  active:translate-y-0
  transition-all duration-200
  focus:outline-none focus:ring-4 focus:ring-blue-500/50
  disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:translate-y-0
">
  Get Started
</button>
```

**Card Design**:
```jsx
<div className="
  bg-white
  rounded-2xl
  p-8
  shadow-sm
  border border-gray-100
  hover:shadow-xl hover:border-gray-200
  transition-all duration-300
  hover:-translate-y-1
">
  {/* Card content */}
</div>
```

**Input Design**:
```jsx
<input className="
  w-full
  px-4 py-3
  bg-gray-50
  border-2 border-gray-200
  rounded-xl
  text-gray-900
  placeholder:text-gray-400
  focus:outline-none
  focus:bg-white
  focus:border-blue-500
  focus:ring-4 focus:ring-blue-500/10
  transition-all duration-200
" />
```

### 7. Animation & Micro-interactions

**Animation Principles**:
- Use subtle, purposeful animations
- Keep durations between 150-300ms for UI interactions
- Use easing functions: `ease-out` for entrances, `ease-in` for exits
- Implement hover states on all interactive elements
- Add loading states and skeleton screens
- Use transitions on color, transform, and shadow properties
- Respect `prefers-reduced-motion` for accessibility

**Premium Animation Examples**:
```css
/* Smooth Hover Effects */
.card {
  transition: all 300ms cubic-bezier(0.4, 0, 0.2, 1);
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

/* Fade-in Animation */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.element {
  animation: fadeIn 600ms ease-out;
}

/* Gradient Animation */
.gradient-bg {
  background: linear-gradient(270deg, #667eea, #764ba2, #f093fb);
  background-size: 400% 400%;
  animation: gradientShift 15s ease infinite;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}
```

### 8. Performance Optimization

**Critical Performance Metrics**:
- Largest Contentful Paint (LCP): < 2.5s
- First Input Delay (FID): < 100ms
- Cumulative Layout Shift (CLS): < 0.1
- Time to Interactive (TTI): < 3.8s

**Optimization Techniques**:
```jsx
// Lazy load images
<img 
  loading="lazy"
  srcSet="image-320w.jpg 320w, image-640w.jpg 640w, image-1280w.jpg 1280w"
  sizes="(max-width: 640px) 100vw, (max-width: 1024px) 50vw, 33vw"
  alt="Description"
/>

// Preload critical assets
<link rel="preload" href="/fonts/inter.woff2" as="font" type="font/woff2" crossOrigin />

// Code splitting
const HeavyComponent = lazy(() => import('./HeavyComponent'));
```

**Performance Rules**:
- Minimize bundle size (aim for < 200KB initial load)
- Use next-gen image formats (WebP, AVIF)
- Implement proper image compression and sizing
- Defer non-critical JavaScript
- Use CSS instead of JavaScript for animations when possible
- Minimize render-blocking resources
- Implement proper caching strategies

### 9. Accessibility Standards

**WCAG 2.1 AAA Compliance**:
```jsx
// Semantic HTML
<nav aria-label="Main navigation">
  <ul>
    <li><a href="#home">Home</a></li>
  </ul>
</nav>

// Proper heading hierarchy
<h1>Main Title</h1>
<h2>Section Title</h2>
<h3>Subsection Title</h3>

// Form labels and ARIA
<label htmlFor="email">Email Address</label>
<input 
  id="email"
  type="email"
  aria-required="true"
  aria-describedby="email-help"
/>
<span id="email-help">We'll never share your email</span>

// Focus indicators
.button:focus {
  outline: 3px solid var(--color-primary-500);
  outline-offset: 2px;
}

// Skip links
<a href="#main-content" className="sr-only focus:not-sr-only">
  Skip to main content
</a>
```

**Accessibility Checklist**:
- ✓ Keyboard navigation works for all interactive elements
- ✓ Focus indicators are visible and clear
- ✓ Color is not the only means of conveying information
- ✓ All images have descriptive alt text
- ✓ Form inputs have associated labels
- ✓ Headings follow proper hierarchy
- ✓ ARIA labels used appropriately
- ✓ Sufficient color contrast ratios
- ✓ Text can be resized to 200% without loss of functionality
- ✓ Content is readable and functional with CSS disabled

### 10. Premium Design Patterns

**Hero Section**:
```jsx
<section className="relative min-h-screen flex items-center justify-center overflow-hidden bg-gradient-to-br from-gray-900 via-blue-900 to-gray-900">
  {/* Animated background */}
  <div className="absolute inset-0 opacity-20">
    <div className="absolute inset-0 bg-[url('/grid.svg')] bg-center [mask-image:linear-gradient(180deg,white,rgba(255,255,255,0))]"></div>
  </div>
  
  {/* Content */}
  <div className="relative z-10 max-w-7xl mx-auto px-6 text-center">
    <h1 className="text-6xl md:text-7xl lg:text-8xl font-bold text-white mb-6 tracking-tight">
      Build Something
      <span className="block bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent">
        Extraordinary
      </span>
    </h1>
    <p className="text-xl md:text-2xl text-gray-300 mb-12 max-w-3xl mx-auto leading-relaxed">
      The most advanced platform for creating exceptional digital experiences.
    </p>
    <div className="flex flex-col sm:flex-row gap-4 justify-center">
      <button className="px-8 py-4 bg-white text-gray-900 rounded-xl font-semibold hover:bg-gray-100 transition-all shadow-xl">
        Get Started Free
      </button>
      <button className="px-8 py-4 bg-white/10 backdrop-blur-sm text-white rounded-xl font-semibold border border-white/20 hover:bg-white/20 transition-all">
        Watch Demo
      </button>
    </div>
  </div>
</section>
```

**Feature Grid**:
```jsx
<section className="py-24 bg-gray-50">
  <div className="max-w-7xl mx-auto px-6">
    <h2 className="text-5xl font-bold text-center mb-16">
      Everything you need to succeed
    </h2>
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      {features.map((feature, i) => (
        <div key={i} className="bg-white rounded-2xl p-8 shadow-sm hover:shadow-xl transition-all duration-300 group">
          <div className="w-12 h-12 bg-gradient-to-br from-blue-500 to-purple-600 rounded-xl mb-6 flex items-center justify-center group-hover:scale-110 transition-transform">
            {feature.icon}
          </div>
          <h3 className="text-2xl font-semibold mb-4">{feature.title}</h3>
          <p className="text-gray-600 leading-relaxed">{feature.description}</p>
        </div>
      ))}
    </div>
  </div>
</section>
```

**Testimonial Section**:
```jsx
<section className="py-24 bg-gradient-to-br from-blue-600 to-purple-700">
  <div className="max-w-7xl mx-auto px-6">
    <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
      {testimonials.map((testimonial, i) => (
        <div key={i} className="bg-white/10 backdrop-blur-lg rounded-2xl p-8 border border-white/20">
          <div className="flex items-center mb-6">
            <img 
              src={testimonial.avatar}
              alt={testimonial.name}
              className="w-12 h-12 rounded-full mr-4"
            />
            <div>
              <div className="font-semibold text-white">{testimonial.name}</div>
              <div className="text-blue-200 text-sm">{testimonial.role}</div>
            </div>
          </div>
          <p className="text-white/90 leading-relaxed italic">
            "{testimonial.quote}"
          </p>
        </div>
      ))}
    </div>
  </div>
</section>
```

### 11. Technical Implementation

**Recommended Tech Stack**:
- **Framework**: React with Next.js or Vite
- **Styling**: Tailwind CSS with custom configuration
- **Animations**: Framer Motion or CSS animations
- **Icons**: Lucide React or Heroicons
- **Fonts**: Inter, SF Pro, or custom brand fonts
- **State Management**: React Context or Zustand (lightweight)
- **Forms**: React Hook Form with Zod validation

**Project Structure**:
```
src/
├── components/
│   ├── ui/           # Reusable UI components
│   ├── sections/     # Page sections
│   └── layout/       # Layout components
├── styles/
│   ├── globals.css   # Global styles and CSS variables
│   └── animations.css
├── utils/            # Helper functions
└── pages/            # Page components
```

**CSS Custom Properties Setup**:
```css
:root {
  /* Colors */
  --color-primary: 59 130 246;
  --color-background: 255 255 255;
  --color-foreground: 23 23 23;
  
  /* Spacing */
  --spacing-unit: 0.25rem;
  
  /* Borders */
  --radius-sm: 0.5rem;
  --radius-md: 0.75rem;
  --radius-lg: 1rem;
  --radius-xl: 1.5rem;
  
  /* Shadows */
  --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}
```

### 12. Quality Assurance Checklist

Before delivering any design, verify:

**Visual Quality**:
- [ ] Typography is crisp and properly weighted
- [ ] Colors are harmonious and purposeful
- [ ] Spacing is consistent and generous
- [ ] Borders and shadows are subtle and refined
- [ ] Images are high-quality and properly optimized
- [ ] Icons are consistent in style and weight

**Responsive Design**:
- [ ] Layout works on 375px, 768px, 1024px, 1440px, 1920px
- [ ] No horizontal scrolling on mobile
- [ ] Touch targets are sufficiently large
- [ ] Content reflows naturally at all breakpoints
- [ ] Images are responsive and don't overflow

**Interactions**:
- [ ] All interactive elements have hover states
- [ ] Focus states are visible and clear
- [ ] Animations are smooth and purposeful
- [ ] Loading states are implemented
- [ ] Error states are clear and helpful

**Performance**:
- [ ] Images are compressed and optimized
- [ ] No layout shifts during page load
- [ ] JavaScript bundle is minimized
- [ ] Critical CSS is inlined
- [ ] Fonts are properly loaded

**Accessibility**:
- [ ] All images have alt text
- [ ] Color contrast meets WCAG AAA
- [ ] Keyboard navigation works
- [ ] Screen reader friendly
- [ ] Semantic HTML used throughout

## Anti-Patterns to Avoid

**Never do these**:
- ❌ Use default browser styles without customization
- ❌ Rely on generic AI-looking gradients everywhere
- ❌ Use too many fonts (max 2-3)
- ❌ Create cluttered layouts without white space
- ❌ Ignore mobile users (mobile-first is mandatory)
- ❌ Use stock photos that look generic
- ❌ Implement flashy animations that distract
- ❌ Forget focus states for keyboard users
- ❌ Use poor color contrast
- ❌ Build fixed-width layouts that don't respond
- ❌ Neglect performance optimization
- ❌ Copy exact Tailwind UI or other template designs

## Inspiration Sources

Look to these for design excellence:
- **Apple.com** - minimalism and product focus
- **Linear.app** - refined UI and micro-interactions
- **Stripe.com** - clean, professional design
- **Vercel.com** - modern, technical aesthetic
- **Framer.com** - sophisticated animations
- **Airbnb.com** - user-friendly interfaces
- **Figma.com** - collaborative tool design

## Final Polish

The difference between good and exceptional:
- **Micro-interactions**: Buttons that respond to hover with subtle scale and shadow changes
- **Loading states**: Skeleton screens instead of spinners
- **Empty states**: Thoughtful illustrations and helpful copy
- **Error states**: Clear, friendly error messages with recovery steps
- **Smooth transitions**: Every state change animated gracefully
- **Attention to detail**: Pixel-perfect spacing, perfect alignment, intentional hierarchy
- **Brand consistency**: Every element reinforces the brand identity
- **Emotional resonance**: Design that makes users feel something

## Remember

Premium web design is not about adding more—it's about refining what's there until every pixel serves a purpose. The best designs feel effortless because countless hours were spent making them that way. Sweat the details. Question every choice. Aim for timeless over trendy. Create experiences that users remember.