# Motion and tactile craft in Appdo templates

Static screenshots from Appdo MCP or Figma show keyframe states (`O03`, `O04`, `F01`, `F03`), never the choreography between them. When implementing a screen or flow in React Native / Expo, translate static reference frames into fluid, physical UI-thread motion rather than hard-cutting React state.

For full Reanimated and Gesture Handler recipes, pair this guide with `animate-expo` / `expo-animation` when installed in the workspace, and see `references/60fps-patterns.md` for the 20 golden interaction archetypes and `@/theme/motion` token system.

## 1. Gate every animation by frequency and purpose

| Frequency | Decision |
| --- | --- |
| 100+ times/day (tab switches, scrolling, keyboard appearance) | Platform default or `animation: "none"`. Never slide between peer tabs. |
| Tens of times/day (button press, chip selection, mode card tap, quiz row tap) | Fast tactile press-in response (`100–150ms`) on the UI thread. |
| Occasional (onboarding step transitions, focus stage changes, sheets, modals) | Choreographed spring/ease-out transition (`250–420ms`). |
| Rare / first-time (onboarding hero illustrations, session completion `F05` / `O12`) | Signature ambient motion and staggered entrance. |

Every animation must serve a named purpose: **feedback** (press scale), **spatial continuity** (step progression, sheet movement), **state indication** (active mode glow, progress bar interpolation), or **delight** (hero illustration ambient motion).

## 2. Five mandatory motion layers for Appdo templates

Whenever implementing an interactive flow from static design references, include these five layers unless the platform or reduced-motion setting dictates otherwise:

1. **Immediate press-in physics (`SpringPressable`)**
   - Trigger visual feedback on `onPressIn`, never wait for `onPress`.
   - Scale to `0.96–0.97` over `100–140ms` using `Easing.bezier(0.23, 1, 0.32, 1)` and settle back on `onPressOut` with a spring (`{ duration: 320, dampingRatio: 0.78 }`).
   - Keep touch targets at least `44×44pt` (`48×48dp` on Android) using `hitSlop` when the visual pill is compact.

2. **Choreographed stage transitions (no hard-cut conditional rendering)**
   - Multi-step flows held in state (such as Onboarding `O02`→`O12`, Quizzes, or Focus states `F01`→`F08`) must not swap views with un-animated `{step === 'X' && <View />}` cuts.
   - Stagger the incoming stage on the UI thread:
     - **Hero / focal visual**: enters first (`0ms` delay) from `scale(0.94)`, `translateY(14)`, `opacity(0)` using `{ duration: 400, dampingRatio: 0.82 }`.
     - **Headline & copy stack**: enters second (`55–70ms` delay) from `translateY(12)`, `opacity(0)`.
     - **Interactive controls / cards**: enter third (`100–130ms` delay) with subtle per-item stagger (`25–40ms`).

3. **Continuous value interpolation**
   - Progress indicators, segmented bars, dial progress, and comparison charts should interpolate smoothly with `withSpring` or `withTiming` (`Easing.bezier(0.23, 1, 0.32, 1)`) when their underlying state changes.
   - Ambient theme backdrops (e.g., switching between semantic hues) should crossfade or pulse smoothly rather than snapping colors in a single frame.

4. **Hero micro-motion for signature screens**
   - Signature onboarding and focus heroes (such as a glass dome, glowing squircle cluster, or active timer dial) should include restrained, UI-thread ambient motion: subtle breathing luminescence (`scale: 1 → 1.05`, `opacity` oscillation over `2.4–3.2s`) and gentle orbital drift on secondary elements.
   - Never animate `BlurView` intensity or Android `elevation` per frame; animate `transform` and `opacity` of pre-rendered layers instead.

5. **Synchronized haptics and reduced motion**
   - Fire haptics on the **same frame** as the causal visual change (`selection` for step/chip switches, `light` for option selection, `medium` for primary CTA commit, `success` for completion).
   - Respect `useReducedMotion()` from `react-native-reanimated`: when enabled, replace translation, scale bounce, and continuous ambient loops with calm opacity crossfades.
