# Sources and adaptation

Prepared 2026-10-09. This is an Appdo-authored skill informed by the public organization and research-to-implementation approach of [Appllama/appllama-skills](https://github.com/Appllama/appllama-skills).

Upstream reference entry points:

- [appllama-usage](https://github.com/Appllama/appllama-skills/blob/main/skills/appllama-usage/SKILL.md)
- [appllama-app-design-skill](https://github.com/Appllama/appllama-skills/blob/main/skills/appllama-app-design-skill/SKILL.md)
- [Upstream MIT license](https://github.com/Appllama/appllama-skills/blob/main/LICENSE)

The upstream names, logo and library media remain their owners' property. This package contains newly written instructions, not bundled upstream code, artwork or library captures, and does not imply affiliation. Retain the upstream copyright and license if future changes incorporate upstream material.

Appdo-specific decisions:

- One entry skill with optional MCP guidance, rather than requiring two installed skills.
- Appdo tool contracts and coverage, including keyword-only search and saved-category collections.
- Local template integration and explicit distinction between prototype services and real services.
- Verification proportional to the changed behavior; no fixed research quota, universal dependency choices or unsupported performance claims.

Appdo contract sources in the repository: `docs/integrations/APPDO_MCP.md`, `src/lib/mcp/tools/`, `src/lib/mcp/appdo-design-library.ts`, and the target template's `AGENTS.md` and package scripts. Public connection guide: https://www.appdo.net/docs/mcp.

Review this reference when the server contract or template architecture changes. Live schemas and applicable project instructions take precedence over a dated example.
