# Appdo MCP research

This is an optional research route. The design workflow also works without a connector.

## Connection and authority

Public setup: https://www.appdo.net/docs/mcp
Streamable HTTP endpoint: `https://www.appdo.net/mcp`

Use an existing authorized Appdo connection. If setup is needed, use the client's current OAuth instructions; never copy a browser session token or put credentials into skill files. A successful discovery response does not prove a successful login or an authenticated tool call.

Discover the actual tools and their schemas in the current host. Prefixes vary by client; names below are the server's unprefixed names. Invoke `get_capabilities({})` and inspect availability, dates and limits. Treat the current response as authoritative over this versioned guide.

## Choose the smallest useful traversal

| Need | Tools and decision |
| --- | --- |
| An exact supplied reference | `get_screen({screen_ref: value})`; use the exact returned or user-provided Appdo identifier |
| A category or product pattern | `search_apps`, then `get_app` and `list_app_screens` for promising results |
| A journey | `list_flows` → `get_flow_apps` using a returned flow ID → `list_app_screens` |
| A screen type | `search_screens` with supported keyword/filter arguments |
| A component pattern | `list_ui_elements` → `get_element_screens` using a returned element ID |
| A 60fps micro-interaction or spring transition | `list_motion_filters` → `search_motion_shots({ filter, has_breakdown: true })` → `get_motion_shot({ slug, include_code: true })` |
| UX psychology & frame-by-frame storyboards | `list_motion_storyboards({ query })` to inspect `S1`–`S5` frames, psychology principles, and UX impacts |
| The user's saved research | `list_my_boards` → `get_board`, when the task concerns their collections |
| A code starting point | `list_templates` → `get_template` using a returned slug (supports `flow` filter and `include_images: true` for extracted Figma kits) |
| The user's purchases | `list_my_orders`, only when purchase information is relevant |

For an exact reference, check capabilities once and resolve it directly; broad research is unnecessary. `get_screen` accepts either `screen_ref` or the pair `app_id` and `screen_id` (including extracted Figma screen codes such as `"O03"` or `"F01"`, plus `include_image: true` to return the inline image content block), not both forms together. App IDs are Appdo library identities, not guessed App Store IDs. Saved-board preview item IDs are not screen references.

When choreographing transitions or tactile feedback between static screens, use `search_motion_shots` (`2,094` shots across `491` apps) with `filter` (from `list_motion_filters`), `has_breakdown: true` (`123` phase-by-phase millisecond/spring breakdowns), or `has_swift_code: true` (`143` standalone code references), then call `get_motion_shot({ slug, include_code: true })` to retrieve `1s` keyframes, AI interaction anatomy, storyboard psychology, reference code, and `expo_reanimated_guidance` mapped directly to `@/theme/motion`.

Current screen filters are `query`, `app_id`, `section`, `flow`, `screen_type`, `element`, `cursor` and `limit`. `list_app_screens` requires `app_id`. Sections are `welcome-screen`, `onboarding`, `paywall` and `other-tabs`. Check the live schema before passing arguments. Discover taxonomy values instead of translating or inventing IDs.

Appdo v1.1 uses keyword search and structured taxonomy filters: **there is no `mode: "semantic"` argument or `get_credits` tool**. Short category, app or screen keywords work better than a long aesthetic brief. If no match appears, try a relevant synonym or broader supported filter, then report missing coverage rather than asserting that the pattern does not exist.

## Inspect and interpret

Open returned media with available image/browser tools before making visual claims. If an image cannot be viewed, say so and separate metadata findings from visual observations. Preserve a useful note such as:

```text
Reference: exact screen_ref or motion shot slug returned by Appdo
Observed: the selected topic stays visible above the primary action; card expands over 420ms (dampingRatio 0.94)
Decision: keep that context in this template's existing bottom action area using motion.springs.arrival
Coverage: one captured state + 1s motion keyframes; keyboard behavior was not observed
```

Capture order is available sequence, not proof of a complete journey. Theme variants and state variants may share one route. Revenue and downloads are estimates; unknown values are not zero and ranking is not evidence of causation.

`similar_screens` in v1 shares flow or tags; it is not a computer-vision match. Element/color tags exist only where recorded. Missing tags do not mean an element is absent from pixels.

## Pagination and failures

- Research, motion, and board pages normally use `items`, `total`, `next_cursor`; `list_templates` uses `templates` and `list_my_orders` uses `orders`. `list_my_boards` returns `boards`; `list_motion_filters` returns `filters` (and optional `glossary`).
- Follow `next_cursor` sequentially with identical filters and limit. Research/motion/board pages allow up to 20 items; template/order lists allow up to 50. Read the schema for defaults.
- Cursors bind the caller, tool, arguments and catalog revision and currently expire after an hour. On `INVALID_CURSOR`, restart once from the first page and deduplicate by stable IDs. If it repeats, report the pagination problem and continue with available evidence; do not loop indefinitely.
- Re-resolve an inaccessible media link by its reference once. Appdo returns existing URLs without guaranteeing uptime or a fixed expiry period.
- Respect rate-limit retry guidance. If authentication or a source fails repeatedly, stop that research path, explain the limitation and use local evidence where possible.

All 19 current tools are read-only. Boards are saved-library category groups, not editable custom boards. Template responses expose public details/demo/gallery, not purchased source archives. The MCP cannot install source code or grant a license. Use a local checkout or user-authorized source package for implementation.

Do not import Appllama's paid-credit model, media expiry claims or tools into Appdo instructions. Appdo v1.1 reports `billing: "not-metered"`; this is a present capability, not a promise about future pricing.
