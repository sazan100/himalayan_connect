# Himalaya Chat - Privacy-First Messaging Platform

## Overview

Himalaya Chat is a privacy-focused messaging application with a unique Nepali Himalayan cultural theme. The platform combines end-to-end encrypted messaging with distinctive features like Prayer Flag messages, Yeti Mode (stealth privacy), and Summit Circles (temporary group chats). Built as a full-stack web application, it emphasizes zero-knowledge architecture where messages are stored in-memory only and automatically deleted, ensuring maximum privacy.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- React 18+ with TypeScript for type safety
- Vite as the build tool and development server
- Wouter for lightweight client-side routing
- TanStack Query for server state management and caching
- Framer Motion for animations and transitions

**UI Component System:**
- shadcn/ui component library with Radix UI primitives
- Tailwind CSS for styling with custom design tokens
- New York style variant from shadcn/ui
- Custom theme system supporting light/dark modes via context
- Responsive design with mobile-first approach (breakpoint at 768px)

**Design Philosophy:**
- Hybrid of Telegram's clean interface and WhatsApp's conversation patterns
- Himalayan visual language (mountain backgrounds, prayer flag colors, cultural elements)
- Typography: Inter for UI, Playfair Display for accents, JetBrains Mono for technical content
- Color scheme includes prayer flag colors (blue, white, red, green, yellow) integrated into the design system

**State Management:**
- AuthContext for user authentication state
- ThemeContext for light/dark mode preferences
- WebSocketContext for real-time communication state
- Local component state using React hooks
- TanStack Query for server data caching

### Backend Architecture

**Server Framework:**
- Express.js application serving both API and static assets
- HTTP server wrapped with WebSocket support (ws library)
- Custom logging middleware for request monitoring
- JSON body parsing with raw body buffer access for webhooks

**API Design:**
- RESTful endpoints registered via `registerRoutes` function
- WebSocket connection at `/ws` path for real-time features
- Session-based authentication (preparation for passport integration)
- Error handling with structured JSON responses

**Data Flow:**
- In-memory storage implementation (MemStorage class)
- No persistent database for messages (privacy by design)
- Users stored with minimal credentials only
- Stories auto-expire after 24 hours
- Summit Circles expire based on configured duration
- Automatic cleanup intervals for expired content

**Real-Time Communication:**
- WebSocket connections managed per authenticated user
- Message broadcasting to specific users or all connected clients
- Presence system tracking online/offline/away/busy status
- Typing indicators with conversation-scoped events
- Screenshot detection alerts sent via WebSocket
- Reaction and read receipt synchronization

### Data Storage Solutions

**In-Memory Storage Strategy:**
- `MemStorage` class implementing `IStorage` interface
- Maps used for fast key-based lookups:
  - Users: `Map<string, User>`
  - Messages: `Map<string, Message[]>` (by conversation ID)
  - Stories: `Map<string, Story>`
  - Groups: `Map<string, Group>`
  - Summit Circles: `Map<string, SummitCircle>`

**Data Models:**
- User: ID, username, hashed password, display name, avatar, status, yetiMode flag, lastSeen
- Message: ID, sender/receiver IDs, content, type (text/image/video/voice/prayerFlag), encryption flag, timestamp, expiration, readBy array, reactions, replyTo reference
- Story: ID, user ID, content, type, timestamp, 24hr expiration, viewedBy array
- Group: ID, name, participants array, admin, creation timestamp
- Summit Circle: ID, name, participants, duration-based expiration, creation timestamp

**Privacy Features:**
- Messages stored only in-memory, never persisted to disk
- Optional message expiration (disappearing messages)
- Encryption flag on all messages (client-side encryption ready)
- Screenshot detection with alerts to other participants
- Yeti Mode for enhanced privacy visibility

### Authentication and Authorization

**Current Implementation:**
- Username/password authentication stored in-memory
- User registration creates new user entries
- Login returns user object, stored in localStorage on client
- Session management prepared (connect-pg-simple imported for future use)

**Security Considerations:**
- Passwords should be hashed (bcrypt/argon2 integration needed)
- Session-based auth with HTTP-only cookies (prepared but not active)
- CORS configuration for cross-origin requests
- Rate limiting prepared (express-rate-limit imported)
- Client-side encryption utilities (`encryption.ts`) using Web Crypto API

### External Dependencies

**Database Preparation:**
- Drizzle ORM configured with PostgreSQL dialect
- Schema defined in `shared/schema.ts` using Zod for validation
- Migration system configured (output to `./migrations`)
- Database currently not provisioned (environment variable `DATABASE_URL` required)
- Storage can be migrated from in-memory to PostgreSQL by implementing database-backed storage

**UI Component Libraries:**
- Radix UI primitives for accessible components (accordion, alert-dialog, avatar, checkbox, dialog, dropdown-menu, hover-card, label, menubar, navigation-menu, popover, progress, radio-group, scroll-area, select, separator, slider, switch, tabs, toast, toggle, tooltip)
- shadcn/ui component patterns and styling conventions
- Embla Carousel for image/story galleries
- cmdk for command palette functionality

**Form Management:**
- React Hook Form for form state
- Zod for schema validation
- @hookform/resolvers for Zod integration

**Development Tools:**
- Replit-specific plugins (@replit/vite-plugin-runtime-error-modal, cartographer, dev-banner)
- TypeScript for type checking
- ESBuild for server bundling in production
- Vite HMR for hot module replacement in development

**Potential Future Integrations:**
- Stripe for payments (imported but not implemented)
- Nodemailer for email notifications (imported but not implemented)
- OpenAI/Google Generative AI for AI features (imported but not implemented)
- Multer for file uploads (imported but not implemented)
- JWT for token-based auth alternative (imported but not implemented)

**Build and Deployment:**
- Development: tsx running TypeScript server directly with Vite middleware
- Production: Client built with Vite to `dist/public`, server bundled with ESBuild to `dist/index.cjs`
- Static file serving from built client directory
- SPA fallback to `index.html` for client-side routing

**Asset Management:**
- Path aliases configured: `@/` for client/src, `@shared/` for shared, `@assets/` for attached_assets
- Fonts loaded from Google Fonts CDN (Inter, Playfair Display, JetBrains Mono)
- SVG mountain backgrounds rendered inline for performance
- favicon.png served from public directory