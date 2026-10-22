# Architecture and contract notes

Prepared 2026-10-09 (updated 2026-10-22). This is an Appdo-authored skill package for researching, implementing, and verifying mobile flows in Appdo templates.

Appdo architectural decisions:

- One entry skill with optional MCP guidance, working seamlessly both with live Appdo MCP and with local template source code.
- Appdo tool contracts and coverage, including keyword-only search, 60fps motion & storyboard references, and saved-category collections.
- Local template integration and explicit distinction between prototype services and real services.
- Verification proportional to the changed behavior; no fixed research quota, universal dependency choices or unsupported performance claims.

Appdo contract sources in the repository: `docs/integrations/APPDO_MCP.md`, `src/lib/mcp/tools/`, `src/lib/mcp/appdo-design-library.ts`, and the target template's `AGENTS.md` and package scripts. Public connection guide: https://www.appdo.net/docs/mcp.

Review this reference when the server contract or template architecture changes. Live schemas and applicable project instructions take precedence over a dated example.
