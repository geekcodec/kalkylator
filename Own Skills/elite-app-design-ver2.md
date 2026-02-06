markdown---
name: elite-mobile-app-design
description: Creates world-class native mobile app UI/UX through systematic design decisions, proven patterns, and rigorous quality enforcement. Use for any mobile interface requiring professional polish, intuitive UX, and platform-native feel. Prevents common mistakes through explicit anti-patterns and decision frameworks.
---

# Elite Mobile App Design System

This skill transforms mobile app development into a systematic, quality-guaranteed process that consistently produces exceptional results indistinguishable from apps by top-tier studios.

## CRITICAL: How to Use This Skill

**This skill is organized as a PROCESS, not a reference manual. Follow it sequentially:**

1. **Phase 1: Strategic Foundation** → Understand purpose, choose platform approach
2. **Phase 2: Design System Setup** → Establish tokens, never deviate
3. **Phase 3: Information Architecture** → Structure app before designing screens
4. **Phase 4: Component Selection** → Use pre-built patterns, don't invent
5. **Phase 5: Screen Assembly** → Compose screens from components
6. **Phase 6: Flow & Navigation** → Connect screens into user journeys
7. **Phase 7: Interaction Design** → Add gestures, animations, feedback
8. **Phase 8: State Management** → Design all states (loading, error, empty, success)
9. **Phase 9: Polish & Refinement** → Micro-interactions, haptics, transitions
10. **Phase 10: Quality Validation** → Mandatory checkpoint before delivery

**DO NOT skip phases. Each builds on the previous.**

---

## Phase 1: Strategic Foundation

### Step 1.1: App Purpose Classification

**Choose ONE primary purpose (this drives all subsequent decisions):**

**A) Task Completion App** (Banking, To-Do, Productivity)
```
User Goal: Complete specific task efficiently
Design Priorities:
  1. Speed to task completion
  2. Clarity of information
  3. Error prevention
  4. Trust signals

Design Implications:
  - Minimal visual decoration
  - Large touch targets (reduce errors)
  - Clear progress indicators
  - Prominent CTAs
  - Conservative color palette
  - Data-dense when appropriate
  - Confirmation dialogs for destructive actions
  
Avoid:
  - Splash screens (slow down task)
  - Unnecessary animations
  - Hidden features
  - Ambiguous button labels
```

**B) Content Consumption App** (News, Social Media, Entertainment)
```
User Goal: Discover and consume content
Design Priorities:
  1. Content visibility
  2. Easy navigation/discovery
  3. Infinite engagement
  4. Shareability

Design Implications:
  - Full-bleed images/video
  - Minimal UI chrome
  - Gesture-based navigation
  - Infinite scroll
  - Quick actions (like, share, save)
  - Rich media handling
  - Subtle UI that fades away
  
Avoid:
  - Cluttered navigation bars
  - Competing visual elements
  - Slow image loading
  - Intrusive ads/CTAs
```

**C) Data Dashboard App** (Analytics, Health, Finance)
```
User Goal: Understand data, spot trends, make decisions
Design Priorities:
  1. Data clarity
  2. Scanability
  3. Actionable insights
  4. Customization

Design Implications:
  - Chart-heavy layouts
  - Clear visual hierarchy
  - Color-coded data
  - Filter/sort controls
  - Comparison features
  - Export capabilities
  - Dense information displays
  
Avoid:
  - Decorative elements
  - Distracting animations
  - Poor contrast in charts
  - Unlabeled data points
```

**D) Social/Communication App** (Messaging, Dating, Communities)
```
User Goal: Connect with others, express identity
Design Priorities:
  1. Real-time feedback
  2. Personalization
  3. Rich expression
  4. Notifications strategy

Design Implications:
  - Avatar-first design
  - Rich media support
  - Typing indicators
  - Read receipts
  - Reaction systems
  - Profile customization
  - Push notification excellence
  
Avoid:
  - Delayed feedback
  - Generic profiles
  - Text-only interactions
  - Unclear online status
```

**E) Utility Tool App** (Calculator, Weather, Scanner)
```
User Goal: Quick answer or action, then exit
Design Priorities:
  1. Instant launch
  2. Immediate value
  3. No learning curve
  4. Widget support

Design Implications:
  - Single-screen focused
  - Large, clear controls
  - Instant feedback
  - Minimal navigation
  - Widget integration
  - Shortcuts support
  - No onboarding needed
  
Avoid:
  - Multi-step flows
  - Account requirements
  - Complex settings
  - Tutorial screens
```

**DECISION FRAMEWORK:**
```
User spends < 30 seconds in app? → Utility Tool
User creates/shares content? → Social/Communication
User analyzes information? → Data Dashboard
User reads/watches content? → Content Consumption
User completes specific tasks? → Task Completion
```

### Step 1.2: Platform Strategy Decision

**Choose ONE approach (affects entire design system):**

**Option A: iOS-First, iOS-Only**
```
When to choose:
  - Target audience is primarily iOS users (US, Western Europe, Japan)
  - Budget allows single platform focus
  - App leverages iOS-specific features (FaceID, Apple Pay, Shortcuts)
  - Need fastest time to market on one platform

Design approach:
  - 100% iOS Human Interface Guidelines
  - SF Pro font family exclusively
  - iOS system colors and components
  - Bottom-aligned navigation (tab bar)
  - Swipe-back gestures throughout
  - Large titles that collapse
  - Context menus (long press)
  - Haptic Feedback API

File structure:
  /screens/ios/
  /components/ios/
  /design-tokens/ios-tokens.ts
```

**Option B: Android-First, Android-Only**
```
When to choose:
  - Target audience is primarily Android users (Asia, South America, Africa)
  - Budget allows single platform focus
  - App leverages Android-specific features (widgets, notifications)
  - Material Design aesthetic fits brand

Design approach:
  - 100% Material Design 3 guidelines
  - Roboto font family exclusively
  - Material You dynamic theming
  - Bottom navigation or drawer
  - Floating Action Buttons
  - Material motion system
  - Elevation and surfaces
  - Ripple effects

File structure:
  /screens/android/
  /components/android/
  /design-tokens/material-tokens.ts
```

**Option C: Cross-Platform with Platform Adaptation**
```
When to choose:
  - Need both iOS and Android
  - Budget supports 10-20% extra dev time for platform variants
  - User base is split across platforms
  - Most common choice for commercial apps

Design approach:
  - Shared core design system
  - Platform-specific navigation patterns
  - Platform-specific components where expectations differ
  - 80% shared components, 20% platform variants
  - Conditional rendering based on Platform.OS

File structure:
  /screens/shared/
  /components/shared/
  /components/ios/
  /components/android/
  /design-tokens/shared-tokens.ts
  /design-tokens/ios-overrides.ts
  /design-tokens/android-overrides.ts

Platform divergence points (must handle differently):
  1. Navigation (TabBar vs BottomNav)
  2. Action buttons (iOS buttons vs FAB)
  3. Modals (iOS sheets vs Material dialogs)
  4. Form controls (iOS switches vs Material switches)
  5. Icons (SF Symbols vs Material Icons)
  6. Typography (SF Pro vs Roboto)
  7. Haptics (iOS Haptic Feedback vs Android Vibration)
```

**DECISION FRAMEWORK:**
```
Revenue primarily from one platform? → Single platform
Need feature parity on both? → Cross-platform adapted
Limited budget? → Single platform first, port later
Global audience? → Cross-platform adapted
```

### Step 1.3: Target Device Matrix

**Define minimum and optimal targets:**
```typescript
// Device Matrix Configuration
const DEVICE_TARGETS = {
  ios: {
    minimum: {
      device: 'iPhone SE (3rd gen)',
      screenSize: { width: 375, height: 667 },
      os: 'iOS 15.0',
      safeArea: { top: 20, bottom: 0, left: 0, right: 0 },
    },
    optimal: {
      device: 'iPhone 14 Pro',
      screenSize: { width: 393, height: 852 },
      os: 'iOS 17.0',
      safeArea: { top: 59, bottom: 34, left: 0, right: 0 },
    },
    large: {
      device: 'iPhone 15 Pro Max',
      screenSize: { width: 430, height: 932 },
      os: 'iOS 17.0',
      safeArea: { top: 59, bottom: 34, left: 0, right: 0 },
    },
    tablet: {
      device: 'iPad Pro 11"',
      screenSize: { width: 834, height: 1194 },
      os: 'iPadOS 17.0',
    }
  },
  android: {
    minimum: {
      device: 'Samsung Galaxy A13',
      screenSize: { width: 360, height: 800 },
      os: 'Android 12',
      dpi: 320,
    },
    optimal: {
      device: 'Google Pixel 7',
      screenSize: { width: 412, height: 915 },
      os: 'Android 14',
      dpi: 440,
    },
    large: {
      device: 'Samsung Galaxy S23 Ultra',
      screenSize: { width: 480, height: 1080 },
      os: 'Android 14',
      dpi: 560,
    },
    tablet: {
      device: 'Samsung Galaxy Tab S9',
      screenSize: { width: 712, height: 1138 },
      os: 'Android 14',
    }
  }
};

// MANDATORY: Test on minimum device before considering done
// RECOMMENDED: Design primarily for optimal device
// NICE TO HAVE: Optimize for large devices and tablets
```

