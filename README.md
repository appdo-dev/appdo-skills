# Appdo Skills

Design, build, and verify mobile flows with Appdo.

[Appdo](https://www.appdo.net) · [MCP setup](https://www.appdo.net/docs/mcp) · [Tiếng Việt](#tiếng-việt)

## Included skill

| Skill | Purpose |
| --- | --- |
| [appdo-mobile-design](skills/appdo-mobile-design/SKILL.md) | Research mobile patterns, implement screens in Appdo templates, and verify navigation, accessibility and visual states. Includes Expo / React Native guidance and a Learning Language AI example. |

The skill works standalone with local code and supplied references; Appdo MCP adds optional library research.

## Install

From your project directory:

```sh
npx skills@latest add appdo-dev/appdo-skills --skill appdo-mobile-design
```

Choose a supported agent when prompted. To install specifically for Codex:

```sh
npx skills@latest add appdo-dev/appdo-skills --skill appdo-mobile-design -a codex
```

To install user-wide, add `-g`. To inspect available skills before installing:

```sh
npx skills@latest add appdo-dev/appdo-skills --list
```

For a manual installation, copy the entire `skills/appdo-mobile-design` directory into your agent's skills directory. Codex normally uses `$CODEX_HOME/skills` or `~/.codex/skills`. Keep the `references/` and `agents/` folders together. Compare an existing installation before replacing it. Open a new session if the agent has not refreshed its skill list.

## Try it

```text
$appdo-mobile-design Improve the speaking practice flow in Learning Language AI. Keep the current theme and architecture, implement relevant states, and verify the flow in a simulator.
```

```text
$appdo-mobile-design Review this mobile screen using the screenshot and local source. Prioritize readability, the primary action, and back behavior.
```

```text
$appdo-mobile-design Research paywall patterns with Appdo MCP and recommend an approach for this template. Research only; do not change code.
```

## Optional Appdo MCP

Endpoint: `https://www.appdo.net/mcp`

Follow the [connection guide](https://www.appdo.net/docs/mcp) and authorize with your Appdo account. Installing this skill does not install a connector or grant account access.

The skill checks the connected server's capabilities before researching. Appdo v1.1 supports keyword search, screen references, flow and element discovery, **60fps motion & micro-interaction reference tools** (`list_motion_filters`, `search_motion_shots`, `get_motion_shot`, `list_motion_storyboards`), saved collections and published template details. All 19 current tools are read-only. Semantic search and visual-similarity ranking are not implemented in v1.1. Public template details do not include purchased source downloads.

Without a working connection, the skill uses the current code, design tokens and supplied images, and reports the research limitation.

## Package structure

```text
skills/appdo-mobile-design/
  SKILL.md
  agents/openai.yaml
  references/
    appdo-mcp.md
    appdo-templates.md
    motion.md
    60fps-patterns.md
    verification.md
    sources.md
```

## Status

Current release: **0.3.0** (adds `references/60fps-patterns.md` with centralized `@/theme/motion` spring tokens, 5 Golden Micro-Interaction Primitives (`SpringPressable`, `PlanSwitchCards`, `HoldToCommitButton`, `RollingNumber`, `EffortSliderCard`), 20 interaction archetypes, Appdo MCP v1.1 60fps Motion Reference tools (`2,094` shots + `67` UX psychology storyboards), and runtime validation on `expo-base`, `tempo-focus`, and `learning-language-ai`). The skill is not automatically integrated into Appdo AI Editor.

## Tiếng Việt

Bộ skill hỗ trợ thiết kế, triển khai và review luồng mobile của Appdo. Có thể sử dụng độc lập từ code và ảnh tham khảo; MCP là tùy chọn.

Cài bằng lệnh ở trên, sau đó thử:

```text
$appdo-mobile-design Cải thiện luồng speaking practice của Learning Language AI, giữ theme hiện tại và kiểm tra trên simulator.
```

Skill hướng dẫn giữ cấu trúc template, dùng đúng công cụ MCP, hoàn thiện hành vi và phân biệt kết quả đã kiểm tra với phần chưa xác minh.

## License

Skill instructions and documentation in this repository are authored for Appdo (see [architecture and contract notes](skills/appdo-mobile-design/references/sources.md)) and released under the [MIT license](LICENSE). This license does not grant rights to third-party trademarks, library media or separately licensed Appdo templates.
