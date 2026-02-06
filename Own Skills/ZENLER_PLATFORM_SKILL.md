# Zenler Platform Compatibility Skill

**Version:** 1.0  
**Last Updated:** February 2026  
**Purpose:** Reference guide for building compatible apps and integrations with the Zenler.com platform

---

## Table of Contents

1. [Platform Overview](#platform-overview)
2. [Technical Stack](#technical-stack)
3. [Architecture Patterns](#architecture-patterns)
4. [Frontend Development](#frontend-development)
5. [Backend Infrastructure](#backend-infrastructure)
6. [Email & Communication](#email--communication)
7. [Asset Management](#asset-management)
8. [Performance Optimization](#performance-optimization)
9. [Design System](#design-system)
10. [Integration Patterns](#integration-patterns)
11. [Security & Compliance](#security--compliance)
12. [Best Practices](#best-practices)
13. [Known Limitations](#known-limitations)
14. [Quick Reference](#quick-reference)

---

## Platform Overview

### What is Zenler?

Zenler is an all-in-one SaaS platform for creating, marketing, and selling online courses, memberships, and coaching programs. It consolidates 10+ tools into a unified system.

### Core Capabilities

- **Course Creation** - Video, audio, PDF, PPT, SCORM, quizzes, surveys
- **Marketing Funnels** - Lead magnets, video series, sales pages
- **Email Automation** - SendGrid-powered transactional and marketing emails
- **Community** - Facebook-like social features with SEO optimization
- **Live Classes** - Zoom integration (up to 500 participants)
- **Site Builder** - Drag-and-drop page designer with templates
- **Membership Sites** - Tiered access, drip content
- **Webinars** - Native hosting up to 4 hours
- **Gamification** - Points, levels, streaks, leaderboards (2025+)

### Multi-Tenant Architecture

Each customer gets a subdomain: `yourschool.zenler.com`

---

## Technical Stack

### Core Technologies

```yaml
Frontend:
  - JavaScript Library: jQuery (not React/Vue/Angular)
  - Tag Management: Google Tag Manager
  - Fonts: Google Font API
  - Mobile: Viewport Meta, iPhone/Mobile Compatible
  
Backend:
  - Hosting: Amazon AWS EC2
  - Region: Oregon (us-west-2)
  - CDN: Amazon CloudFront
  - Architecture: Multi-tenant SaaS (1000+ subdomains)
  
Email:
  - Transactional: SendGrid
  - Business Email: Google Workspace
  - Authentication: SPF, DMARC (None policy)
  
Analytics:
  - Google Analytics 4
  - Google Tag Manager
  - Global Site Tag (gtag.js)
  
Support:
  - Zendesk integration
  
Payment:
  - Stripe
  - PayPal
  - Razorpay
  
Live Video:
  - Zoom (native integration)
  
Security:
  - SSL by Default
  - HTTPS redirect
  - Subdomain isolation
```

### Storage & CDN Structure

```
CloudFront CDN: https://d235vmrai5heq2.cloudfront.net/
├── web/assets/images/
│   ├── logo.svg?v=V3.5.00082 (versioned)
│   ├── elements/ (decorative SVGs)
│   ├── img-icon/ (feature icons)
│   ├── testimonials/ (user photos)
│   └── feature-*.webp (screenshots)
├── flags/ (language flags)
└── [tenant-specific assets]
```

**Key Observations:**
- Uses query string versioning (`?v=VERSION`)
- WebP for images, SVG for icons
- Organized folder structure
- CDN-first architecture

---

## Architecture Patterns

### 1. Multi-Tenant SaaS Pattern

```
User Request → subdomain.zenler.com
            ↓
    AWS Load Balancer
            ↓
    EC2 Instance (shared)
            ↓
    Database (tenant-isolated by subdomain)
            ↓
    S3 Storage → CloudFront CDN
```

**Implications for Your App:**
- Data is isolated by subdomain
- Shared infrastructure = performance considerations
- Cannot access other tenants' data
- Subdomain is your "namespace"

### 2. Event-Driven Automation

```
User Action → Event Queue → Automation Engine → Action
                                              ↓
                                    Email | Tag | Access | Webhook
```

**Trigger Examples:**
- Course enrollment → Welcome email
- Course completion → Certificate + Badge
- Purchase → Access grant + Confirmation
- Inactivity → Re-engagement sequence

**For Your App:**
- Hook into Zenler's event system
- Use triggers for automation
- Build state machines around events

### 3. Template-Based Rendering

```
Template Library → User Selection → Customization Layer → Server-Side Render → CloudFront Cache
```

**Components:**
- Pre-built blocks/sections
- Drag-and-drop interface
- Limited custom CSS/HTML
- Server-side rendering (not client-side SPA)

### 4. Microservices Integration

```
Core Platform (Zenler)
├── Email Service → SendGrid API
├── Live Video → Zoom API
├── Payments → Stripe/PayPal APIs
├── Support → Zendesk API
├── Analytics → Google Analytics API
└── Community → Native (SEO-optimized)
```

---

## Frontend Development

### JavaScript Framework: jQuery

**Critical Understanding:**
Zenler uses **jQuery**, not modern frameworks like React/Vue/Angular.

#### Best Practices

```javascript
// ✅ DO: Use jQuery patterns
$(document).ready(function() {
    // Namespace your code
    var YourApp = {
        init: function() {
            this.bindEvents();
            this.setupCustomFeatures();
        },
        
        bindEvents: function() {
            $('.your-custom-button').on('click', this.handleClick.bind(this));
        },
        
        handleClick: function(e) {
            e.preventDefault();
            // Your logic
        }
    };
    
    YourApp.init();
});

// ✅ DO: Cache jQuery selectors
var $customElement = $('.frequently-accessed-element');

// ✅ DO: Use event delegation for dynamic content
$('body').on('click', '.dynamic-button', function() {
    // Handler
});

// ✅ DO: Leverage Zenler's existing jQuery
if (typeof jQuery !== 'undefined') {
    // jQuery is loaded, use it
}
```

```javascript
// ❌ DON'T: Try to inject React/Vue
// This will cause conflicts
ReactDOM.render(<App />, element); // NO!

// ❌ DON'T: Override core jQuery functions
$.fn.click = function() { }; // NO!

// ❌ DON'T: Load competing frameworks
<script src="vue.js"></script> // NO!
```

#### Working with Google Tag Manager

```javascript
// Push custom events to dataLayer
dataLayer.push({
    'event': 'zenlerAppEvent',
    'eventCategory': 'CustomApp',
    'eventAction': 'ButtonClick',
    'eventLabel': 'Feature Name',
    'eventValue': 1
});

// Track custom conversions
dataLayer.push({
    'event': 'conversion',
    'conversionType': 'courseCompletion',
    'courseId': 'course-123',
    'userId': 'user-456'
});
```

### HTML/CSS Guidelines

```html
<!-- ✅ DO: Use semantic HTML -->
<section class="your-app-section" data-app="antigravity">
    <header class="section-header">
        <h2>Feature Title</h2>
    </header>
    <div class="section-content">
        <!-- Content -->
    </div>
</section>

<!-- ✅ DO: Namespace your CSS classes -->
<div class="ag-container">
    <div class="ag-card">
        <div class="ag-card__header"></div>
        <div class="ag-card__body"></div>
    </div>
</div>

<!-- ❌ DON'T: Use generic class names that might conflict -->
<div class="container"> <!-- Too generic -->
<div class="header"> <!-- Too generic -->
```

```css
/* ✅ DO: Namespace all your CSS */
.ag-container {
    max-width: 1200px;
    margin: 0 auto;
}

.ag-card {
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* ✅ DO: Use responsive breakpoints that match mobile apps */
@media (max-width: 768px) {
    .ag-container {
        padding: 16px;
    }
}

/* ❌ DON'T: Override Zenler's core styles without !important */
.zenler-button {
    background: red; /* May not work */
}

/* ✅ DO: Use specificity or namespace */
.ag-container .zenler-button {
    background: red;
}
```

### Mobile-First Development

```css
/* Mobile First Approach */
.ag-element {
    /* Mobile styles (default) */
    padding: 8px;
    font-size: 14px;
}

@media (min-width: 768px) {
    /* Tablet */
    .ag-element {
        padding: 16px;
        font-size: 16px;
    }
}

@media (min-width: 1024px) {
    /* Desktop */
    .ag-element {
        padding: 24px;
        font-size: 18px;
    }
}
```

**Why Mobile-First?**
- Zenler has native iOS/Android apps
- Users access courses on mobile
- Platform is optimized for mobile delivery

---

## Backend Infrastructure

### AWS Architecture

```
┌─────────────────────────────────────────┐
│         Amazon CloudFront CDN           │
│    (Global Edge Locations)              │
└────────────┬────────────────────────────┘
             │
             ↓
┌─────────────────────────────────────────┐
│         Application Load Balancer       │
└────────────┬────────────────────────────┘
             │
             ↓
┌─────────────────────────────────────────┐
│   EC2 Instances (Oregon Region)         │
│   - Multi-tenant application            │
│   - Subdomain routing                   │
│   - Session management                  │
└────────────┬────────────────────────────┘
             │
      ┌──────┴──────┐
      ↓             ↓
┌──────────┐   ┌──────────┐
│    RDS   │   │    S3    │
│ Database │   │  Storage │
└──────────┘   └──────────┘
```

### Database Structure (Inferred)

**Likely Schema:**

```sql
-- Tenant Isolation Pattern
users
├── id (primary key)
├── tenant_id (subdomain identifier)
├── email
├── password_hash
└── created_at

courses
├── id
├── tenant_id (subdomain identifier)
├── user_id (owner)
├── title
├── content
└── settings (JSON)

enrollments
├── id
├── tenant_id
├── user_id
├── course_id
├── progress (JSON)
└── completed_at
```

**Key Points:**
- Every table has `tenant_id` for isolation
- Cannot access database directly
- Work through Zenler's APIs/interface
- Data exports available through platform

### File Storage Pattern

```
S3 Bucket Structure:
├── static/
│   ├── web/assets/
│   └── shared-resources/
├── tenants/
│   ├── subdomain1/
│   │   ├── courses/
│   │   ├── uploads/
│   │   └── generated/
│   └── subdomain2/
│       └── ...
└── backups/
```

**Access Patterns:**
- CloudFront provides signed URLs for private content
- Public assets cached at edge locations
- Video files likely use progressive download or HLS

---

## Email & Communication

### SendGrid Integration

**Email Flow:**

```
Zenler Platform → SendGrid API → Recipient
                ↓
         Webhook Response
                ↓
    Update Delivery Status
```

**Email Types:**

1. **Transactional Emails** (SendGrid)
   - Account creation
   - Password reset
   - Purchase confirmation
   - Enrollment confirmation
   - Course completion certificates

2. **Marketing Emails** (SendGrid)
   - Newsletter broadcasts
   - Promotional campaigns
   - Course announcements
   - Drip sequences

3. **Automation Emails** (Event-triggered)
   - Welcome sequences
   - Abandoned cart
   - Re-engagement campaigns
   - Milestone celebrations

### Custom Email Integration

```javascript
// Using Zenler's email system
{
    "trigger": "course_completion",
    "action": {
        "type": "email",
        "template_id": "custom_certificate",
        "recipient": "{{user.email}}",
        "variables": {
            "course_name": "{{course.title}}",
            "completion_date": "{{event.date}}",
            "certificate_url": "{{certificate.url}}"
        }
    }
}
```

**Best Practices:**

```javascript
// ✅ DO: Use Zenler's tag system for segmentation
tags = ['course-completed', 'advanced-user', 'premium-member'];

// ✅ DO: Respect email preferences
if (user.email_preferences.marketing === true) {
    sendMarketingEmail();
}

// ✅ DO: Track email engagement
{
    "email_sent": true,
    "opened": false,
    "clicked": false,
    "bounced": false,
    "unsubscribed": false
}

// ❌ DON'T: Send emails outside Zenler's system
// This breaks deliverability tracking
sendEmailDirectly(); // NO!
```

### SMTP Configuration

**Two Options:**

1. **Use Zenler's SMTP** (SendGrid-backed)
   - Pro: Integrated, no setup
   - Con: Shared sender reputation

2. **Connect Custom SMTP**
   - Pro: Your sender reputation
   - Con: Requires DNS configuration
   - Best for: Large email lists (10k+)

---

## Asset Management

### CDN Usage Pattern

```javascript
// ✅ DO: Use Zenler's CDN for platform assets
const logoUrl = 'https://d235vmrai5heq2.cloudfront.net/web/assets/images/logo.svg?v=V3.5.00082';

// ✅ DO: Version your custom assets
const customAsset = '/assets/my-app-feature.js?v=1.2.3';

// ✅ DO: Use appropriate image formats
const images = {
    icon: 'icon.svg',        // Scalable, small file
    photo: 'photo.webp',     // Modern, compressed
    fallback: 'photo.jpg'    // Legacy support
};
```

### Image Optimization

```html
<!-- ✅ DO: Provide WebP with fallback -->
<picture>
    <source srcset="image.webp" type="image/webp">
    <source srcset="image.jpg" type="image/jpeg">
    <img src="image.jpg" alt="Description">
</picture>

<!-- ✅ DO: Use lazy loading -->
<img src="image.webp" loading="lazy" alt="Description">

<!-- ✅ DO: Specify dimensions to prevent layout shift -->
<img src="image.webp" width="800" height="600" alt="Description">
```

### File Upload Handling

**Supported Formats:**
- **Video:** MP4, WebM
- **Audio:** MP3, AAC
- **Documents:** PDF, DOCX, PPT, PPTX
- **Images:** JPG, PNG, WebP, SVG
- **SCORM:** ZIP packages
- **Custom:** HTML, CSS, JS

```javascript
// File upload size limits (inferred)
const limits = {
    video: '2GB',      // Per file
    document: '100MB', // Per file
    image: '10MB',     // Per file
    total: 'Unlimited' // Per account
};
```

---

## Performance Optimization

### CloudFront Caching Strategy

```javascript
// Asset versioning for cache busting
const assetVersion = 'V3.5.00082'; // Matches Zenler pattern

// Cache-friendly URL structure
const url = `${baseUrl}/asset.js?v=${assetVersion}`;

// Force refresh on updates
function updateAssetVersion(newVersion) {
    // Update all asset URLs
    $('script[data-versioned]').each(function() {
        const $script = $(this);
        const src = $script.attr('src').split('?')[0];
        $script.attr('src', `${src}?v=${newVersion}`);
    });
}
```

### Performance Checklist

**✅ Frontend Optimization:**

```javascript
// 1. Minimize DOM manipulation
// ❌ BAD
for (let i = 0; i < 1000; i++) {
    $('.container').append('<div>Item</div>');
}

// ✅ GOOD
let html = '';
for (let i = 0; i < 1000; i++) {
    html += '<div>Item</div>';
}
$('.container').html(html);

// 2. Debounce scroll/resize events
function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

$(window).on('scroll', debounce(function() {
    // Scroll handler
}, 100));

// 3. Use event delegation
// ❌ BAD - attaches handler to every button
$('.button').on('click', handler);

// ✅ GOOD - single handler on parent
$('body').on('click', '.button', handler);
```

**✅ Asset Loading:**

```html
<!-- Defer non-critical JavaScript -->
<script src="analytics.js" defer></script>

<!-- Async for independent scripts -->
<script src="chat-widget.js" async></script>

<!-- Preload critical assets -->
<link rel="preload" href="critical.css" as="style">
<link rel="preload" href="hero-image.webp" as="image">

<!-- DNS prefetch for external resources -->
<link rel="dns-prefetch" href="//d235vmrai5heq2.cloudfront.net">
```

**✅ Video Optimization:**

```javascript
// Lazy load videos
const videos = document.querySelectorAll('video[data-src]');
const videoObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            const video = entry.target;
            video.src = video.dataset.src;
            video.load();
            videoObserver.unobserve(video);
        }
    });
});

videos.forEach(video => videoObserver.observe(video));
```

### Mobile App Considerations

Since Zenler has native iOS/Android apps:

```javascript
// Detect if running in app
function isZenlerApp() {
    return navigator.userAgent.includes('ZenlerApp');
}

// Optimize for app environment
if (isZenlerApp()) {
    // Reduce animations
    document.body.classList.add('zenler-app');
    
    // Use app-specific features
    // (push notifications, offline storage, etc.)
}
```

---

## Design System

### Visual Hierarchy

**Zenler's Design Patterns:**

```css
/* Spacing System (inferred from platform) */
:root {
    --space-xs: 4px;
    --space-sm: 8px;
    --space-md: 16px;
    --space-lg: 24px;
    --space-xl: 32px;
    --space-2xl: 48px;
}

/* Typography Scale */
:root {
    --font-size-xs: 12px;
    --font-size-sm: 14px;
    --font-size-base: 16px;
    --font-size-lg: 18px;
    --font-size-xl: 24px;
    --font-size-2xl: 32px;
}

/* Color Palette (adapt to your brand) */
:root {
    --color-primary: #your-brand-color;
    --color-secondary: #your-secondary-color;
    --color-success: #10b981;
    --color-warning: #f59e0b;
    --color-error: #ef4444;
    --color-text: #1f2937;
    --color-text-muted: #6b7280;
    --color-border: #e5e7eb;
    --color-background: #ffffff;
}
```

### Component Patterns

**Card Component:**

```html
<div class="ag-card">
    <div class="ag-card__header">
        <h3 class="ag-card__title">Card Title</h3>
        <p class="ag-card__subtitle">Optional subtitle</p>
    </div>
    <div class="ag-card__body">
        <p class="ag-card__content">Main content goes here</p>
    </div>
    <div class="ag-card__footer">
        <button class="ag-button ag-button--primary">Action</button>
    </div>
</div>
```

```css
.ag-card {
    background: var(--color-background);
    border: 1px solid var(--color-border);
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.ag-card__header {
    padding: var(--space-lg);
    border-bottom: 1px solid var(--color-border);
}

.ag-card__title {
    margin: 0;
    font-size: var(--font-size-lg);
    font-weight: 600;
    color: var(--color-text);
}

.ag-card__body {
    padding: var(--space-lg);
}

.ag-card__footer {
    padding: var(--space-lg);
    border-top: 1px solid var(--color-border);
    background: #f9fafb;
}
```

**Button Component:**

```html
<!-- Button variations -->
<button class="ag-button ag-button--primary">Primary</button>
<button class="ag-button ag-button--secondary">Secondary</button>
<button class="ag-button ag-button--outline">Outline</button>
<button class="ag-button ag-button--ghost">Ghost</button>
<button class="ag-button ag-button--danger">Danger</button>

<!-- Button sizes -->
<button class="ag-button ag-button--sm">Small</button>
<button class="ag-button ag-button--md">Medium</button>
<button class="ag-button ag-button--lg">Large</button>
```

```css
.ag-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: var(--space-sm) var(--space-md);
    font-size: var(--font-size-base);
    font-weight: 500;
    border: 1px solid transparent;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.2s;
}

.ag-button--primary {
    background: var(--color-primary);
    color: white;
}

.ag-button--primary:hover {
    opacity: 0.9;
    transform: translateY(-1px);
}

.ag-button--sm {
    padding: var(--space-xs) var(--space-sm);
    font-size: var(--font-size-sm);
}

.ag-button--lg {
    padding: var(--space-md) var(--space-lg);
    font-size: var(--font-size-lg);
}
```

### Layout Patterns

**Sidebar + Content (Matches Zenler's course player):**

```html
<div class="ag-layout">
    <aside class="ag-layout__sidebar">
        <!-- Course navigation, curriculum -->
    </aside>
    <main class="ag-layout__content">
        <!-- Main content area -->
    </main>
</div>
```

```css
.ag-layout {
    display: grid;
    grid-template-columns: 300px 1fr;
    min-height: 100vh;
}

.ag-layout__sidebar {
    background: #f9fafb;
    border-right: 1px solid var(--color-border);
    overflow-y: auto;
}

.ag-layout__content {
    padding: var(--space-xl);
    overflow-y: auto;
}

@media (max-width: 768px) {
    .ag-layout {
        grid-template-columns: 1fr;
    }
    
    .ag-layout__sidebar {
        position: fixed;
        top: 0;
        left: -300px;
        width: 300px;
        height: 100vh;
        transition: left 0.3s;
        z-index: 1000;
    }
    
    .ag-layout--sidebar-open .ag-layout__sidebar {
        left: 0;
    }
}
```

### Responsive Grid System

```css
.ag-grid {
    display: grid;
    gap: var(--space-lg);
}

/* 12-column grid */
.ag-grid--12 {
    grid-template-columns: repeat(12, 1fr);
}

/* Common layouts */
.ag-col-6 { grid-column: span 6; }
.ag-col-4 { grid-column: span 4; }
.ag-col-3 { grid-column: span 3; }

/* Responsive */
@media (max-width: 768px) {
    .ag-col-6,
    .ag-col-4,
    .ag-col-3 {
        grid-column: span 12;
    }
}
```

---

## Integration Patterns

### Webhook Integration

**Setting Up Webhooks:**

```javascript
// Zenler supports webhooks for key events
const webhookEvents = [
    'user.created',
    'user.updated',
    'enrollment.created',
    'enrollment.completed',
    'purchase.completed',
    'purchase.refunded',
    'community.post.created',
    'community.member.joined'
];

// Webhook payload structure (typical)
{
    "event": "enrollment.completed",
    "timestamp": "2026-02-03T10:30:00Z",
    "data": {
        "user_id": "user_123",
        "course_id": "course_456",
        "completion_date": "2026-02-03",
        "certificate_url": "https://..."
    }
}
```

**Webhook Handler Example:**

```javascript
// Express.js webhook endpoint
app.post('/webhooks/zenler', (req, res) => {
    const { event, data } = req.body;
    
    switch(event) {
        case 'enrollment.completed':
            // Trigger custom automation
            sendCustomCertificate(data.user_id, data.course_id);
            updateCRM(data.user_id, { status: 'completed' });
            break;
            
        case 'purchase.completed':
            // Track in analytics
            trackConversion(data);
            break;
    }
    
    res.status(200).send('OK');
});
```

### API Integration Patterns

**Working with External APIs:**

```javascript
// Make API calls from custom JavaScript
function integrateWithExternalService() {
    const apiKey = 'your-api-key';
    const endpoint = 'https://api.example.com/v1/resource';
    
    $.ajax({
        url: endpoint,
        method: 'POST',
        headers: {
            'Authorization': `Bearer ${apiKey}`,
            'Content-Type': 'application/json'
        },
        data: JSON.stringify({
            user_id: getUserId(),
            course_data: getCourseData()
        }),
        success: function(response) {
            // Handle response
            updateUI(response);
        },
        error: function(xhr, status, error) {
            console.error('API Error:', error);
            showErrorMessage();
        }
    });
}
```

### Zapier Integration

**Common Zaps for Zenler:**

```yaml
Triggers:
  - New Enrollment
  - Course Completed
  - New Purchase
  - New Community Post
  - Tag Added to User

Actions:
  - Add to Google Sheets
  - Create HubSpot Contact
  - Send Slack Notification
  - Add to Mailchimp List
  - Create Trello Card

Example Zap:
  1. Trigger: Course Completed (Zenler)
  2. Action: Add Row (Google Sheets)
  3. Action: Send Email (Gmail)
  4. Action: Create Contact (HubSpot)
```

### Custom Integrations

**N8N Workflow Example:**

```json
{
  "nodes": [
    {
      "name": "Zenler Webhook",
      "type": "n8n-nodes-base.webhook",
      "webhookId": "zenler-enrollment"
    },
    {
      "name": "Supabase Insert",
      "type": "n8n-nodes-base.supabase",
      "operation": "insert",
      "table": "enrollments"
    },
    {
      "name": "SendGrid Email",
      "type": "n8n-nodes-base.sendgrid",
      "operation": "send"
    }
  ]
}
```

---

## Security & Compliance

### Data Security

**Platform Security Features:**

```yaml
Infrastructure:
  - SSL/TLS encryption (all traffic)
  - AWS security groups
  - DDoS protection (CloudFront)
  - Subdomain isolation
  
Authentication:
  - Password hashing (bcrypt/argon2)
  - Session management
  - Remember me tokens
  - Password reset flow
  
Data Protection:
  - GDPR compliance tools
  - Data export functionality
  - Right to deletion
  - Cookie consent
```

### Best Practices for Your App

```javascript
// ✅ DO: Never store sensitive data in localStorage
// Use sessionStorage for temporary data
sessionStorage.setItem('tempData', JSON.stringify(data));

// ✅ DO: Validate and sanitize user input
function sanitizeInput(input) {
    const div = document.createElement('div');
    div.textContent = input;
    return div.innerHTML;
}

// ✅ DO: Use HTTPS for all external requests
const apiUrl = 'https://secure-api.example.com'; // Always HTTPS

// ❌ DON'T: Expose API keys in frontend code
const apiKey = 'sk_live_abc123'; // NO! This is visible to users

// ✅ DO: Use backend proxy for sensitive operations
function callProtectedAPI(data) {
    return $.ajax({
        url: '/api/proxy/secure-operation', // Your backend
        method: 'POST',
        data: data
    });
}
```

### GDPR Compliance

```javascript
// Cookie consent handling
function setCookie(name, value, days) {
    if (!hasUserConsentedToCookies()) {
        console.warn('Cookie consent required');
        return false;
    }
    
    const expires = new Date();
    expires.setTime(expires.getTime() + days * 24 * 60 * 60 * 1000);
    document.cookie = `${name}=${value};expires=${expires.toUTCString()};path=/;secure`;
}

// Data export functionality
function exportUserData(userId) {
    return {
        personal_info: getUserInfo(userId),
        enrollment_history: getEnrollments(userId),
        purchase_history: getPurchases(userId),
        community_posts: getCommunityPosts(userId),
        certificates: getCertificates(userId)
    };
}

// Data deletion
function deleteUserData(userId) {
    // Zenler provides this through platform
    // Document what gets deleted vs anonymized
}
```

---

## Best Practices

### Development Workflow

**1. Local Development Setup**

```bash
# Recommended structure
your-zenler-app/
├── assets/
│   ├── css/
│   │   └── styles.css
│   ├── js/
│   │   ├── main.js
│   │   └── components/
│   └── images/
├── templates/
│   └── page-templates/
├── config/
│   └── settings.js
└── docs/
    └── README.md
```

**2. Version Control**

```bash
# .gitignore for Zenler projects
node_modules/
.env
.DS_Store
*.log
dist/
build/

# Don't commit Zenler credentials
config/credentials.json
```

**3. Testing Strategy**

```javascript
// Test across Zenler's supported platforms
const testEnvironments = [
    'Chrome Desktop',
    'Safari Desktop',
    'Firefox Desktop',
    'Edge Desktop',
    'Chrome Mobile',
    'Safari iOS',
    'Zenler iOS App',
    'Zenler Android App'
];

// Automated testing considerations
function testCompatibility() {
    // Check jQuery is loaded
    if (typeof jQuery === 'undefined') {
        console.error('jQuery not loaded!');
    }
    
    // Check critical CSS
    const styles = window.getComputedStyle(document.body);
    
    // Check responsive behavior
    const isMobile = window.innerWidth < 768;
}
```

**4. Performance Monitoring**

```javascript
// Track performance metrics
function trackPerformance() {
    if ('performance' in window) {
        const perfData = performance.getEntriesByType('navigation')[0];
        
        dataLayer.push({
            'event': 'performance',
            'pageLoadTime': perfData.loadEventEnd - perfData.fetchStart,
            'domContentLoaded': perfData.domContentLoadedEventEnd - perfData.fetchStart,
            'firstPaint': performance.getEntriesByType('paint')[0].startTime
        });
    }
}

window.addEventListener('load', trackPerformance);
```

### Code Organization

**Modular JavaScript Pattern:**

```javascript
// AntiGravity App Module
var AntiGravity = (function($) {
    'use strict';
    
    // Private variables
    var config = {
        apiEndpoint: '/api/v1',
        debug: false
    };
    
    var state = {
        initialized: false,
        currentUser: null
    };
    
    // Private methods
    function log(message) {
        if (config.debug) {
            console.log('[AntiGravity]', message);
        }
    }
    
    function initializeComponents() {
        log('Initializing components...');
        // Component initialization
    }
    
    // Public API
    return {
        init: function(options) {
            $.extend(config, options);
            initializeComponents();
            state.initialized = true;
            log('Initialized successfully');
        },
        
        getState: function() {
            return state;
        },
        
        // Public methods
        trackEvent: function(eventName, eventData) {
            dataLayer.push({
                'event': 'ag_' + eventName,
                'data': eventData
            });
        }
    };
})(jQuery);

// Initialize when DOM is ready
$(document).ready(function() {
    AntiGravity.init({
        debug: true,
        apiEndpoint: '/api/v2'
    });
});
```

### CSS Architecture (BEM Methodology)

```css
/* Block */
.ag-course-player {}

/* Element */
.ag-course-player__video {}
.ag-course-player__controls {}
.ag-course-player__progress {}

/* Modifier */
.ag-course-player--fullscreen {}
.ag-course-player__video--loading {}

/* Example structure */
.ag-course-player {
    position: relative;
    width: 100%;
    background: #000;
}

.ag-course-player__video {
    width: 100%;
    height: auto;
}

.ag-course-player__controls {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: var(--space-md);
    background: rgba(0,0,0,0.7);
}

.ag-course-player--fullscreen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 9999;
}
```

### Documentation Standards

```javascript
/**
 * AntiGravity Feature Module
 * 
 * @description Handles custom course features for Zenler platform
 * @version 1.2.0
 * @requires jQuery 3.x
 * @zenler-compatible true
 * 
 * @example
 * AntiGravity.Features.init({
 *     feature: 'progress-tracker',
 *     options: {
 *         autoSave: true,
 *         interval: 30000
 *     }
 * });
 */
var Features = (function() {
    // Implementation
})();
```

---

## Known Limitations

### Platform Constraints

**Cannot Do:**

```yaml
Database:
  - Direct database access
  - Custom database schema
  - Raw SQL queries
  
Frontend:
  - Install npm packages directly
  - Use modern build tools (Webpack, Vite)
  - Deploy SPAs (React, Vue, Angular)
  
Backend:
  - Run custom server-side code
  - Install backend frameworks
  - Access file system directly
  
Domain:
  - Fully custom domain structure
  - Subdomain customization beyond base
  - Multiple domains per account (limited)
```

**Workarounds:**

```yaml
Database Needs:
  - Use external database (Supabase, Firebase)
  - Sync via webhooks
  - Store data in user meta fields
  
Modern Frontend:
  - Build locally, upload compiled JS/CSS
  - Use CDN-hosted libraries
  - Vanilla JS or jQuery plugins
  
Backend Logic:
  - External API endpoints
  - Serverless functions (Vercel, Netlify)
  - Zapier/N8N for automation
  
Custom Domain:
  - Use Zenler's CNAME option
  - Reverse proxy setup
  - Subdomain forwarding
```

### Design Limitations

**Course Player Layout:**

```
Fixed Structure:
┌─────────────────────────────────┐
│ Sidebar (300px) │  Main Content │
│                 │               │
│ - Course Nav    │  - Video      │
│ - Curriculum    │  - Text       │
│ - Progress      │  - Resources  │
└─────────────────────────────────┘

Cannot change:
- Sidebar width
- Layout orientation
- Core navigation structure

Can customize:
- Colors
- Fonts
- Content within areas
- Additional overlays
```

### Feature Gaps

**Missing/Limited Features:**

```yaml
A/B Testing:
  - Not built-in
  - Use GTM + external tool
  
Advanced Analytics:
  - Limited to GA4
  - Custom dashboards require export
  
Custom Checkout:
  - Limited customization
  - Can't add upsells natively
  - Use external solution
  
Branded Mobile Apps:
  - Only Premium plan
  - Limited customization
  - Users must use Zenler app
  
Interactive Videos:
  - No native support
  - Use external embeds
  - Limited quiz integration
```

---

## Quick Reference

### Essential URLs

```
Production: https://www.newzenler.com
CDN: https://d235vmrai5heq2.cloudfront.net
Support: https://support.newzenler.com
Status: https://status.newzenler.com
Docs: https://tutorials.newzenler.com
Community: https://facebook.com/groups/newzenlerbeta
```

### Key Technical Specifications

```yaml
Hosting:
  Provider: AWS EC2
  Region: us-west-2 (Oregon)
  CDN: CloudFront
  
Frontend:
  JavaScript: jQuery
  Tag Manager: Google Tag Manager
  Fonts: Google Fonts API
  
Email:
  Service: SendGrid
  SMTP: Available
  Auth: SPF, DMARC
  
Video:
  Live: Zoom integration
  Storage: S3
  Limits: Unlimited
  
Files:
  Max Video: 2GB per file
  Max Document: 100MB
  Max Image: 10MB
  Storage: Unlimited
  
Performance:
  SSL: Required
  HTTP/2: Enabled
  Compression: Gzip/Brotli
  Caching: CloudFront
```

### Common Code Snippets

**Initialize App:**

```javascript
$(document).ready(function() {
    YourApp.init();
});
```

**Track Event:**

```javascript
dataLayer.push({
    'event': 'customEvent',
    'category': 'App',
    'action': 'Action',
    'label': 'Label'
});
```

**Make API Call:**

```javascript
$.ajax({
    url: '/api/endpoint',
    method: 'POST',
    data: JSON.stringify(data),
    contentType: 'application/json',
    success: function(response) {
        // Handle success
    }
});
```

**Responsive Check:**

```javascript
function isMobile() {
    return window.innerWidth < 768;
}
```

**Add Custom Styles:**

```css
.ag-component {
    /* Your styles */
}
```

---

## Changelog

**Version 1.0 (February 2026)**
- Initial skill creation
- Comprehensive platform analysis
- Technical stack documentation
- Best practices compilation
- Integration patterns
- Security guidelines

---

## Additional Resources

### Recommended Reading

1. **Zenler Documentation**
   - https://support.newzenler.com
   - https://tutorials.newzenler.com

2. **jQuery Documentation**
   - https://api.jquery.com
   - https://learn.jquery.com

3. **AWS CloudFront**
   - https://docs.aws.amazon.com/cloudfront

4. **SendGrid API**
   - https://docs.sendgrid.com

5. **Google Tag Manager**
   - https://developers.google.com/tag-manager

### Community

- **Zenler Facebook Group:** https://facebook.com/groups/newzenlerbeta
- **Zenler Status Page:** https://status.newzenler.com

---

## Support

For questions about this skill or Zenler platform compatibility:
1. Check Zenler's official documentation
2. Join the Zenler community
3. Contact Zenler support
4. Reference this skill for best practices

---

**End of Zenler Platform Compatibility Skill**