**Testing Requirements:**
```
EVERY screen must be tested on:
  ✓ Minimum device (smallest supported)
  ✓ Optimal device (primary design target)
  ✓ Large device (largest common size)
  ✓ Both orientations (portrait + landscape)
  ✓ Both color schemes (light + dark)
  ✓ Largest text size setting
  ✓ Reduced motion enabled
```

---

## Phase 2: Design System Setup

### Step 2.1: Design Tokens (Copy Exactly, Customize Values Only)
```typescript
// design-tokens.ts
// CRITICAL: Once set, these are IMMUTABLE within a project
// Changing mid-project causes inconsistency

export const SPACING = {
  // 8pt grid - NEVER use values outside this system
  0: 0,
  1: 4,    // 0.25rem - Minimal gap
  2: 8,    // 0.5rem  - Compact spacing
  3: 12,   // 0.75rem - Small gap
  4: 16,   // 1rem    - Default spacing
  5: 20,   // 1.25rem - Comfortable gap
  6: 24,   // 1.5rem  - Section spacing
  8: 32,   // 2rem    - Large spacing
  10: 40,  // 2.5rem  - Major spacing
  12: 48,  // 3rem    - Screen padding
  16: 64,  // 4rem    - Hero spacing
  20: 80,  // 5rem    - Dramatic spacing
  24: 96,  // 6rem    - XXL spacing
  32: 128, // 8rem    - XXXL spacing
} as const;

// VALIDATION: Enforce spacing system
export const validateSpacing = (value: number): boolean => {
  return Object.values(SPACING).includes(value);
};

export const TYPOGRAPHY = {
  // iOS Scale (SF Pro)
  ios: {
    largeTitle: { size: 34, weight: '700', lineHeight: 41 },
    title1: { size: 28, weight: '700', lineHeight: 34 },
    title2: { size: 22, weight: '700', lineHeight: 28 },
    title3: { size: 20, weight: '600', lineHeight: 25 },
    headline: { size: 17, weight: '600', lineHeight: 22 },
    body: { size: 17, weight: '400', lineHeight: 22 },
    callout: { size: 16, weight: '400', lineHeight: 21 },
    subheadline: { size: 15, weight: '400', lineHeight: 20 },
    footnote: { size: 13, weight: '400', lineHeight: 18 },
    caption1: { size: 12, weight: '400', lineHeight: 16 },
    caption2: { size: 11, weight: '400', lineHeight: 13 },
  },
  
  // Android Scale (Roboto)
  android: {
    displayLarge: { size: 57, weight: '400', lineHeight: 64 },
    displayMedium: { size: 45, weight: '400', lineHeight: 52 },
    displaySmall: { size: 36, weight: '400', lineHeight: 44 },
    headlineLarge: { size: 32, weight: '400', lineHeight: 40 },
    headlineMedium: { size: 28, weight: '400', lineHeight: 36 },
    headlineSmall: { size: 24, weight: '400', lineHeight: 32 },
    titleLarge: { size: 22, weight: '500', lineHeight: 28 },
    titleMedium: { size: 16, weight: '500', lineHeight: 24 },
    titleSmall: { size: 14, weight: '500', lineHeight: 20 },
    bodyLarge: { size: 16, weight: '400', lineHeight: 24 },
    bodyMedium: { size: 14, weight: '400', lineHeight: 20 },
    bodySmall: { size: 12, weight: '400', lineHeight: 16 },
    labelLarge: { size: 14, weight: '500', lineHeight: 20 },
    labelMedium: { size: 12, weight: '500', lineHeight: 16 },
    labelSmall: { size: 11, weight: '500', lineHeight: 16 },
  },
} as const;

export const COLORS = {
  // Semantic colors that adapt to light/dark mode
  light: {
    // Primary - Brand color
    primary: '#007AFF',
    primaryVariant: '#0051D5',
    onPrimary: '#FFFFFF',
    
    // Background layers
    background: '#FFFFFF',
    backgroundSecondary: '#F2F2F7',
    backgroundTertiary: '#FFFFFF',
    
    // Surfaces (cards, sheets)
    surface: '#FFFFFF',
    surfaceVariant: '#F2F2F7',
    onSurface: '#000000',
    
    // Text colors
    textPrimary: 'rgba(0, 0, 0, 0.87)',
    textSecondary: 'rgba(0, 0, 0, 0.60)',
    textTertiary: 'rgba(0, 0, 0, 0.38)',
    textDisabled: 'rgba(0, 0, 0, 0.16)',
    
    // Borders and dividers
    border: 'rgba(0, 0, 0, 0.12)',
    divider: 'rgba(0, 0, 0, 0.08)',
    
    // Semantic states
    success: '#34C759',
    warning: '#FF9500',
    error: '#FF3B30',
    info: '#007AFF',
    
    // Interactive states
    ripple: 'rgba(0, 0, 0, 0.08)',
    hover: 'rgba(0, 0, 0, 0.04)',
    pressed: 'rgba(0, 0, 0, 0.12)',
    focus: 'rgba(0, 122, 255, 0.12)',
  },
  
  dark: {
    primary: '#0A84FF',
    primaryVariant: '#409CFF',
    onPrimary: '#000000',
    
    background: '#000000',
    backgroundSecondary: '#1C1C1E',
    backgroundTertiary: '#2C2C2E',
    
    surface: '#1C1C1E',
    surfaceVariant: '#2C2C2E',
    onSurface: '#FFFFFF',
    
    textPrimary: 'rgba(255, 255, 255, 0.87)',
    textSecondary: 'rgba(255, 255, 255, 0.60)',
    textTertiary: 'rgba(255, 255, 255, 0.38)',
    textDisabled: 'rgba(255, 255, 255, 0.16)',
    
    border: 'rgba(255, 255, 255, 0.12)',
    divider: 'rgba(255, 255, 255, 0.08)',
    
    success: '#32D74B',
    warning: '#FF9F0A',
    error: '#FF453A',
    info: '#0A84FF',
    
    ripple: 'rgba(255, 255, 255, 0.08)',
    hover: 'rgba(255, 255, 255, 0.04)',
    pressed: 'rgba(255, 255, 255, 0.12)',
    focus: 'rgba(10, 132, 255, 0.12)',
  },
} as const;

export const ELEVATION = {
  // iOS shadows (subtle)
  ios: {
    none: { shadowOpacity: 0 },
    sm: { 
      shadowColor: '#000',
      shadowOffset: { width: 0, height: 1 },
      shadowOpacity: 0.05,
      shadowRadius: 2,
    },
    md: {
      shadowColor: '#000',
      shadowOffset: { width: 0, height: 2 },
      shadowOpacity: 0.08,
      shadowRadius: 8,
    },
    lg: {
      shadowColor: '#000',
      shadowOffset: { width: 0, height: 4 },
      shadowOpacity: 0.12,
      shadowRadius: 16,
    },
  },
  
  // Android elevation (dp)
  android: {
    0: 0,
    1: 1,
    2: 3,
    3: 6,
    4: 8,
    5: 12,
  },
} as const;

export const RADIUS = {
  none: 0,
  sm: 6,
  md: 8,
  lg: 12,
  xl: 16,
  '2xl': 24,
  full: 9999,
} as const;

export const ANIMATION = {
  duration: {
    instant: 0,
    fast: 150,
    normal: 250,
    slow: 350,
    slower: 500,
  },
  
  easing: {
    // iOS curves
    ios: {
      standard: [0.4, 0.0, 0.2, 1.0],
      decelerate: [0.0, 0.0, 0.2, 1.0],
      accelerate: [0.4, 0.0, 1.0, 1.0],
      spring: { tension: 300, friction: 20 },
    },
    
    // Material curves
    android: {
      standard: [0.4, 0.0, 0.2, 1.0],
      decelerate: [0.0, 0.0, 0.2, 1.0],
      accelerate: [0.4, 0.0, 1.0, 1.0],
      emphasized: [0.2, 0.0, 0.0, 1.0],
    },
  },
} as const;

export const TOUCH_TARGET = {
  minimum: 44,      // iOS minimum, Android minimum is 48
  comfortable: 56,  // Recommended for primary actions
  large: 64,        // For important actions
} as const;

export const Z_INDEX = {
  base: 0,
  dropdown: 1000,
  sticky: 1100,
  fixed: 1200,
  modalBackdrop: 1300,
  modal: 1400,
  popover: 1500,
  tooltip: 1600,
  toast: 1700,
} as const;
```

