# Alfred System - Personal Command Center

## Project Overview
- **Project name**: Alfred System
- **Type**: Single-page web application (personal productivity tool)
- **Core functionality**: Agile/SCRUM-based goal management system with AI chat integration and visual kanban board
- **Target users**: Entrepreneurs, founders, and high-performers who want extreme excellence in their personal organization

---

## UI/UX Specification

### Layout Structure

**Page Sections:**
1. **Sidebar (left)** - Navigation + Quick actions + Chat toggle
2. **Main Content Area** - Kanban board / Goal views
3. **Chat Panel (right)** - Collapsible AI assistant panel

**Grid Layout:**
- Sidebar: 280px fixed width
- Main: Fluid (calc(100% - 280px - chatWidth))
- Chat Panel: 380px (collapsible)

**Responsive Breakpoints:**
- Desktop: > 1200px (full layout)
- Tablet: 768px - 1200px (collapsed sidebar icons, hidden chat)
- Mobile: < 768px (hamburger menu, stacked views)

### Visual Design - "Liquid Platinum" Theme

**Aesthetic Direction:**
Inspired by Bruce Wayne's refined elegance + Apple's liquid glass + luxury automotive interiors. Dark, sophisticated, premium.

**Color Palette:**
```css
--bg-primary: #0a0a0c;          /* Near black with blue undertone */
--bg-secondary: #121218;       /* Card backgrounds */
--bg-tertiary: #1a1a24;        /* Elevated surfaces */
--glass-bg: rgba(255,255,255,0.03); /* Liquid glass effect */
--glass-border: rgba(255,255,255,0.08);

--accent-platinum: #c0c0c8;     /* Primary accent - platinum */
--accent-gold: #d4af37;         /* Success/progress gold */
--accent-copper: #b87333;      /* Warning/attention */
--accent-ice: #a8d8ea;         /* Info/cool tones */

--text-primary: #f5f5f7;       /* Primary text */
--text-secondary: #8a8a9a;     /* Secondary/muted text */
--text-tertiary: #5a5a6a;      /* Disabled/placeholder */

--kanban-todo: #2d2d3a;
--kanban-progress: #3d5a80;
--kanban-done: #1d3d2f;
```

**Typography:**
- **Display Font**: "Playfair Display" (headings, hero text) - elegant serif
- **Body Font**: "Outfit" (modern geometric sans, clean but distinctive)
- **Monospace**: "JetBrains Mono" (code/data elements)

**Font Sizes:**
- Hero: 48px / 3rem
- H1: 32px / 2rem
- H2: 24px / 1.5rem
- H3: 18px / 1.125rem
- Body: 15px / 0.9375rem
- Small: 13px / 0.8125rem
- Micro: 11px / 0.6875rem

**Spacing System:**
- Base unit: 8px
- xs: 4px, sm: 8px, md: 16px, lg: 24px, xl: 32px, xxl: 48px

**Visual Effects:**

*Liquid Glass:*
```css
.glass {
  background: linear-gradient(135deg, rgba(255,255,255,0.05), rgba(255,255,255,0.02));
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid var(--glass-border);
  box-shadow: 
    0 8px 32px rgba(0,0,0,0.4),
    inset 0 1px 0 rgba(255,255,255,0.1);
}
```

*Shadows:*
- Subtle: 0 2px 8px rgba(0,0,0,0.3)
- Medium: 0 8px 24px rgba(0,0,0,0.4)
- Elevated: 0 16px 48px rgba(0,0,0,0.5)
- Glow (gold): 0 0 30px rgba(212,175,55,0.2)

*Animations:*
- Page load: Staggered fade-in + slide up (0.6s ease-out)
- Card hover: Scale 1.02 + shadow elevation (0.2s)
- Glass transition: 0.3s ease
- Progress bar: Smooth fill animation (0.8s ease-in-out)
- Kanban drag: Smooth with rotation tilt (0.2s)

### Components

**1. Sidebar**
- Logo (Alfred crest - geometric shield icon)
- Navigation items with icons
- Quick add button (prominent)
- User profile mini
- States: default, hover (glow), active (accent border)

