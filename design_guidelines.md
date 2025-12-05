# Design Guidelines: Himalayan Privacy Messenger

## Design Approach

**Hybrid Reference + Custom System**: Drawing from Telegram's clean interface architecture and WhatsApp's conversation patterns, enhanced with custom Himalayan visual language. The design balances messaging app conventions (immediate usability) with distinctive cultural aesthetics (brand differentiation).

**Core Principle**: Privacy through visual simplicity - minimal chrome, maximum content focus, with Nepali Himalayan elements integrated subtly to avoid overwhelming the functional UI.

## Typography

**Font Stack**:
- Primary: Inter or System UI (messages, UI elements) - crisp, highly legible for chat
- Accent: Playfair Display or Libre Baskerville (headers, special features) - adds cultural sophistication
- Monospace: JetBrains Mono (encryption keys, technical info)

**Hierarchy**:
- Chat messages: 15-16px, regular weight
- Usernames: 14px, semibold
- Timestamps: 12px, light
- Headers: 24-28px, bold
- Feature titles (Prayer Flags, Yeti Mode): 18-20px, medium

## Layout System

**Spacing Primitives**: Tailwind units of 1, 2, 3, 4, 6, 8, 12, 16
- Tight spacing (p-1, p-2): Message bubbles, compact UI
- Standard (p-4, p-6): Chat containers, modals
- Generous (p-8, p-12): Feature sections, onboarding

**Grid Structure**:
- Sidebar: Fixed 280px (desktop), full-width drawer (mobile)
- Main chat: flex-1 with max-width constraint
- Right panel (stories/media): 320px collapsible

## Component Library

### Navigation
- **Left Sidebar**: Vertical chat list with search, user avatar at top, feature shortcuts at bottom (Yeti Mode toggle, Summit Circles, Settings)
- **Top Bar**: Conversation header with participant name, status indicator, action buttons (call, video, info)
- **Bottom Navigation (Mobile)**: Chats, Stories, Summit Circles, Profile (4 tabs)

### Chat Components
- **Message Bubbles**: Rounded corners (rounded-2xl for sent, rounded-tl-sm for received), shadow-sm, max-width 70%, timestamp inside bubble
- **Media Messages**: Full-bleed within bubble, rounded corners, loading skeleton
- **Voice Notes**: Waveform visualization, play button, duration, rounded-full container
- **Reactions**: Small emoji row below message, hover to add more
- **Typing Indicator**: Three animated dots, subtle pulse

### Unique Feature Components
- **Prayer Flag Messages**: Cascading card layout with string connection visual, colorful flag-shaped containers
- **Yeti Mode Toggle**: Prominent switch with mountain icon, subtle snowflake animation when active
- **Summit Circles**: Circular timer visual showing expiration, participant avatars in circle formation
- **Screenshot Alert**: Modal with mountain warning icon, traditional pattern border

### Stories
- **Story Ring**: Gradient circular progress indicator (prayer flag colors), avatar in center
- **Story Viewer**: Full-screen with bottom sheet for reactions, swipe gestures
- **Story Grid**: 3-column on desktop, 2-column on tablet, horizontal scroll on mobile

### Forms & Inputs
- **Message Input**: Rounded-full container, attachment icon, emoji picker, send button (paper plane icon)
- **Search**: Rounded-lg with icon, instant filter results
- **Settings Forms**: Clean vertical layout, toggle switches, grouped sections with dividers

### Modals & Overlays
- **Profile Modal**: Centered card with subtle mountain silhouette background, user info, privacy status
- **Media Viewer**: Full-screen black backdrop, image/video centered, close button top-right
- **Encryption Key Display**: Monospace code block, copy button, visual verification icon

## Himalayan Theme Integration

**Visual Motifs** (used sparingly):
- Mountain silhouettes as subtle background elements in empty states
- Prayer flag color accents (blue, white, red, green, yellow) for feature highlights
- Traditional Nepali pattern borders for special messages or celebrations
- Mandala-inspired loading spinners
- Snow particle effects for Yeti Mode activation

**Cultural Elements**:
- Namaste gesture icon for greetings/welcome screens
- Himalayan peak icons for achievement badges (message milestones)
- Prayer wheel animation for loading states in spiritual contexts
- Traditional architecture-inspired card corners (slight upturned edges)

## Animations

**Minimal & Purposeful**:
- Message send: Subtle slide-up with fade (150ms)
- Story transition: Smooth crossfade (300ms)
- Yeti Mode activation: Gentle fade with snow particle burst (500ms)
- Prayer Flag cascade: Staggered slide-in (100ms delay between flags)
- No scroll animations, no parallax

## Images

**Hero/Onboarding**: Large hero image of Himalayan mountain range (Everest/Annapurna) with gradient overlay for text readability - used on login/welcome screen only

**In-App Images**:
- Empty state illustrations: Minimalist line-art mountains with yak/prayer flags
- Profile backgrounds: Optional user-uploaded images with Himalayan defaults
- Story content: User-generated photos/videos
- Feature banners: Small accent images for Prayer Flags, Summit Circles introductions

## Accessibility

- Consistent focus states: 2px outline with offset
- Touch targets: Minimum 44x44px for all interactive elements
- Color contrast: 4.5:1 minimum for text
- Alt text for all images and icons
- Keyboard navigation throughout
- Screen reader labels for icon-only buttons

## Responsive Behavior

**Desktop (1024px+)**: Three-column layout (sidebar, chat, right panel)
**Tablet (768-1023px)**: Two-column (sidebar collapsible, right panel overlay)
**Mobile (<768px)**: Single column, bottom tab navigation, drawers for secondary panels

Critical: Chat interface must feel native and familiar while Himalayan theme adds warmth and cultural identity without compromising messaging efficiency.