### Step 2.2: Color Usage Rules (MANDATORY)
```typescript
// Color Decision Tree
export const getTextColor = (
  background: 'light' | 'dark',
  emphasis: 'primary' | 'secondary' | 'tertiary' | 'disabled'
): string => {
  const colors = background === 'light' ? COLORS.light : COLORS.dark;
  
  switch (emphasis) {
    case 'primary': return colors.textPrimary;
    case 'secondary': return colors.textSecondary;
    case 'tertiary': return colors.textTertiary;
    case 'disabled': return colors.textDisabled;
  }
};

// NEVER use arbitrary colors
// ❌ BAD: color: '#888888'
// ✅ GOOD: color: getTextColor('light', 'secondary')

// Contrast Validation
export const meetsContrastRequirement = (
  foreground: string,
  background: string,
  level: 'AA' | 'AAA' = 'AA'
): boolean => {
  const ratio = calculateContrastRatio(foreground, background);
  const required = level === 'AAA' ? 7.0 : 4.5;
  return ratio >= required;
};

// MANDATORY: All text must pass contrast check
// Usage:
if (!meetsContrastRequirement(textColor, backgroundColor)) {
  throw new Error('Insufficient contrast ratio');
}
```

---

## Phase 3: Information Architecture

### Step 3.1: Navigation Structure Decision

**DECISION TREE: Choose your navigation pattern**
```typescript
type NavigationPattern = 
  | 'flat-tabs'           // 3-5 equal-weight sections
  | 'hierarchical'        // Deep drill-down
  | 'hub-spoke'          // Central hub, radial features
  | 'linear-flow'        // Wizard/onboarding
  | 'modal-driven'       // Task-focused overlays
  | 'content-feed';      // Infinite scroll primary

// Navigation Pattern Selector
function selectNavigationPattern(appType: AppPurpose): NavigationPattern {
  switch (appType) {
    case 'social':
    case 'content-consumption':
      return 'flat-tabs'; // Home, Discover, Profile
      
    case 'task-completion':
      if (hasDeepHierarchy) return 'hierarchical';
      if (hasMultipleTopFeatures) return 'flat-tabs';
      return 'hub-spoke';
      
    case 'data-dashboard':
      return 'flat-tabs'; // Overview, Details, Settings
      
    case 'utility-tool':
      return 'modal-driven'; // Single screen + quick actions
      
    case 'e-commerce':
      return 'hierarchical'; // Browse → Category → Product → Checkout
  }
}
```

**Pattern A: Flat Tabs (Most Common)**
```typescript
// Use when:
// - 3-5 top-level sections of equal importance
// - User switches between sections frequently
// - Each section is independently valuable

// iOS Implementation
const TabNavigation = () => (
  
    <Tab.Screen 
      name="Home"
      component={HomeScreen}
      options={{
        tabBarIcon: ({ color, size }) => ,
      }}
    />
    <Tab.Screen 
      name="Search"
      component={SearchScreen}
      options={{
        tabBarIcon: ({ color, size }) => ,
      }}
    />
    <Tab.Screen 
      name="Profile"
      component={ProfileScreen}
      options={{
        tabBarIcon: ({ color, size }) => ,
      }}
    />
  
);

// Android Implementation (Material Bottom Navigation)
const BottomNavigation = () => (
  
    
    {/* ... */}
  
);

// RULES:
// - 3-5 tabs maximum (5 is pushing it)
// - Always show labels on mobile
// - Icons + labels together
// - Never hide tab bar on scroll
// - Most important tab goes first (usually Home)
```

**Pattern B: Hierarchical (Deep Navigation)**
```typescript
// Use when:
// - Content has natural parent-child relationships
// - Users drill down into details
// - Back navigation is primary way to navigate up

const HierarchicalNav = () => (
  <Stack.Navigator
    screenOptions={{
      headerShown: true,
      headerBackTitleVisible: false, // iOS
      headerTitleAlign: 'center',
      gestureEnabled: true,
      gestureDirection: 'horizontal',
      animation: 'slide_from_right',
    }}
  >
    
    <Stack.Screen 
      name="CategoryDetail"
      component={CategoryDetailScreen}
      options={({ route }) => ({ title: route.params.categoryName })}
    />
    
  
);

// RULES:
// - Maximum 3 levels deep before rethinking structure
// - Always show back button
// - Page title = current level
// - Breadcrumbs on tablet/desktop
```

**Pattern C: Hub-Spoke (Central Dashboard)**
```typescript
// Use when:
// - Single home screen with multiple entry points
// - Features are independent of each other
// - User returns to hub between tasks

const HubScreen = () => (
  
    
      Good morning, {userName}
      
    
    
    
      }
        onPress={() => navigate('Payments')}
      />
      }
        onPress={() => navigate('Transfers')}
      />
      }
        onPress={() => navigate('Cards')}
      />
      }
        onPress={() => navigate('Settings')}
      />
    
    
    
  
);

// RULES:
// - Hub is always home (tab 1 or root screen)
// - Features presented as cards/buttons
// - Each spoke returns to hub when done
// - Maximum 8-10 spokes before overwhelming
```

### Step 3.2: Screen Hierarchy Mapping
```typescript
// Create this BEFORE designing any screens
interface AppStructure {
  navigation: NavigationPattern;
  screens: ScreenDefinition[];
}

interface ScreenDefinition {
  id: string;
  title: string;
  level: number; // 0 = top level, 1 = second level, etc.
  parent?: string;
  children?: string[];
  purpose: 'list' | 'detail' | 'form' | 'dashboard' | 'settings';
  canReachFrom: string[]; // Which screens can navigate here
}

// Example: E-commerce app
const APP_STRUCTURE: AppStructure = {
  navigation: 'flat-tabs',
  screens: [
    {
      id: 'home',
      title: 'Home',
      level: 0,
      purpose: 'dashboard',
      canReachFrom: [],
    },
    {
      id: 'categories',
      title: 'Shop',
      level: 0,
      purpose: 'list',
      canReachFrom: [],
      children: ['category-detail'],
    },
    {
      id: 'category-detail',
      title: 'Category',
      level: 1,
      parent: 'categories',
      purpose: 'list',
      canReachFrom: ['categories', 'search'],
      children: ['product-detail'],
    },
    {
      id: 'product-detail',
      title: 'Product',
      level: 2,
      parent: 'category-detail',
      purpose: 'detail',
      canReachFrom: ['category-detail', 'favorites', 'cart'],
    },
    {
      id: 'cart',
      title: 'Cart',
      level: 0,
      purpose: 'list',
      canReachFrom: [],
      children: ['checkout'],
    },
    {
      id: 'checkout',
      title: 'Checkout',
      level: 1,
      parent: 'cart',
      purpose: 'form',
      canReachFrom: ['cart'],
    },
  ],
};

// VALIDATION: Ensure structure makes sense
function validateStructure(structure: AppStructure): string[] {
  const errors: string[] = [];
  
  // Check for orphaned screens
  structure.screens.forEach(screen => {
    if (screen.level > 0 && !screen.parent) {
      errors.push(`Screen ${screen.id} has level > 0 but no parent`);
    }
  });
  
  // Check for too-deep hierarchies
  const maxDepth = Math.max(...structure.screens.map(s => s.level));
  if (maxDepth > 3) {
    errors.push(`Hierarchy is ${maxDepth} levels deep. Consider flattening.`);
  }
  
  // Check for unreachable screens
  structure.screens.forEach(screen => {
    if (screen.level > 0 && screen.canReachFrom.length === 0) {
      errors.push(`Screen ${screen.id} is unreachable`);
    }
  });
  
  return errors;
}
```

---

## Phase 4: Component Library (Platform-Specific)