**2. Kanban Board**
- 4 columns: To Do, In Progress, Done, Archive
- Cards with:
  - Title (bold)
  - Description preview (2 lines max)
  - Priority indicator (colored dot)
  - Due date badge
  - Subtasks progress indicator
- Drag & drop functionality
- Add card button per column

**3. Goal/Objective Cards**
- Title with edit capability
- Breakdown into sprints/iterations
- Progress percentage (animated bar)
- Linked kanban tasks
- Due date with countdown

**4. AI Chat Panel**
- Toggle button (floating)
- Message bubbles (user right, AI left)
- Context indicator (what Alfred "knows" about you)
- Input with send button
- Typing indicator animation

**5. Progress Dashboard**
- Circular progress rings (main goals)
- Weekly/monthly completion stats
- Streak counter
- Achievement badges

**6. Buttons**
- Primary: Gold accent, slight glow on hover
- Secondary: Glass effect, border only
- Ghost: Text only, underline on hover
- Danger: Copper accent

**7. Input Fields**
- Dark background (#1a1a24)
- Platinum border on focus
- Floating labels
- Error states with copper glow

---

## Functionality Specification

### Core Features

**1. Goal Management**
- Create goals with title, description, due date, priority
- Break goals into smaller objectives/tasks
- Set milestones within goals
- Track completion percentage automatically

**2. Kanban Board**
- 4 columns: To Do → In Progress → Done → Archive
- Create/edit/delete cards
- Drag and drop between columns
- Each card has: title, description, priority, due date, subtasks
- Subtask checkboxes
- Card count per column

**3. AI Chat (Alfred)**
- Context-aware conversations
- User can provide context via /context command
- Remembers context within session
- Gives personalized advice based on:
  - Current goals
  - Pending tasks
  - Progress patterns
- Tone: Serious, direct, challenging (like Alfred from Batman)

**4. Progress Tracking**
- Overall progress bar (based on completed tasks vs total)
- Per-goal progress
- Weekly stats (tasks completed, time in progress)
- Visual progress rings

**5. Data Persistence**
- LocalStorage for all data
- Export/Import JSON functionality

### User Interactions

**Adding a Goal:**
1. Click "New Goal" button
2. Modal opens with form
3. Enter title, description, due date, priority
4. System auto-creates first sprint
5. Goal appears in dashboard

**Adding a Task:**
1. Click "+" on any kanban column
2. Inline form appears
3. Enter title, optional description
4. Press Enter or click add
5. Card slides into column

**Chatting with Alfred:**
1. Click chat toggle button
2. Panel slides in from right
3. Type message and send
4. Alfred responds with context awareness

**Providing Context to Alfred:**
- Type `/context [your info]` in chat
- Example: `/context I'm building a SaaS for dentistries`
- Alfred acknowledges and uses this context

### Edge Cases
- Empty states for all sections (goals, tasks, chat)
- Long text truncation with "..."
- Invalid dates handling
- Maximum goals/tasks limits (soft limits with warning)
- Chat history limit (last 50 messages)

---

## Acceptance Criteria

### Visual Checkpoints
- [ ] Dark, premium aesthetic with liquid glass effects
- [ ] Smooth animations on page load (staggered)
- [ ] Cards have hover elevation effect
- [ ] Progress bars animate smoothly
- [ ] Kanban columns have clear visual separation
- [ ] Chat panel slides in/out smoothly
- [ ] Typography is distinctive (not generic)

### Functional Checkpoints
- [ ] Can create, edit, delete goals
- [ ] Can create, edit, delete tasks in kanban
- [ ] Drag and drop works between columns
- [ ] Progress updates when tasks move to Done
- [ ] Chat responds to messages
- [ ] /context command works
- [ ] Data persists after page refresh
- [ ] Responsive on tablet/mobile

### Excellence Standards
- No console errors
- Smooth 60fps animations
- Accessible (keyboard navigation, contrast ratios)
- Clean, organized code

---

## Technical Implementation
- Single HTML file with embedded CSS/JS
- No external frameworks (vanilla JS)
- Google Fonts for typography
- LocalStorage for persistence
- CSS custom properties for theming
