# 60fps Golden Interactions & Psychology Reference for Expo Templates

Derived from the Appdo 60fps interaction library (2,094 shots, 67 storyboards, and 20 compile-checked snippets), translated 1:1 into **Expo / React Native (`react-native-reanimated` v4)** primitives in `@/theme/motion` and `@/components/*`.

## 1. Centralized Motion Token System (`src/theme/motion.ts`)

Every Appdo template inherits four named spring roles (`ReduceMotion.System` aware) so the entire application moves with one consistent voice:

| Token | Reanimated Config | Reference Archetype | Use Case |
| :--- | :--- | :--- | :--- |
| `motion.springs.feedback` | `{ duration: 320, dampingRatio: 0.78 }` | `#008` Line Graph Morph (*Family*) | Immediate button release (`SpringPressable`), filter chip selection, step checkboxes |
| `motion.springs.change` | `{ duration: 360, dampingRatio: 0.90 }` | `#012` / `#014` / `#017` (*Monogram*, *Captions*, *Family*) | Accordion expand/collapse, sheet resizing, progress bar fill, number flip |
| `motion.springs.arrival` | `{ duration: 420, dampingRatio: 0.94 }` | `#004` Plan Switch Card Expand (*AllTrails*) | Cohesive two-card plan expansion, screen stage arrival (`stageEntering`) |
| `motion.springs.emphasis` | `{ duration: 460, dampingRatio: 0.72 }` | `#007` Hold to Commit (*Opal*) | Milestone lock-in, commitment completion pop |

## 2. Included Golden Micro-Interaction Primitives

1. **`<SpringPressable />` (`src/components/spring-pressable.tsx`)**
   - Triggers immediate UI-thread `scaleTo` (`0.97` default) over `120ms` (`motion.easings.out`) on `onPressIn` and settles back with `motion.springs.feedback` on `onPressOut`.
   - Degrades gracefully to calm opacity feedback when `useReducedMotion()` is active.

2. **`<PlanSwitchCards />` (`src/components/plan-switch-cards.tsx` — Snippet `#004` AllTrails)**
   - Stacked option/plan cards sharing `motion.layoutSpring`. Selecting a card darkens its border and expands its 3-step timeline while collapsing the unselected card in lockstep.
   - **Psychology**: *Progressive Disclosure, Transparency, Risk Reversal*.

3. **`<HoldToCommitButton />` (`src/components/hold-to-commit-button.tsx` — Snippet `#007` Opal)**
   - Press-and-hold commitment pill that sweeps a progress fill across the button over `1.2s` before locking into a committed state (`✓`). Releasing early rewinds smoothly in `180ms`.
   - **Psychology**: *Commitment & Consistency, Effort Justification, Deliberate Friction*.

4. **`<RollingNumber />` (`src/components/rolling-number.tsx` — Snippets `#006` Push & `#011` Family)**
   - Tabular numerical counter that rolls vertically (`FadeInDown` / `FadeOutUp`) when values change, with optional `maskable` tap-to-hide privacy dots (`••••`).
   - **Psychology**: *Feedback Loop, Privacy Control, Progress Visibility*.

5. **`<EffortSliderCard />` (`src/components/effort-slider.tsx` — Shots `#677` Apple Fitness Effort Slider & `#385` Seven Workout Timer)**
   - 10 ascending intensity bars (`1–10 RPE`) that fluidly shift accent color and biological zone badge (`{ duration: 250, dampingRatio: 0.72 }`), paired with a rhythmic `3-2-1-GO` set countdown timer.
   - **Psychology**: *Immediate Visual Feedback, Embodied Intensity, Rhythmic Anticipation*.

## 3. All 20 Golden Interaction Archetypes (SwiftUI → Expo Mapping)

