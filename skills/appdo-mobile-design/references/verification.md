# Verify the changed mobile experience

Use checks relevant to the change and the project's required validation. Reuse a healthy running app when possible. Verify new behavior and plausible regressions rather than collecting screenshots without a question to answer.

## Layout and accessibility

- Inspect the changed screen in a native simulator/emulator or device for each available target platform. A web preview can supplement this but does not prove native behavior.
- Check a compact viewport, supported themes, increased text size and realistically long content. The primary action must remain reachable around safe areas, home indicators and the keyboard.
- Verify labels, roles, selected/disabled states and reading order. Use platform target sizes (normally at least 44 pt on iOS and 48 dp on Android); do not shrink touch areas to match an image.
- Check readable contrast and communicate status with more than color. Verify meaningful content is not lost through truncation.
- Exercise loading, empty, error and success paths that the feature can actually reach. Avoid adding fictional states solely to fill a checklist.

## Interaction and navigation

| Change | Evidence to collect |
| --- | --- |
| Static layout or styling | Inspect screenshots of the affected states and check nearby interactions |
| Navigation or completion | Walk entry → main action → completion → back; confirm history matches the product rule |
| Form or composer | Type, edit, submit, handle validation, show/dismiss keyboard and check focus |
| Sheet or gesture | Open, interact, dismiss, cancel mid-gesture and try repeated input |
| Async action | Check waiting, failure/retry and duplicate-tap behavior using available test controls |
| Motion or reported jank | Record and inspect the affected interaction; profile if making performance claims |

Use native back gestures and Android back where applicable. Reset or replace history only when the product requires it, such as leaving completed onboarding; do not prohibit back on every success screen. A dismissal should return to a coherent underlying state.

Record a flow when timing, transition continuity or gesture behavior is part of the change. Watch it at normal speed and inspect suspicious frames. Static screenshots cannot establish motion quality, and a recording alone is not a measured FPS result. Keep performance claims tied to profiler evidence and the actual runtime/build/device.

For reduced motion, confirm that essential state changes remain understandable and the application respects the user's system preference. Avoid introducing a bespoke gesture or animation framework only to satisfy this guide.

## Evidence and stopping condition

After a fix, repeat the affected checks. Once the requested behavior and required checks pass, stop; a design task does not require endless subjective polishing or an unrelated full-app audit.

Report:

- What was implemented and which reference or product need informed it.
- The tests run and the screens/interactions actually inspected.
- The platform, theme and runtime used for visual evidence.
- Any unverified behavior and the concrete reason (for example, no Android runtime or no live speech service).

If no runtime is available, finish useful code/static checks and clearly mark visual and interaction verification as pending. Do not label the flow simulator-verified based on source review, a passing build or screenshots supplied as design references.