### Step 4.1: Button System (Complete Specification)
```typescript
// Button Variant Decision Tree
type ButtonVariant = 'filled' | 'tinted' | 'outlined' | 'ghost';
type ButtonSize = 'small' | 'medium' | 'large';
type ButtonPriority = 'primary' | 'secondary' | 'tertiary' | 'destructive';

// DECISION FRAMEWORK:
function selectButtonVariant(
  priority: ButtonPriority,
  context: 'modal' | 'screen' | 'card'
): ButtonVariant {
  if (priority === 'primary') {
    return 'filled'; // Always filled for primary action
  }
  
  if (priority === 'destructive') {
    return context === 'modal' ? 'filled' : 'ghost';
  }
  
  if (priority === 'secondary') {
    return context === 'modal' ? 'outlined' : 'tinted';
  }
  
  return 'ghost'; // Tertiary actions
}

// iOS Button Component
interface ButtonProps {
  variant: ButtonVariant;
  size: ButtonSize;
  onPress: () => void;
  disabled?: boolean;
  loading?: boolean;
  icon?: ReactNode;
  children: string;
  fullWidth?: boolean;
  destructive?: boolean;
}

const IOSButton: React.FC = ({
  variant,
  size,
  onPress,
  disabled = false,
  loading = false,
  icon,
  children,
  fullWidth = false,
  destructive = false,
}) => {
  // Trigger haptic feedback on press
  const handlePress = () => {
    if (!disabled && !loading) {
      HapticFeedback.impact('light');
      onPress();
    }
  };
  
  // Size specifications
  const sizeStyles = {
    small: {
      height: 28,
      paddingHorizontal: SPACING[2],
      fontSize: TYPOGRAPHY.ios.caption1.size,
    },
    medium: {
      height: 44,
      paddingHorizontal: SPACING[4],
      fontSize: TYPOGRAPHY.ios.body.size,
    },
    large: {
      height: 50,
      paddingHorizontal: SPACING[6],
      fontSize: TYPOGRAPHY.ios.headline.size,
    },
  };
  
  // Variant specifications
  const getVariantStyles = () => {
    const baseColor = destructive ? COLORS.light.error : COLORS.light.primary;
    
    switch (variant) {
      case 'filled':
        return {
          backgroundColor: baseColor,
          color: COLORS.light.onPrimary,
        };
      case 'tinted':
        return {
          backgroundColor: `${baseColor}15`, // 15% opacity
          color: baseColor,
        };
      case 'outlined':
        return {
          backgroundColor: 'transparent',
          borderWidth: 2,
          borderColor: baseColor,
          color: baseColor,
        };
      case 'ghost':
        return {
          backgroundColor: 'transparent',
          color: baseColor,
        };
    }
  };
  
  return (
    
      {loading ? (
        <ActivityIndicator 
          size="small" 
          color={variant === 'filled' ? COLORS.light.onPrimary : COLORS.light.primary} 
        />
      ) : (
        <>
          {icon && {icon}}
          
            {children}
          
        </>
      )}
    
  );
};

const styles = StyleSheet.create({
  button: {
    borderRadius: RADIUS.lg,
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'center',
    gap: SPACING[2],
  },
  fullWidth: {
    width: '100%',
  },
  disabled: {
    opacity: 0.4,
  },
  icon: {
    width: 18,
    height: 18,
  },
  text: {
    fontWeight: '600',
  },
});

// USAGE RULES:
// 1. Maximum ONE filled button per screen section
// 2. Primary action is always filled
// 3. Secondary actions use tinted or outlined
// 4. Tertiary actions use ghost
// 5. Destructive actions in modals are filled red
// 6. Destructive actions in screens are ghost red
// 7. Always provide haptic feedback
// 8. Loading state shows spinner, disables interaction
```

### Step 4.2: Input Field System
```typescript
// Input Field Component (iOS Style)
interface InputFieldProps {
  label: string;
  value: string;
  onChangeText: (text: string) => void;
  placeholder?: string;
  error?: string;
  helperText?: string;
  required?: boolean;
  disabled?: boolean;
  secureTextEntry?: boolean;
  keyboardType?: KeyboardTypeOptions;
  autoCapitalize?: 'none' | 'sentences' | 'words' | 'characters';
  autoComplete?: string;
  maxLength?: number;
  multiline?: boolean;
  numberOfLines?: number;
  leftIcon?: ReactNode;
  rightIcon?: ReactNode;
  onFocus?: () => void;
  onBlur?: () => void;
}

const InputField: React.FC = ({
  label,
  value,
  onChangeText,
  placeholder,
  error,
  helperText,
  required = false,
  disabled = false,
  secureTextEntry = false,
  keyboardType = 'default',
  autoCapitalize = 'sentences',
  autoComplete,
  maxLength,
  multiline = false,
  numberOfLines = 1,
  leftIcon,
  rightIcon,
  onFocus,
  onBlur,
}) => {
  const [isFocused, setIsFocused] = useState(false);
  const inputId = useId();
  
  const handleFocus = () => {
    setIsFocused(true);
    onFocus?.();
  };
  
  const handleBlur = () => {
    setIsFocused(false);
    onBlur?.();
  };
  
  return (
    
      {/* Label */}
      
        
          {label}
        
        {required && (
          *
        )}
      
      
      {/* Input Container */}
      
        {leftIcon && (
          {leftIcon}
        )}
        
        
        
        {rightIcon && (
          {rightIcon}
        )}
      
      
      {/* Helper Text / Error */}
      {(error || helperText) && (
        
          {error || helperText}
        
      )}
      
      {/* Character Count */}
      {maxLength && (
        
          {value.length}/{maxLength}
        
      )}
    
  );
};

const styles = StyleSheet.create({
  container: {
    width: '100%',
    marginBottom: SPACING[4],
  },
  labelContainer: {
    flexDirection: 'row',
    marginBottom: SPACING[2],
  },
  label: {
    fontSize: TYPOGRAPHY.ios.subheadline.size,
    fontWeight: '500',
    color: COLORS.light.textPrimary,
  },
  labelError: {
    color: COLORS.light.error,
  },
  required: {
    color: COLORS.light.error,
    marginLeft: SPACING[1],
  },
  inputContainer: {
    flexDirection: 'row',
    alignItems: 'center',
    backgroundColor: COLORS.light.backgroundSecondary,
    borderRadius: RADIUS.lg,
    borderWidth: 2,
    borderColor: 'transparent',
    paddingHorizontal: SPACING[4],
    minHeight: 44,
  },
  inputContainerFocused: {
    borderColor: COLORS.light.primary,
    backgroundColor: COLORS.light.background,
    ...Platform.select({
      ios: {
        shadowColor: COLORS.light.primary,
        shadowOffset: { width: 0, height: 0 },
        shadowOpacity: 0.15,
        shadowRadius: 4,
      },
      android: {
        elevation: 2,
      },
    }),
  },
  inputContainerError: {
    borderColor: COLORS.light.error,
  },
  inputContainerDisabled: {
    opacity: 0.5,
    backgroundColor: COLORS.light.backgroundTertiary,
  },
  input: {
    flex: 1,
    fontSize: TYPOGRAPHY.ios.body.size,
    color: COLORS.light.textPrimary,
    paddingVertical: SPACING[3],
  },
  inputMultiline: {
    minHeight: 88,
    textAlignVertical: 'top',
    paddingTop: SPACING[3],
  },
  leftIcon: {
    marginRight: SPACING[2],
  },
  rightIcon: {
    marginLeft: SPACING[2],
  },
  helperText: {
    fontSize: TYPOGRAPHY.ios.footnote.size,
    color: COLORS.light.textSecondary,
    marginTop: SPACING[2],
  },
  errorText: {
    color: COLORS.light.error,
  },
  characterCount: {
    fontSize: TYPOGRAPHY.ios.caption2.size,
    color: COLORS.light.textTertiary,
    textAlign: 'right',
    marginTop: SPACING[1],
  },
});

// VALIDATION HELPER
const validateInput = (
  value: string,
  rules: ValidationRules
): string | undefined => {
  if (rules.required && !value) {
    return `${rules.fieldName} is required`;
  }
  
  if (rules.minLength && value.length < rules.minLength) {
    return `${rules.fieldName} must be at least ${rules.minLength} characters`;
  }
  
  if (rules.maxLength && value.length > rules.maxLength) {
    return `${rules.fieldName} must be less than ${rules.maxLength} characters`;
  }
  
  if (rules.pattern && !rules.pattern.test(value)) {
    return rules.patternMessage || `${rules.fieldName} is invalid`;
  }
  
  if (rules.email && !EMAIL_REGEX.test(value)) {
    return 'Please enter a valid email address';
  }
  
  return undefined;
};

// USAGE:
const [email, setEmail] = useState('');
const [emailError, setEmailError] = useState();

const handleEmailChange = (text: string) => {
  setEmail(text);
  const error = validateInput(text, {
    fieldName: 'Email',
    required: true,
    email: true,
  });
  setEmailError(error);
};

}
/>
```