| # | Interaction Name | Reference App | Primary Expo Primitive |
| :--- | :--- | :--- | :--- |
| `001` | Group Stage Timeline Tab | Apple Sports | `Gesture.Pan` + bracket window snap |
| `002` | Circle Progress Fill | GrowPal | `react-native-svg` animated stroke / childless progress fill |
| `003` | List Item Accordion Expand | Amie | `Animated.View layout={motion.layoutSpring}` |
| `004` | Plan Switch Card Expand | AllTrails | `<PlanSwitchCards />` (`duration: 420, dampingRatio: 0.94`) |
| `005` | Forward Toast Icon | Telegram | Floating `Animated.View` toast (`150ms` enter / `200ms` exit) |
| `006` | Number Flip with Reflection | Push | `<RollingNumber />` (`tabular-nums` + vertical slide) |
| `007` | Hold to Commit Button | Opal | `<HoldToCommitButton />` (`1200ms` linear hold + spring lock) |
| `008` | Line Graph Morph | Family | `dampingRatio: 0.82, duration: 320` path interpolation |
| `009` | Continue Button to Tick | CRED | Button morph into completion check state |
| `010` | OTP Input Pulse Fill Success | Toss | Staggered 6-box wave + success badge reveal |
| `011` | Hide Sensitive Number | Family | `<RollingNumber maskable />` privacy dot crossfade |
| `012` | Keyboard to Input Morph | Monogram | Bottom pill morph (`duration: 360, dampingRatio: 0.92`) |
| `013` | Mini Player Play & Scrub | [untitled] | Waveform drag scrub + floating time badge |
| `014` | See All Menu Expand | Captions | Shortcut grid expansion (`duration: 360, dampingRatio: 0.90`) |
| `015` | List Fade Up from Down | Vakitler | `stageEntering(getStaggerDelay(index))` |
| `016` | Card 3D Flip | How We Feel | `rotateY` perspective interpolation (`150ms`–`360ms`) |
| `017` | Bottom Sheet Detail Expansion | Family | Sheet container `layout={motion.layoutSpring}` |
| `018` | Bottom Tabs Active Expansion | Neuecast | Pill indicator shared layout transition |
| `019` | Spin to Circle Voice Orb | ChatGPT | `withRepeat` breathing scale/opacity (`2800ms`) |
| `020` | Selection to Illustration | Revolut | Live preview card scaling row count with picker state |

## 4. Querying the Full 3,241-Record Motion Library (Appdo MCP & Supabase)

Beyond the 20 archetypes above, the complete extracted motion dataset (`36 MB`, `3,241` normalized records) is live in **Supabase PostgreSQL** and exposed via **Appdo MCP**:

1. **Via Appdo MCP Tools (`/mcp`):**
   - `list_motion_filters({ category, include_glossary: true })` — 108 5-axis filters (`Platform`, `Screen`, `Element`, `Gesture`, `Animation`) + 85 motion glossary definitions.
   - `search_motion_shots({ query, app_slug, filter, has_breakdown, has_swift_code })` — Search 2,094 shots (including 1,744 with AI anatomy & `1s` keyframes, 123 with phase-by-phase breakdowns, and 143 with reference code).
   - `get_motion_shot({ slug, include_code: true })` — Full breakdown, `1s` keyframes, UX psychology storyboard, SwiftUI reference code, and `expo_reanimated_guidance`.
   - `list_motion_storyboards({ query, app_slug })` — 67 frame-by-frame interaction storyboards (`S1`–`S5`) with behavioral psychology principles and UX impact analysis.

2. **Via Supabase Cloud Tables (`public.motion_reference_*`):**
   - `public.motion_reference_shots` (`2,094` rows)
   - `public.motion_reference_apps` (`491` rows)
   - `public.motion_reference_filters` (`108` rows)
   - `public.motion_reference_glossary` (`85` rows)
   - `public.motion_reference_icons` (`83` rows)
   - `public.motion_reference_storyboards` (`67` rows)
   - `public.motion_reference_assets` (`313` rows)
