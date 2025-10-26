# Idle Empire - Design Guidelines

## Design Approach

**Reference-Based Strategy**: Draw inspiration from modern idle/clicker games (Cookie Clicker, Adventure Capitalist) combined with contemporary gaming UI aesthetics. The design should feel immersive and rewarding while maintaining clean information hierarchy for stats and progression tracking.

**Core Principles**:
- Instant visual feedback for all player actions
- Clear stat hierarchy emphasizing gold and progression
- Atmospheric depth without cluttering gameplay
- Premium feel that justifies in-app purchases

---

## Typography

**Font Stack**: Inter (already implemented) - maintains excellent readability for numbers and stats

**Hierarchy**:
- **Hero Numbers** (Gold counter, main stats): 32-40px, weight 800, tight letter-spacing (0.5px)
- **Section Headers**: 20-24px, weight 600
- **Body Stats/Labels**: 14-16px, weight 400-600
- **Micro Labels** (item counts, timestamps): 12-13px, weight 400

**Number Treatment**: All numeric displays should use tabular numbers (font-variant-numeric: tabular-nums) for stable width during updates

---

## Layout System

**Spacing Primitives**: Use Tailwind units of **2, 4, 6, 8, 12, 16, 20** for consistent rhythm
- Micro spacing (gaps, padding): 2-4 units
- Component internal spacing: 6-8 units  
- Section spacing: 12-16 units
- Major layout gaps: 20 units

**Grid Structure**:
- Desktop: Two-column layout (main stats/actions | shop sidebar)
- Sidebar width: 360-400px fixed
- Main content: Flexible with max-width constraint
- Mobile: Stack vertically, shop becomes full-width accordion

**Container Strategy**:
- Max width: 1100-1200px
- Padding: 12px mobile, 16-20px desktop
- Cards use consistent 12-16px internal padding

---

## Component Library

### Card System
**Primary Cards**: Stats, Shop, Action Area
- Glass morphism effect with subtle backdrop blur
- Multi-layer background: gradient overlay on semi-transparent base
- Thin border (1px) with low-opacity light color for definition
- Border-radius: 12-16px for modern feel
- Shadow: Multi-layer (0 4px 12px, 0 8px 24px) with varying opacity

**Nested Cards**: Shop items, upgrade rows
- Lighter glass effect than primary cards
- Border-radius: 8px
- Minimal shadow to avoid depth confusion

### Button Hierarchy

**Primary Action** (Mine button):
- Large size: 18-20px font, 16-20px padding
- Gradient background (avoid specific colors per constraint)
- Strong shadow with hover lift effect
- Active state: Scale transform (0.98)
- Disabled state: Reduced opacity (0.5-0.6) with grayscale filter

**Secondary Actions** (Shop buy buttons):
- Medium size: 14-16px font, 10-12px padding
- Solid or gradient background
- Border-radius: 8px
- Hover: Slight scale (1.02) or brightness increase

**Tertiary Actions** (Save, Export, Auth):
- Small size: 14px font, 8-10px padding
- Minimal background or transparent with border
- Border-radius: 6-8px

### Modal System
**Overlay**: Full-screen with gradient backdrop (dark with high opacity 0.85-0.92)
**Modal Card**: 360-400px width, center-aligned
- Inherits primary card styling
- Close button: Top-right absolute position
- Form inputs: Full-width with 8-10px padding

### Stats Display
**Big Numbers**: Extra large font (32-40px), bold weight (800)
- Gold counter gets special treatment as primary metric
- Use smooth number animation (easeOutCubic) when values update

**Secondary Stats** (GPS, levels):
- Label + Value inline pairs
- Clear visual separation between label and number
- Consistent vertical spacing (6-8px between stat rows)

### Shop Interface
**Tab Navigation**: 
- Horizontal tabs above shop content
- Active state: Background fill + accent treatment
- Inactive state: Transparent with muted text

**Shop Items**:
- Horizontal layout: Icon/Name left, Cost/Button right
- Two-line info: Title bold, ownership count below in smaller text
- Buy button aligned right
- Cost display adjacent to button
- Disabled items: Reduce opacity, show "Not enough gold" state

**Scrollable Container**: Max-height constraint (500-550px) with custom scrollbar styling

### Floating Feedback
**Gold Pop-ups**: 
- Absolute positioned within action area
- Gradient background matching reward theme
- Float-up animation (80-100px travel, 1.2s duration)
- Fade out with slight scale reduction
- Random horizontal offset for variety (-40px to +40px)

**Visual Sparkles**: Occasional decorative particles during autoclick ticks

---

## Animation Strategy

**Minimal & Purposeful**: Given glitch concerns, use animations sparingly and with clear purpose

**Approved Animations**:
1. **Number counters**: Smooth easing (600ms easeOutCubic)
2. **Floating gold**: Single-use, self-removing (1.2s)
3. **Button press**: Quick scale pulse (300-500ms)
4. **Hover states**: Subtle lift/scale (150-200ms)

**Forbidden**:
- Infinite loops on static elements
- Overlapping animations on same element
- Background animations or particles
- Page transitions

**Implementation Rules**:
- Always remove animation classes after completion
- Use `transform` and `opacity` only (GPU accelerated)
- Include `will-change` hints sparingly
- Debounce rapid interactions (mine button)

---

## Game-Specific Elements

### Activity Log
- Fixed height container (160-180px) with scroll
- Timestamp + message format
- Newest entries at top (prepend)
- Monospace timestamp for alignment
- Subtle background for each log entry

### Premium Shop
- Distinct visual treatment from regular shop
- Show real-world price prominently
- Gold reward amount highlighted
- "Best Value" badges for higher tiers
- Confirmation modal before fake purchase

### Progress Indicators
- Subtle progress bars for upgrades if applicable
- Visual milestone markers
- Achievement-style notifications for major thresholds

---

## Accessibility & States

**Loading States**: Spinner or skeleton for async operations (auth, save)
**Error States**: Inline error messages in modals (red accent)
**Empty States**: Friendly messaging when no items owned
**Disabled States**: Consistent 0.5-0.6 opacity + cursor not-allowed

**Focus Management**:
- Visible focus rings on interactive elements
- Tab order follows logical flow
- Modal traps focus when open

---

## Responsive Breakpoints

- **Mobile** (<768px): Single column, larger touch targets (min 44px)
- **Tablet** (768-1024px): Maintain two-column with adjusted sidebar
- **Desktop** (>1024px): Full layout with optimal spacing

**Mobile Optimizations**:
- Stack shop below actions
- Larger font sizes for primary stats (+2-4px)
- Increased padding for touch comfort
- Simplified animations (reduce motion)

---

## Images

**Not applicable** - This is a game UI with generated content, no hero images or photography needed. All visual interest comes from UI treatment, typography, and subtle effects.