### Step 4.3: List/Card Components
```typescript
// List Item Component (Platform Adaptive)
interface ListItemProps {
  title: string;
  subtitle?: string;
  description?: string;
  leftContent?: ReactNode; // Avatar, icon, checkbox
  rightContent?: ReactNode; // Chevron, switch, button
  onPress?: () => void;
  disabled?: boolean;
  selected?: boolean;
}

const ListItem: React.FC = ({
  title,
  subtitle,
  description,
  leftContent,
  rightContent,
  onPress,
  disabled = false,
  selected = false,
}) => {
  const isIOS = Platform.OS === 'ios';
  
  // Calculate height based on content
  const getHeight = () => {
    if (description) return 88; // Three-line
    if (subtitle) return 72;    // Two-line
    return 56;                   // One-line
  };
  
  return (
    
      {/* Left Content (Avatar/Icon/Checkbox) */}
      {leftContent && (
        
          {leftContent}
        
      )}
      
      {/* Main Content */}
      
        
          {title}
        
        
        {subtitle && (
          
            {subtitle}
          
        )}
        
        {description && (
          
            {description}
          
        )}
      
      
      {/* Right Content (Chevron/Switch/Button) */}
      {rightContent && (
        
          {rightContent}
        
      )}
    
  );
};

const styles = StyleSheet.create({
  listItem: {
    flexDirection: 'row',
    alignItems: 'center',
    paddingHorizontal: SPACING[4],
    paddingVertical: SPACING[3],
    backgroundColor: COLORS.light.surface,
    borderBottomWidth: StyleSheet.hairlineWidth,
    borderBottomColor: COLORS.light.divider,
  },
  listItemSelected: {
    backgroundColor: COLORS.light.focus,
  },
  listItemDisabled: {
    opacity: 0.5,
  },
  leftContent: {
    marginRight: SPACING[4],
  },
  mainContent: {
    flex: 1,
    justifyContent: 'center',
  },
  rightContent: {
    marginLeft: SPACING[3],
  },
  title: {
    fontSize: TYPOGRAPHY.ios.body.size,
    fontWeight: '400',
    color: COLORS.light.textPrimary,
    marginBottom: SPACING[1],
  },
  subtitle: {
    fontSize: TYPOGRAPHY.ios.subheadline.size,
    color: COLORS.light.textSecondary,
    marginBottom: SPACING[1],
  },
  description: {
    fontSize: TYPOGRAPHY.ios.footnote.size,
    color: COLORS.light.textTertiary,
    lineHeight: TYPOGRAPHY.ios.footnote.lineHeight,
  },
});

// COMMON LIST ITEM VARIANTS:

// 1. Simple text list item
}
  onPress={() => navigate('Settings')}
/>

// 2. Avatar + title + subtitle
}
  title={user.name}
  subtitle={user.email}
  rightContent={}
  onPress={() => navigate('Profile', { userId: user.id })}
/>

// 3. Icon + title + description
}
  title="Privacy"
  description="Control who can see your information"
  rightContent={}
  onPress={() => navigate('Privacy')}
/>

// 4. Switch control
}
  title="Notifications"
  subtitle="Receive push notifications"
  rightContent={
    
  }
/>

// 5. Selectable (with checkbox)
<ListItem
  leftContent={
    <Checkbox
      checked={isSelected}
      onPress={() => toggleSelection(item.id)}
    />
  }
  title={item.title}
  subtitle={item.subtitle}
  selected={isSelected}
  onPress={() => toggleSelection(item.id)}
/>
```

---

## Phase 5: Screen State Management

### Step 5.1: The Five States of Every Screen

**MANDATORY: Every screen must handle ALL five states**
```typescript
type ScreenState = 
  | 'loading'    // Initial data fetch
  | 'error'      // Failed to load
  | 'empty'      // No data to show
  | 'partial'    // Some data, more loading
  | 'success';   // Data loaded successfully

// State Management Hook
function useScreenState(
  fetchData: () => Promise,
  options?: {
    retryLimit?: number;
    cacheKey?: string;
  }
) {
  const [state, setState] = useState('loading');
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);
  const [retryCount, setRetryCount] = useState(0);
  
  const loadData = async () => {
    try {
      setState('loading');
      setError(null);
      
      const result = await fetchData();
      
      if (isEmpty(result)) {
        setState('empty');
      } else {
        setState('success');
        setData(result);
      }
    } catch (err) {
      setError(err as Error);
      setState('error');
    }
  };
  
  const retry = () => {
    if (options?.retryLimit && retryCount >= options.retryLimit) {
      return;
    }
    setRetryCount(prev => prev + 1);
    loadData();
  };
  
  useEffect(() => {
    loadData();
  }, []);
  
  return { state, data, error, retry, reload: loadData };
}

// Screen Template
const MyScreen = () => {
  const { state, data, error, retry } = useScreenState(() => fetchMyData());
  
  // Loading State
  if (state === 'loading') {
    return ;
  }
  
  // Error State
  if (state === 'error') {
    return (
      <ErrorState
        error={error}
        onRetry={retry}
        onGoBack={() => navigation.goBack()}
      />
    );
  }
  
  // Empty State
  if (state === 'empty') {
    return (
      <EmptyState
        title="No items yet"
        description="Start adding items to see them here"
        action={{
          label: 'Add Item',
          onPress: () => navigation.navigate('AddItem'),
        }}
      />
    );
  }
  
  // Success State
  return (
    
  );
};
```

### Step 5.2: Loading State Patterns
```typescript
// Pattern 1: Skeleton Loading (Preferred)
const SkeletonLoader = () => (
  
    {[1, 2, 3, 4, 5].map(i => (
      
        
        
          
          
        
      
    ))}
  
);

const SkeletonCircle = ({ size }: { size: number }) => (
  <View 
    style={[
      styles.skeleton,
      { width: size, height: size, borderRadius: size / 2 }
    ]} 
  />
);

const SkeletonLine = ({ 
  width, 
  height, 
  marginTop = 0 
}: { 
  width: string | number;
  height: number;
  marginTop?: number;
}) => (
  <View 
    style={[
      styles.skeleton,
      { 
        width: typeof width === 'string' ? width : width,
        height,
        borderRadius: RADIUS.sm,
        marginTop,
      }
    ]} 
  />
);

const styles = StyleSheet.create({
  skeleton: {
    backgroundColor: COLORS.light.backgroundSecondary,
    overflow: 'hidden',
  },
  skeletonRow: {
    flexDirection: 'row',
    padding: SPACING[4],
    gap: SPACING[3],
  },
  skeletonContent: {
    flex: 1,
  },
});

// Add shimmer animation
import { useSharedValue, useAnimatedStyle, withRepeat, withTiming } from 'react-native-reanimated';

const SkeletonShimmer = ({ children }: { children: ReactNode }) => {
  const shimmerTranslate = useSharedValue(-1);
  
  useEffect(() => {
    shimmerTranslate.value = withRepeat(
      withTiming(1, { duration: 1500 }),
      -1,
      false
    );
  }, []);
  
  const animatedStyle = useAnimatedStyle(() => ({
    transform: [
      { 
        translateX: shimmerTranslate.value * 400 
      }
    ],
  }));
  
  return (
    
      {children}
      
    
  );
};

// Pattern 2: Spinner Loading (Use sparingly)
const SpinnerLoader = ({ size = 'large' }: { size?: 'small' | 'large' }) => (
  
    
    Loading...
  
);

// Pattern 3: Pull to Refresh (Lists)
const ListWithRefresh = ({ data, onRefresh }: ListProps) => {
  const [refreshing, setRefreshing] = useState(false);
  
  const handleRefresh = async () => {
    setRefreshing(true);
    await onRefresh();
    setRefreshing(false);
  };
  
  return (
    
      }
    />
  );
};

// USAGE RULES:
// - Use skeleton for list/grid loading (shows structure)
// - Use spinner for full-screen initial load
// - Never show blank screen without indication
// - Provide cancel option for long operations
// - Show progress percentage for uploads/downloads
```

### Step 5.3: Error State Patterns
```typescript
// Comprehensive Error State Component
interface ErrorStateProps {
  error: Error;
  errorType?: 'network' | 'auth' | 'notFound' | 'server' | 'unknown';
  onRetry?: () => void;
  onGoBack?: () => void;
  onContactSupport?: () => void;
}

const ErrorState: React.FC = ({
  error,
  errorType = 'unknown',
  onRetry,
  onGoBack,
  onContactSupport,
}) => {
  // Auto-detect error type
  const detectedType = errorType || detectErrorType(error);
  
  // Get error content based on type
  const errorContent = getErrorContent(detectedType);
  
  return (
    
      
        {errorContent.icon}
      
      
      
        {errorContent.title}
      
      
      
        {errorContent.message}
      
      
      
        {onRetry && (
          }
          >
            Try Again
          
        )}
        
        {onGoBack && (
          
            Go Back
          
        )}
        
        {onContactSupport && (
          
            Contact Support
          
        )}
      
      
      {__DEV__ && (
        
          
            {error.message}
          
        
      )}
    
  );
};

// Error type detection
function detectErrorType(error: Error): ErrorStateProps['errorType'] {
  const message = error.message.toLowerCase();
  
  if (message.includes('network') || message.includes('timeout')) {
    return 'network';
  }
  if (message.includes('401') || message.includes('403')) {
    return 'auth';
  }
  if (message.includes('404')) {
    return 'notFound';
  }
  if (message.includes('500') || message.includes('502')) {
    return 'server';
  }
  
  return 'unknown';
}

// Error content configuration
function getErrorContent(type: ErrorStateProps['errorType']) {
  const content = {
    network: {
      icon: ,
      title: 'No Internet Connection',
      message: 'Please check your connection and try again.',
    },
    auth: {
      icon: ,
      title: 'Authentication Required',
      message: 'Please sign in to continue.',
    },
    notFound: {
      icon: ,
      title: 'Not Found',
      message: 'The item you\'re looking for doesn\'t exist.',
    },
    server: {
      icon: ,
      title: 'Server Error',
      message: 'Something went wrong on our end. Please try again later.',
    },
    unknown: {
      icon: ,
      title: 'Something Went Wrong',
      message: 'An unexpected error occurred. Please try again.',
    },
  };
  
  return content[type];
}

// USAGE:
<ErrorState
  error={error}
  onRetry={() => refetch()}
  onGoBack={() => navigation.goBack()}
  onContactSupport={() => Linking.openURL('mailto:support@example.com')}
/>
```

