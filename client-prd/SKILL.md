---
name: client-prd
description: >
  Generates a client-facing Product Requirements Document (PRD) as an email-safe HTML file
  that can be copied and pasted directly into Gmail or Outlook and rendered correctly.
  Use this skill any time the user says "draft a client PRD", "write a PRD for [project]",
  "make a PRD I can email", "build a project requirements doc", "generate a PRD for [client]",
  or any variation of creating a pre-build plan document to share with a client.
  Also triggers when the user says "let's document the plan before we build" or "write up
  what we agreed on so I can send it to the client." Always invoke this skill when the
  output needs to be a client-deliverable document rather than a chat reply.
---

# Client PRD Skill

Generates a structured, client-facing Product Requirements Document as a single HTML file
coded entirely with inline styles — no external CSS, no style blocks, no web fonts — so it
survives copy-paste into Gmail or Outlook without breaking.

Output is a file named `[ClientName]_PRD_v[N].html` saved to the working directory and
presented for download.

---

## Workflow

### Step 1 — Gather inputs

Collect the following before writing anything. Pull from user memory, user preferences,
or earlier conversation context whenever available — for example, if Claude already knows
the user's name, agency name, or default brand colors, use that information silently
without re-asking. Only ask the user directly for fields that are genuinely missing.

**Required:**
- Client or project name (used in filename and header)
- Project type (website redesign, app build, video production, etc.)
- Whose brand to style the document in: the user's agency or the client's

**Optional but improves output:**
- Brand colors (hex values) — if not provided, use the neutral defaults (see references/brand-defaults.md)
- Key scope items already discussed (in-scope and out-of-scope)
- Known timeline or phase structure
- Open questions that need client answers
- Version number (default: 1.0)
- Status (default: "For Client Review")

If brand guide details are provided (colors, fonts), note that Gmail strips external fonts.
Apply the brand colors to all elements. For typography, use the closest web-safe fallback
and note this in a comment at the top of the HTML file.

---

### Step 2 — Plan the document structure

Before writing HTML, silently confirm the section set. Default sections are:

1. Project Overview
2. Goals & Success Criteria (table)
3. Scope of Work (in-scope list + out-of-scope list)
4. Proposed Timeline (table)
5. Open Questions for Client (numbered list)
6. Recommended Next Step (callout block)

Add, remove, or rename sections based on the project type. For example:
- Video production PRDs should replace "Timeline" with "Production Schedule" and add a "Deliverables" section
- App builds should add a "Technical Stack" section
- Accessibility/compliance work should add a "Regulatory Context" section

---

### Step 3 — Write the HTML

Read `references/email-html-rules.md` now. Apply every rule without exception.
Read `references/prd-template.md` for the structural skeleton and inline style patterns.

Write the complete HTML document. Do not summarize or abbreviate — write every section
in full. Bracket placeholders like `[Client Name]` are never acceptable in the final output;
all fields must be populated from the gathered inputs.

The pre-flight checklist comment block at the top of the file is mandatory. See
`references/prd-template.md` for the exact format.

---

### Step 4 — Save and present

Save the file as:
```
[ClientName_NospacesTitleCase]_PRD_v[VersionNumber].html
```

Examples:
- `AcmeCorp_PRD_v1.html`
- `Riverside_PRD_v2.html`
- `NorthernLights_PRD_v1.html`

Present the file for download. Follow with a one-sentence paste instruction reminder:
> Open in a browser, select all (Cmd+A), copy (Cmd+C), paste into Gmail or Outlook compose.

---

## Hard Rules

- NEVER use `<style>` blocks or external stylesheets. Gmail and Outlook strip them.
- NEVER use Google Fonts or any external font `<link>`. Use web-safe font stacks only.
- NEVER use JavaScript.
- NEVER use CSS classes — all styles must be inline `style="..."` attributes.
- NEVER leave bracket placeholders in the final output.
- ALWAYS write every section in full prose and complete sentences.
- ALWAYS include the pre-flight checklist comment at the top of the file.
- Table layouts MUST use explicit `border-collapse:collapse` and `border` on each `<td>`.
- `border-radius` is decorative only — acceptable on outer wrapper but do not rely on it
  for visual structure since Outlook's Word renderer ignores it.
- The file MUST be self-contained — one file, no dependencies.
