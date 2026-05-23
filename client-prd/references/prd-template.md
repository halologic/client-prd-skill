# PRD Template & Brand Defaults

Structural skeleton and default brand values for client PRD HTML documents.
Read alongside `email-html-rules.md` before writing any PRD HTML.

---

## Neutral Default Brand Values

Use these when the user has not specified a brand or has chosen to send the PRD in
their own agency's neutral style. These values produce a professional, readable
document that works across most contexts.

| Token | Value |
|---|---|
| Primary dark | `#003366` (navy) |
| Accent blue | `#7aabcc` |
| Highlight blue | `#a0c4e0` |
| Light blue bg | `#eef5fb` |
| Table header bg | `#f0f4f8` |
| Alternating row bg | `#f9f9f7` |
| Table border | `#dde3ea` |
| Status color (draft) | `#c05000` (amber) |
| Body text | `#222` |
| Secondary text | `#333` |
| Muted text | `#555` |
| Footer text | `#888` |
| Page bg | `#f5f5f0` |
| Card bg | `#ffffff` |
| In-scope green | `#006633` |
| Out-of-scope red | `#993300` |
| Agency label | `[Your Agency Name]` |

---

## Applying a Client Brand

When the user provides a brand guide or color values for the client:

1. Replace `#003366` (primary dark) with the client's primary brand color
2. Replace `#7aabcc` / `#a0c4e0` (accents) with lighter tints of the client's primary
3. Replace `#eef5fb` (callout background) with a very light tint of the client's primary
4. Keep `#f0f4f8`, `#f9f9f7`, `#dde3ea` as neutral table chrome unless client has
   strong secondary neutrals to substitute
5. Update agency label in header to client name or leave as user's agency per their choice
6. Add font note in the pre-flight comment block

Always check contrast: primary color text on white background must meet WCAG AA (4.5:1
for normal text, 3:1 for large/bold). If the client's brand color is light, use it as a
background and use white or dark text on top of it.

---

## Full Document Skeleton

Below is the complete HTML skeleton. Claude should use this as the starting structure
and fill in all content. Do not omit sections or leave placeholders.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>[ClientName] PRD v[N] – [AgencyName]</title>
</head>
<!--
  PRD PRE-FLIGHT CHECKLIST
  [populate per email-html-rules.md]
-->
<body style="margin:0;padding:0;background:#f5f5f0;font-family:Georgia,serif;">

<!-- OUTER WRAPPER -->
<div style="max-width:680px;margin:32px auto;background:#ffffff;
            border:1px solid #ddd;border-radius:4px;overflow:hidden;">

  <!-- ① HEADER BAND -->
  <div style="background:[PRIMARY];padding:28px 36px 24px;">
    <div style="font-family:Arial,Helvetica,sans-serif;font-size:11px;
                color:[ACCENT];letter-spacing:2px;text-transform:uppercase;
                margin-bottom:6px;">[AgencyName]</div>
    <div style="font-size:24px;font-weight:700;color:#ffffff;
                line-height:1.25;">Product Requirements Document</div>
    <div style="font-size:15px;color:[HIGHLIGHT];margin-top:4px;">[ProjectName]</div>
  </div>

  <!-- ② META BAR -->
  <div style="background:#f0f4f8;border-bottom:1px solid #dde3ea;
              padding:14px 36px;font-family:Arial,Helvetica,sans-serif;
              font-size:12px;color:#555;">
    <span style="margin-right:28px;">
      <strong style="color:[PRIMARY];">Version:</strong> [X.X] Draft
    </span>
    <span style="margin-right:28px;">
      <strong style="color:[PRIMARY];">Date:</strong> [Month DD, YYYY]
    </span>
    <span style="margin-right:28px;">
      <strong style="color:[PRIMARY];">Prepared by:</strong> [Name]
    </span>
    <span>
      <strong style="color:[PRIMARY];">Status:</strong>
      <span style="color:#c05000;font-weight:700;">For Client Review</span>
    </span>
  </div>

  <!-- ③ BODY -->
  <div style="padding:32px 36px 40px;">

    <!-- SECTION HEADING PATTERN (repeat for each section) -->
    <!--
    <div style="font-family:Arial,Helvetica,sans-serif;font-size:10px;font-weight:700;
                color:[PRIMARY];letter-spacing:2px;text-transform:uppercase;
                border-bottom:2px solid [PRIMARY];padding-bottom:6px;
                margin-bottom:14px;">0N &nbsp;Section Title</div>
    -->

    <!-- 01 PROJECT OVERVIEW -->
    <!-- Two paragraphs: what the project is + any key regulatory/compliance context -->

    <!-- 02 GOALS & SUCCESS CRITERIA -->
    <!-- Table: Goal | How We Measure It -->
    <!-- 3–5 rows, alternating background -->

    <!-- 03 SCOPE OF WORK -->
    <!-- IN SCOPE header (green) + bulleted list -->
    <!-- OUT OF SCOPE header (red/amber) + bulleted list -->

    <!-- 04 PROPOSED TIMELINE -->
    <!-- Table: Phase | Deliverable | Target -->
    <!-- Discovery → Design → Development → QA → Launch -->

    <!-- 05 OPEN QUESTIONS FOR CLIENT -->
    <!-- Numbered list, 3–6 questions -->
    <!-- Only include questions that are genuinely unresolved -->

    <!-- NEXT STEP CALLOUT -->
    <!-- Blue left-border box with bold label and action paragraph -->

    <!-- FOOTER -->
    <div style="font-family:Arial,Helvetica,sans-serif;font-size:12px;color:#888;
                border-top:1px solid #eee;padding-top:16px;">
      This document is a working draft shared for client review. All timelines are
      estimates pending kickoff conversation.
      &copy; [YEAR] [AgencyName].
    </div>

  </div><!-- /body -->
</div><!-- /outer wrapper -->

</body>
</html>
```

---

## Section Content Guidelines

### 01 Project Overview
- 2–3 paragraphs, full sentences
- Paragraph 1: What is being built and for whom
- Paragraph 2: Key approach or methodology (WordPress, accessibility-first, etc.)
- Paragraph 3 (optional): Any regulatory, compliance, or deadline context

### 02 Goals & Success Criteria
- 3–5 rows minimum
- Goals should be outcomes, not activities ("Modern design" not "Design a homepage")
- Measurements should be specific and verifiable (scores, audit passes, approval milestones)
- Always include a "client self-sufficiency" or handoff goal if training is in scope

### 03 Scope of Work
**In Scope:** Be specific. List technology stack, number of pages or deliverables,
specific services included. Specificity prevents scope creep conversations later.

**Out of Scope:** Always include 3–5 items. Common exclusions: e-commerce, custom plugins,
ongoing SEO/maintenance, hosting setup, content writing (if client is providing copy).

### 04 Proposed Timeline
- Phase names: Discovery, Design, Development, QA & Accessibility, Launch
- Deliverables are the client-facing milestone artifacts (approval gates, staging site, etc.)
- Targets expressed as "Week N" or "Week N–M" ranges, not specific calendar dates
  (unless dates were explicitly agreed upon)

### 05 Open Questions
- Only include genuinely unresolved items
- Frame as questions the client needs to answer, not internal decisions
- Typically 4–6 items
- Common categories: content ownership, brand assets, third-party integrations,
  approval chain, existing platform constraints

### Next Step Callout
- One specific, actionable next step (not "let us know if you have questions")
- Usually: schedule kickoff call, review and approve this document, or provide brand assets
- Mention what happens after that step (agreement issued, deposit invoice, build begins)