### Step 5.4: Empty State Patterns
```typescript
// Empty State Component
interface EmptyStateProps {
  title: string;
  description: string;
  illustration?: ReactNode;
  action?: {
    label: string;
    onPress: () => void;
    icon?: ReactNode;
  };
  secondaryAction?: {
    label: string;
    onPress: () => void;
  };
}

const EmptyState: React.FC = ({
  title,
  description,
  illustration,
  action,
  secondaryAction,
}) => {
  return (
    
      {illustration && (
        
          {illustration}
        
      )}
      
      
        {title}
      
      
      
        {description}
      
      
      {action && (
        
          {action.label}
        
      )}
      
      {secondaryAction && (
        
          {secondaryAction.label}
        
      )}
    
  );
};

const styles = StyleSheet.create({
  emptyContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: SPACING[8],
  },
  illustration: {
    marginBottom: SPACING[8],
  },
  emptyTitle: {
    fontSize: TYPOGRAPHY.ios.title2.size,
    fontWeight: '700',
    color: COLORS.light.textPrimary,
    textAlign: 'center',
    marginBottom: SPACING[3],
  },
  emptyDescription: {
    fontSize: TYPOGRAPHY.ios.body.size,
    color: COLORS.light.textSecondary,
    textAlign: 'center',
    marginBottom: SPACING[8],
    maxWidth: 300,
  },
});

// CONTEXT-SPECIFIC EMPTY STATES:

// 1. Empty inbox
}
/>

// 2. Empty cart
}
  action={{
    label: 'Start Shopping',
    onPress: () => navigate('Shop'),
    icon: ,
  }}
/>

// 3. Empty search results
}
  action={{
    label: 'Clear Search',
    onPress: clearSearch,
  }}
/>

// 4. No internet (special case - show cached data if available)
}
  secondaryAction={{
    label: 'View Cached Content',
    onPress: showCachedData,
  }}
/>
```

---

## Phase 6: Gestures & Interactions

### Step 6.1: Standard Gesture Library
```typescript
// Swipe-to-Delete (iOS Style)
import Swipeable from 'react-native-gesture-handler/Swipeable';

const SwipeableListItem = ({ 
  item, 
  onDelete, 
  onArchive 
}: SwipeableItemProps) => {
  const swipeableRef = useRef(null);
  
  // Left swipe actions (archive)
  const renderLeftActions = (progress, dragX) => {
    const scale = dragX.interpolate({
      inputRange: [0, 80],
      outputRange: [0, 1],
      extrapolate: 'clamp',
    });
    
    return (
      <TouchableOpacity
        onPress={() => {
          swipeableRef.current?.close();
          HapticFeedback.notification('success');
          onArchive(item.id);
        }}
        style={styles.leftAction}
      >
        
          
        
      
    );
  };
  
  // Right swipe actions (delete)
  const renderRightActions = (progress, dragX) => {
    const scale = dragX.interpolate({
      inputRange: [-80, 0],
      outputRange: [1, 0],
      extrapolate: 'clamp',
    });
    
    return (
      <TouchableOpacity
        onPress={() => {
          swipeableRef.current?.close();
          HapticFeedback.notification('warning');
          confirmDelete(item.id);
        }}
        style={styles.rightAction}
      >
        
          
        
      
    );
  };
  
  const confirmDelete = (id: string) => {
    Alert.alert(
      'Delete Item',
      'Are you sure you want to delete this item?',
      [
        { text: 'Cancel', style: 'cancel' },
        { 
          text: 'Delete', 
          style: 'destructive',
          onPress: () => onDelete(id),
        },
      ]
    );
  };
  
  return (
    
      
    
  );
};

const styles = StyleSheet.create({
  leftAction: {
    backgroundColor: COLORS.light.primary,
    justifyContent: 'center',
    alignItems: 'flex-end',
    paddingHorizontal: SPACING[6],
    flex: 1,
  },
  rightAction: {
    backgroundColor: COLORS.light.error,
    justifyContent: 'center',
    alignItems: 'flex-start',
    paddingHorizontal: SPACING[6],
    flex: 1,
  },
});

// GESTURE RULES:
// - Swipe left: Primary destructive action (delete)
// - Swipe right: Secondary action (archive, mark read)
// - Swipe 30%: Show action
// - Swipe 60%: Trigger action on release
// - Always confirm destructive actions
// - Provide haptic feedback
// - Animate smoothly (spring physics)
```

### Step 6.2: Long Press Menu
```typescript
import * as Haptics from 'expo-haptics';
import { ContextMenu } from 'react-native-context-menu-view';

// iOS-style context menu
const ContextMenuExample = ({ item }: { item: Item }) => {
  const handleAction = async (action: string) => {
    await Haptics.selectionAsync();
    
    switch (action) {
      case 'share':
        shareItem(item);
        break;
      case 'edit':
        navigateToEdit(item);
        break;
      case 'delete':
        confirmDelete(item);
        break;
    }
  };
  
  return (
    <ContextMenu
      actions={[
        { 
          title: 'Share', 
          systemIcon: 'square.and.arrow.up',
          action: 'share'
        },
        { 
          title: 'Edit', 
          systemIcon: 'pencil',
          action: 'edit'
        },
        { 
          title: 'Delete', 
          systemIcon: 'trash',
          destructive: true,
          action: 'delete'
        },
      ]}
      onPress={(event) => {
        handleAction(event.nativeEvent.name);
      }}
      previewBackgroundColor="transparent"
    >
      
    
  );
};

// Android-style long press menu
const LongPressMenu = ({ item, children }: LongPressMenuProps) => {
  const [menuVisible, setMenuVisible] = useState(false);
  const [menuPosition, setMenuPosition] = useState({ x: 0, y: 0 });
  
  const handleLongPress = (event: GestureResponderEvent) => {
    Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Medium);
    
    const { pageX, pageY } = event.nativeEvent;
    setMenuPosition({ x: pageX, y: pageY });
    setMenuVisible(true);
  };
  
  return (
    <>
      
        {children}
      
      
      <Menu
        visible={menuVisible}
        onDismiss={() => setMenuVisible(false)}
        anchor={menuPosition}
      >
        <Menu.Item 
          onPress={() => shareItem(item)} 
          title="Share"
          leadingIcon="share-variant"
        />
        <Menu.Item 
          onPress={() => editItem(item)} 
          title="Edit"
          leadingIcon="pencil"
        />
        
        <Menu.Item 
          onPress={() => deleteItem(item)} 
          title="Delete"
          leadingIcon="delete"
          titleStyle={{ color: COLORS.light.error }}
        />
      
    </>
  );
};

// LONG PRESS RULES:
// - Delay: 500ms (iOS) / 600ms (Android)
// - Haptic feedback when menu appears
// - Show preview on iOS (blur background)
// - Show menu anchored to touch on Android
// - Dismiss on tap outside
// - Maximum 5-6 menu items
// - Group related actions
// - Destructive actions at bottom, red color
```

### Step 6.3: Pull to Refresh
```typescript
// Pull to Refresh Implementation
const PullToRefreshList = ({ 
  data, 
  onRefresh,
  renderItem 
}: PullToRefreshProps) => {
  const [refreshing, setRefreshing] = useState(false);
  
  const handleRefresh = async () => {
    setRefreshing(true);
    Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Light);
    
    try {
      await onRefresh();
      Haptics.notificationAsync(Haptics.NotificationFeedbackType.Success);
    } catch (error) {
      Haptics.notificationAsync(Haptics.NotificationFeedbackType.Error);
    } finally {
      setRefreshing(false);
    }
  };
  
  return (
    <FlatList
      data={data}
      renderItem={renderItem}
      refreshControl={
        <RefreshControl
          refreshing={refreshing}
          onRefresh={handleRefresh}
          tintColor={COLORS.light.primary}
          colors={[COLORS.light.primary]} // Android
          progressBackgroundColor={COLORS.light.surface} // Android
        />
      }
      // Performance optimizations
      removeClippedSubviews={true}
      maxToRenderPerBatch={10}
      updateCellsBatchingPeriod={50}
      initialNumToRender={10}
      windowSize={5}
    />
  );
};

// PULL TO REFRESH RULES:
// - Only on scrollable content (lists, feeds)
// - Haptic feedback when triggered
// - Success/error haptic on completion
// - Show timestamp of last refresh (optional)
// - Don't use for critical real-time data
// - Minimum 500ms before hiding (feels snappier)
```

---

## Phase 7: Animations & Transitions

