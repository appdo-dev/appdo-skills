# Working in Appdo templates

Locate the repository and target template before using these relative paths. These notes are a navigation aid, not replacements for the current project instructions.

## Resolve the implementation contract

1. Read root and template `AGENTS.md`, the template README, its `package.json` and lockfile.
2. Follow the template's available Expo guidance and template-specific skill when those files exist. Resolve references relative to the file containing them; do not assume every skill lives at repository root. If an optional skill is absent, continue from code and versioned official documentation.
3. Inspect `src/app` for route entry points, `src/screens` for screen bodies, `src/components` for reusable UI and `src/theme` for tokens. Confirm these folders rather than creating a second architecture when a target differs.
4. Inspect current state providers and service adapters. Preserve public route names, persistence keys, accessibility labels and data contracts unless the feature requires changing them.

Appdo's website tokens and native template tokens serve different surfaces. Do not import web CSS or website components into a native template. Preserve the template's native tab implementation and its web fallback.

A template's Expo version and Runner module profile are deployment contracts. Read its installed versions and exact versioned documentation before choosing APIs. An unavailable native module cannot be fixed by silently adding it to a shared Runner. Follow the project's compatibility process when a requested feature needs one.

Keep identity changes consistent with the current template instructions (commonly `app.json` and `src/app-config.ts`). A visual improvement does not need an identity change.

## Learning Language AI: example starting point

Current source location in the Appdo repository: `templates/learning-language-ai`.
Public template slug: `learning-language-ai`.

With MCP available, pass this object to `get_template`:

```json
{"slug":"learning-language-ai"}
```

Read `template.design_library.app_id` from the result. If absent, use local source/gallery evidence rather than inventing a research registration.

At the time this guide was created, the associated library app was `market:appdo-learning-language-ai`, with a `speaking-practice` flow. Confirm the current response before using those values. The nine original curated captures included theme/state variants of welcome and speaking screens; they did not establish nine separate routes or full onboarding coverage. Read capture notes and distinguish prototype/debug overlays from intended product UI.

For a request to improve speaking practice, inspect the target's speaking screen, practice state provider, theme and action/sheet components. Preserve the chosen topic through entry, active practice, hints and review. Define what happens when the user exits early or retries. Keep mock responses clearly distinct from live speech/AI services.

Use this flow only when it matches the request. The same skill supports other template flows without inheriting Learning Language AI's palette, routes, service choices or state model.

## Validation and delivery

Run relevant package scripts discovered from the target. Learning Language AI currently provides `typecheck`, `test`, `doctor` and `export`; its instructions determine which checks are required after code changes. Skill-only documentation changes do not require a template build or cloud deploy.

For runtime verification, discover available devices and follow the repository's simulator selection. Never embed a developer's absolute path, fixed machine identifier or credentials into reusable skill instructions.

Store requested audit evidence in the repository's established audit location, with the flow, runtime, tested states and remaining limitations. A screenshot of a gallery image is reference evidence, not proof that the modified application ran.

Commit, publish, purchase, account linking and backend changes require the corresponding task scope and existing authorization. Creating or using this design skill alone does not initiate them.
