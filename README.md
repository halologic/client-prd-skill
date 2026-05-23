# Client PRD Skill

A Claude skill that generates client-facing Product Requirements Documents as
email-safe HTML files. Copy the rendered HTML into Gmail or Outlook and send —
no broken layouts, no missing styles, no fuss.

## What It Does

When invoked, this skill:

1. Gathers the project details (client name, project type, brand colors if available)
2. Writes a complete, professionally-styled PRD as a single HTML file
3. Saves it with a predictable filename ready to share

The output is engineered specifically to survive copy-paste into Gmail and Outlook,
which strip most modern CSS. Everything is inline-styled, table-based for layout, and
uses only web-safe fonts.

## What's Included

- **Project Overview** — what's being built and why
- **Goals & Success Criteria** — measurable outcomes in a clean table
- **Scope of Work** — in-scope and out-of-scope items, clearly separated
- **Proposed Timeline** — phases, deliverables, and week-based targets
- **Open Questions for Client** — what you need answered to proceed
- **Recommended Next Step** — a clear, specific call to action

## Trigger Phrases

The skill activates when you say things like:

- "Draft a client PRD for [project]"
- "Write a PRD I can email to [client]"
- "Make a project requirements doc for the [project] build"
- "Document the plan before we build"
- "Generate a PRD for [client]"

## How to Use the Output

Once the skill generates the HTML file:

1. Open it in any web browser
2. Select all (`Cmd+A` on Mac, `Ctrl+A` on Windows)
3. Copy (`Cmd+C` / `Ctrl+C`)
4. Paste into a Gmail or Outlook compose window
5. Send

The formatting carries over and renders correctly in both clients.

## Brand Customization

If you provide a brand guide or hex color values, the skill will style the PRD in
that brand. Otherwise it uses a neutral, professional default palette. You can
choose to send the PRD in your own agency's brand or in the client's brand.

## Installation

Clone or download this repository and place the `client-prd/` folder into your
Claude skills directory:

- **Claude Code:** `~/.claude/skills/` (or wherever your user skills live)
- **Claude.ai / Claude Desktop:** Upload via the Skills interface

## Structure

```
client-prd/
├── SKILL.md                              # Main workflow
└── references/
    ├── email-html-rules.md               # Gmail/Outlook coding rules
    └── prd-template.md                   # Document skeleton and brand defaults
```

## Credit

Originally built in collaboration with Claude, inspired by community discussion
in AiFoundations about using HTML as a presentation layer for plans and PRDs.

## License

MIT — use it, modify it, share it.