### Step 7.1: Screen Transition Library
```typescript
import { createStackNavigator, CardStyleInterpolators } from '@react-navigation/stack';

const Stack = createStackNavigator();

// iOS-style navigation
const IOSNavigation = () => (
  
    
    <Stack.Screen 
      name="Detail" 
      component={DetailScreen}
      options={{
        // Custom transition for specific screen
        cardStyleInterpolator: CardStyleInterpolators.forHorizontalIOS,
      }}
    />
  
);

// Modal presentation (iOS)
const ModalStack = () => (
  
    <Stack.Screen 
      name="ModalContent" 
      component={ModalScreen}
      options={{
        headerShown: true,
        headerLeft: () => (
          <Button variant="ghost" onPress={() => navigation.goBack()}>
            Cancel
          
        ),
        headerRight: () => (
          
            Done
          
        ),
      }}
    />
  
);

// Android-style navigation (Material)
const AndroidNavigation = () => (
  <Stack.Navigator
    screenOptions={{
      headerShown: true,
      gestureEnabled: false, // Android doesn't use gestures for back
      cardStyleInterpolator: CardStyleInterpolators.forFadeFromBottomAndroid,
      headerStyle: {
        elevation: 0,
        backgroundColor: COLORS.light.surface,
      },
    }}
  >
    
    
  
);

// TRANSITION RULES:
// iOS:
// - Horizontal slide for navigation
// - Vertical slide for modals
// - Swipe from left edge to go back
// - Parallax effect (previous screen moves slightly)

// Android:
// - Fade + slight scale for navigation
// - Slide up for modals
// - System back button to go back
// - No parallax effect
```

### Step 7.2: Micro-interaction Animations
```typescript
import Animated, {
  useSharedValue,
  useAnimatedStyle,
  withSpring,
  withTiming,
  withSequence,
} from 'react-native-reanimated';

// Button Press Animation
const AnimatedButton = ({ children, onPress }: ButtonProps) => {
  const scale = useSharedValue(1);
  
  const animatedStyle = useAnimatedStyle(() => ({
    transform: [{ scale: scale.value }],
  }));
  
  const handlePressIn = () => {
    scale.value = withSpring(0.95, {
      damping: 10,
      stiffness: 100,
    });
  };
  
  const handlePressOut = () => {
    scale.value = withSpring(1, {
      damping: 10,
      stiffness: 100,
    });
  };
  
  return (
    
      
        {children}
      
    
  );
};

// Fade In Animation (for screen content)
const FadeIn = ({ children, delay = 0 }: FadeInProps) => {
  const opacity = useSharedValue(0);
  const translateY = useSharedValue(20);
  
  useEffect(() => {
    opacity.value = withDelay(
      delay,
      withTiming(1, { duration: 400 })
    );
    translateY.value = withDelay(
      delay,
      withSpring(0, { damping: 15 })
    );
  }, []);
  
  const animatedStyle = useAnimatedStyle(() => ({
    opacity: opacity.value,
    transform: [{ translateY: translateY.value }],
  }));
  
  return (
    
      {children}
    
  );
};

// Success Checkmark Animation
const SuccessCheckmark = () => {
  const scale = useSharedValue(0);
  const rotate = useSharedValue(0);
  
  useEffect(() => {
    scale.value = withSequence(
      withSpring(1.2, { damping: 8 }),
      withSpring(1, { damping: 10 })
    );
    rotate.value = withSequence(
      withTiming(10, { duration: 100 }),
      withTiming(-10, { duration: 100 }),
      withTiming(0, { duration: 100 })
    );
  }, []);
  
  const animatedStyle = useAnimatedStyle(() => ({
    transform: [
      { scale: scale.value },
      { rotate: `${rotate.value}deg` }
    ],
  }));
  
  return (
    
      
    
  );
};

// Loading Dots Animation
const LoadingDots = () => {
  const dot1 = useSharedValue(0);
  const dot2 = useSharedValue(0);
  const dot3 = useSharedValue(0);
  
  useEffect(() => {
    const animate = () => {
      dot1.value = withSequence(
        withTiming(-10, { duration: 300 }),
        withTiming(0, { duration: 300 })
      );
      
      setTimeout(() => {
        dot2.value = withSequence(
          withTiming(-10, { duration: 300 }),
          withTiming(0, { duration: 300 })
        );
      }, 100);
      
      setTimeout(() => {
        dot3.value = withSequence(
          withTiming(-10, { duration: 300 }),
          withTiming(0, { duration: 300 })
        );
      }, 200);
    };
    
    const interval = setInterval(animate, 1000);
    return () => clearInterval(interval);
  }, []);
  
  const dot1Style = useAnimatedStyle(() => ({
    transform: [{ translateY: dot1.value }],
  }));
  
  const dot2Style = useAnimatedStyle(() => ({
    transform: [{ translateY: dot2.value }],
  }));
  
  const dot3Style = useAnimatedStyle(() => ({
    transform: [{ translateY: dot3.value }],
  }));
  
  return (
    
      
      
      
    
  );
};

// ANIMATION RULES:
// - Duration: 150-300ms for UI interactions
// - Spring physics for natural feel
// - Easing: ease-out for entrances, ease-in for exits
// - Always provide haptic feedback with animations
// - Respect reduced motion accessibility setting
// - Keep animations subtle and purposeful
```

---

## Phase 8: Accessibility (Non-Negotiable)

### Step 8.1: Screen Reader Support
```typescript
// MANDATORY: Every interactive element needs proper labels

// ✅ GOOD: Full accessibility support

  


// ❌ BAD: No accessibility

  


// Complex component example
const ProductCard = ({ product }: ProductCardProps) => {
  return (
    <TouchableOpacity
      accessible={true}
      accessibilityLabel={`${product.name}, $${product.price}`}
      accessibilityHint="Double tap to view product details"
      accessibilityRole="button"
      onPress={() => navigate('Product', { id: product.id })}
    >
      
      
        {product.name}
      
      
        ${product.price}
      
    
  );
};

// Group related elements
const ProfileHeader = ({ user }: ProfileHeaderProps) => {
  return (
    
      
      {user.name}
      {user.title}
      {user.followers} followers
    
  );
};

// Announce dynamic changes
import { AccessibilityInfo } from 'react-native';

const handleDelete = async (id: string) => {
  await deleteItem(id);
  AccessibilityInfo.announceForAccessibility('Item deleted');
};

const handleError = (error: Error) => {
  setError(error.message);
  AccessibilityInfo.announceForAccessibility(
    `Error: ${error.message}`
  );
};

// ACCESSIBILITY RULES:
// - Every touchable element needs accessibilityLabel
// - Use accessibilityHint for complex actions
// - Set accessibilityRole appropriately
// - Group related content with accessible={true}
// - Mark decorative elements with accessible={false}
// - Announce important state changes
// - Test with VoiceOver (iOS) and TalkBack (Android)
```

### Step 8.2: Dynamic Type Support
```typescript
// Support system font scaling
import { useWindowDimensions, PixelRatio } from 'react-native';

const useScaledSize = (size: number): number => {
  const { fontScale } = useWindowDimensions();
  return PixelRatio.roundToNearestPixel(size * fontScale);
};

// Text component with scaling support
const ScalableText = ({ 
  style, 
  children,
  maxFontSizeMultiplier = 1.5, // Cap at 150%
  ...props 
}: TextProps) => {
  return (
    
      {children}
    
  );
};

// Layout that adapts to large text
const AdaptiveLayout = ({ title, body }: LayoutProps) => {
  const { fontScale } = useWindowDimensions();
  const isLargeText = fontScale > 1.3;
  
  return (
    
      
        {title}
      
      
        {body}
      
    
  );
};

const styles = StyleSheet.create({
  container: {
    padding: SPACING[4],
  },
  containerLargeText: {
    padding: SPACING[6], // More padding for large text
  },
  title: {
    fontSize: TYPOGRAPHY.ios.title1.size,
  },
  body: {
    fontSize: TYPOGRAPHY.ios.body.size,
  },
});

// DYNAMIC TYPE RULES:
// - Support up to 200% text scaling
// - Test at largest text size
// - Ensure layout doesn't break
// - Increase touch targets proportionally
// - Truncate or wrap long text appropriately
// - Don't disable font scaling without good reason
```

### Step 8.3: Color Contrast Validation
```typescript
// Automated contrast checking
const validateContrast = (
  foreground: string,
  background: string,
  fontSize: number
): boolean => {
  const ratio = calculateContrastRatio(foreground, background);
  
  // WCAG AA requirements
  const isLargeText = fontSize >= 18 || (fontSize >= 14 && isBold);
  const requiredRatio = isLargeText ? 3.0 : 4.5;
  
  if (ratio < requiredRatio) {
    console.warn(
      `Insufficient contrast: ${ratio.toFixed(2)}:1 ` +
      `(required: ${requiredRatio}:1) ` +
      `for ${foreground} on ${background}`
    );
    return false;
  }
  
  return true;
};

// Use in development
if (__DEV__) {
  validateContrast(
    COLORS.light.textSecondary,
    COLORS.light.background,
    TYPOGRAPHY.ios.body.size
  );
}

// Provide high contrast mode
const useHighContrast = () => {
  const { isHighContrastEnabled } = useAccessibilityInfo();
  
  return isHighContrastEnabled
    ? COLORS.highContrast
    : COLORS.light;
};

// CONTRAST RULES:
// - Minimum 4.5:1 for normal text
// - Minimum 3.0:1 for large text (18pt+)
// - Minimum 3.0:1 for UI components (borders, icons)
// - Provide high contrast mode option
// - Test in grayscale mode
```

---

## Phase 9: Performance Optimization

### Step 9.1: List Performance
```typescript
// High-performance list implementation
const OptimizedList = ({ data }: ListProps) => {
  // Memoize rendered items
  const renderItem = useCallback(({ item }: { item: Item }) => (
    
  ), []);
  
  const keyExtractor = useCallback((item: Item) => item.id, []);
  
  const getItemLayout = useCallback(
    (data, index) => ({
      length: ITEM_HEIGHT,
      offset: ITEM_HEIGHT * index,
      index,
    }),
    []
  );
  
  return (
    <FlatList
      data={data}
      renderItem={renderItem}
      keyExtractor={keyExtractor}
      getItemLayout={getItemLayout} // Enables instant scrolling
      
      // Performance optimizations
      removeClippedSubviews={true}
      maxToRenderPerBatch={10}
      updateCellsBatchingPeriod={50}
      initialNumToRender={10}
      windowSize={5}
      
      // Separators
      ItemSeparatorComponent={Separator}
      
      // Empty state
      ListEmptyComponent={EmptyState}
      
      // Infinite scroll
      onEndReached={loadMore}
      onEndReachedThreshold={0.5}
      ListFooterComponent={isLoadingMore ?  : null}
    />
  );
};

// Memoized list item
const MemoizedListItem = React.memo(
  ({ item }: { item: Item }) => (
    
  ),
  (prevProps, nextProps) => {
    // Custom comparison for optimal re-rendering
    return prevProps.item.id === nextProps.item.id &&
           prevProps.item.updatedAt === nextProps.item.updatedAt;
  }
);

// LIST PERFORMANCE RULES:
// - Use FlatList, not ScrollView with map
// - Memoize renderItem and keyExtractor
// - Provide getItemLayout if items are fixed height
// - Set removeClippedSubviews={true}
// - Limit initialNumToRender to 10-15 items
// - Use React.memo for list items
// - Avoid inline functions in renderItem
// - Paginate long lists (load more on scroll)
```

### Step 9.2: Image Optimization
```typescript
import FastImage from 'react-native-fast-image';

// Optimized image component
const OptimizedImage = ({
  source,
  width,
  height,
  resizeMode = 'cover',
  priority = 'normal',
}: ImageProps) => {
  return (
    <FastImage
      source={{
        uri: source,
        priority: FastImage.priority[priority],
        cache: FastImage.cacheControl.immutable,
      }}
      style={{ width, height }}
      resizeMode={FastImage.resizeMode[resizeMode]}
      
      // Placeholder while loading
      defaultSource={require('./placeholder.png')}
      
      // Loading indicator
      onLoadStart={() => setLoading(true)}
      onLoadEnd={() => setLoading(false)}
    />
  );
};

// Progressive image loading
const ProgressiveImage = ({ 
  thumbnailSource,
  source,
  ...props 
}: ProgressiveImageProps) => {
  const [imageLoaded, setImageLoaded] = useState(false);
  
  return (
    
      
      
        <FastImage
          source={source}
          onLoadEnd={() => setImageLoaded(true)}
          {...props}
        />
      
    
  );
};

// IMAGE OPTIMIZATION RULES:
// - Use FastImage for better caching
// - Provide @1x, @2x, @3x versions
// - Compress images (80% quality is fine)
// - Use WebP format when possible
// - Lazy load images off-screen
// - Resize images to display size on server
// - Show placeholder while loading
// - Use progressive loading for large images
// - Cache images appropriately
```

### Step 9.3: App Launch Optimization
```typescript
// Optimize app launch time

// 1. Splash screen strategy
import * as SplashScreen from 'expo-splash-screen';

// Keep splash screen visible while loading
SplashScreen.preventAutoHideAsync();

const App = () => {
  const [appIsReady, setAppIsReady] = useState(false);
  
  useEffect(() => {
    async function prepare() {
      try {
        // Load critical data
        await Promise.all([
          loadFonts(),
          loadUserData(),
          initializeAnalytics(),
        ]);
      } catch (e) {
        console.warn(e);
      } finally {
        setAppIsReady(true);
      }
    }
    
    prepare();
  }, []);
  
  const onLayoutRootView = useCallback(async () => {
    if (appIsReady) {
      await SplashScreen.hideAsync();
    }
  }, [appIsReady]);
  
  if (!appIsReady) {
    return null;
  }
  
  return (
    
      {/* App content */}
    
  );
};

// 2. Code splitting (lazy load screens)
const HomeScreen = lazy(() => import('./screens/HomeScreen'));
const ProfileScreen = lazy(() => import('./screens/ProfileScreen'));

// 3. Defer non-critical initialization
useEffect(() => {
  // Run after initial render
  setTimeout(() => {
    initializeNonCriticalServices();
  }, 1000);
}, []);

// LAUNCH OPTIMIZATION RULES:
// - Target < 2 second launch time
// - Load only critical data before first screen
// - Defer analytics, crash reporting, etc.
// - Use code splitting for large screens
// - Cache frequently accessed data
// - Optimize image assets
// - Minimize bundle size
```

---

## Phase 10: Quality Validation Checklist

### MANDATORY: Complete Before Delivery
```typescript
// Automated quality checks
interface QualityCheckResult {
  category: string;
  checks: QualityCheck[];
  passed: boolean;
}

interface QualityCheck {
  name: string;
  passed: boolean;
  severity: 'critical' | 'warning' | 'info';
  message?: string;
}

const runQualityChecks = (): QualityCheckResult[] => {
  return [
    // Visual Quality
    {
      category: 'Visual Quality',
      checks: [
        checkFontsLoaded(),
        checkColorContrast(),
        checkSpacingConsistency(),
        checkImageQuality(),
        checkResponsiveness(),
      ],
      passed: true,
    },
    
    // Functionality
    {
      category: 'Functionality',
      checks: [
        checkNavigation(),
        checkForms(),
        checkLoadingStates(),
        checkErrorHandling(),
        checkEmptyStates(),
      ],
      passed: true,
    },
    
    // Accessibility
    {
      category: 'Accessibility',
      checks: [
        checkAccessibilityLabels(),
        checkColorContrast(),
        checkTouchTargets(),
        checkKeyboardNavigation(),
        checkScreenReaderSupport(),
      ],
      passed: true,
    },
    
    // Performance
    {
      category: 'Performance',
      checks: [
        checkLaunchTime(),
        checkListPerformance(),
        checkImageOptimization(),
        checkBundleSize(),
        checkMemoryLeaks(),
      ],
      passed: true,
    },
    
    // Platform Compliance
    {
      category: 'Platform Compliance',
      checks: [
        checkPlatformGuidelines(),
        checkSafeAreas(),
        checkGestures(),
        checkNotifications(),
      ],
      passed: true,
    },
  ];
};
```

### Manual Testing Checklist

**Device Testing** (CRITICAL):
```
□ iPhone SE (smallest current iPhone) - 375 × 667
□ iPhone 14 Pro (Dynamic Island) - 393 × 852
□ iPhone 15 Pro Max (largest) - 430 × 932
□ Android phone (various ratios) - 360 × 800
□ Android tablet - 712 × 1138
□ Both orientations (portrait + landscape)
```

**Appearance Testing**:
```
□ Light mode
□ Dark mode
□ Largest text size (Settings → Accessibility → Larger Text)
□ Reduced motion (Settings → Accessibility → Reduce Motion)
□ High contrast mode
□ Grayscale mode (color blind testing)
```

**Functionality Testing**:
```
□ All user flows complete successfully
□ All forms validate correctly
□ All buttons trigger correct actions
□ All navigation works as expected
□ Deep links open correct screens
□ Share functionality works
□ Push notifications received
□ App badge updates correctly
```

**Edge Cases**:
```
□ No internet connection
□ Poor network (slow 3G)
□ App backgrounded mid-task
□ Phone call interruption
□ Low battery mode
□ Low storage warning
□ First-time user experience
□ User with no data
□ User with maximum data
```

**Accessibility Testing**:
```
□ VoiceOver (iOS) / TalkBack (Android) full app navigation
□ All interactive elements have labels
□ All images have alt text
□ All form inputs have labels
□ Color contrast meets WCAG AA
□ Focus indicators visible
□ No keyboard traps
```

**Performance Testing**:
□ App launches in < 2 seconds
□ Lists scroll at 60fps
□ No jank in animations
□ Images load progressively
□ No memory leaks
□ Battery usage reasonable
□ App size < 50MB (ideal)

---

## Remember

**Mobile apps are intimate. They live in your user's pocket, accompany them throughout their day, and become part of their routine. This demands a level of quality, polish, and thoughtfulness that exceeds other mediums.**

Every tap matters. Every transition matters. Every state matters. Every pixel matters.

The difference between a good app and a great app isn't features—it's the care taken in every detail. The smooth animation. The perfect spacing. The helpful error message. The delightful empty state.

Design for the hand, not the mouse. Design for interruption, not attention. Design for glances, not stares. Design for people, not users.

Now build something exceptional. 📱✨