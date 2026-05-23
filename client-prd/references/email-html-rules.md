# Email-Safe HTML Rules

Reference for Claude when writing PRD HTML that must survive copy-paste into Gmail or Outlook.
Read this file completely before writing any HTML for a client PRD.

---

## Why Email HTML Is Different

Gmail and Outlook both strip or ignore large portions of standard web HTML:

| Feature | Gmail | Outlook (desktop) |
|---|---|---|
| `<style>` blocks in `<head>` | Stripped | Stripped |
| `<style>` blocks in `<body>` | Stripped | Stripped |
| External CSS via `<link>` | Stripped | Stripped |
| Google Fonts / web fonts | Stripped | Stripped |
| Inline `style=""` attributes | Preserved | Preserved |
| `<table>` layouts | Preserved | Preserved |
| HTML attributes (`width`, `bgcolor`) | Preserved | Preserved |
| `border-radius` | Preserved | **Ignored** (Word renderer) |
| CSS `background-color` | Preserved | Preserved |
| JavaScript | Stripped | Stripped |
| CSS `display: flex` or `grid` | Unreliable | **Ignored** |
| `@media` queries | Gmail: ignored | Outlook: ignored |

---

## The Four Rules That Cannot Be Broken

**Rule 1: Every style must be inline.**
Every visual property — color, font, padding, margin, border, background — must live inside
the `style=""` attribute of the specific element it styles. No exceptions.

```html
<!-- WRONG -->
<style>.header { background: #003366; }</style>
<div class="header">...</div>

<!-- RIGHT -->
<div style="background:#003366;padding:28px 36px;">...</div>
```

**Rule 2: No external resources.**
No `<link rel="stylesheet">`, no Google Fonts `@import`, no image URLs from external CDNs
that require authentication. Images must be publicly accessible URLs or omitted entirely.

**Rule 3: Tables for multi-column layout.**
Flexbox and CSS Grid are unreliable in email clients. Use `<table>` for any layout that
needs columns. This includes data grids AND two-column meta bars.

```html
<!-- WRONG for email -->
<div style="display:flex;gap:24px;">...</div>

<!-- RIGHT for email -->
<table style="width:100%;border-collapse:collapse;">
  <tr>
    <td style="width:50%;padding:10px;">Left</td>
    <td style="width:50%;padding:10px;">Right</td>
  </tr>
</table>
```

**Rule 4: No CSS classes.**
Gmail rewrites class names and strips associated styles. Never use `class=""` for anything
visual. Use inline styles only.

---

## Web-Safe Font Stacks

Use these exact stacks. Do not invent stacks or reference fonts that aren't installed on
Windows and macOS by default.

| Intent | Stack |
|---|---|
| Body / paragraph text | `Georgia, 'Times New Roman', serif` |
| Labels, UI, metadata | `Arial, Helvetica, sans-serif` |
| Monospace / code | `'Courier New', Courier, monospace` |

If a brand guide specifies a custom font (e.g., Archivo, Inter, Nunito), note it in the
HTML comment at the top but use the closest web-safe fallback in actual elements.
Example comment:
```html
<!-- FONT NOTE: Brand guide specifies Archivo. Falling back to Arial for email compatibility. -->
```

---

## Outlook-Specific Caveats

Outlook desktop (2016–2024) uses Microsoft Word's rendering engine, not a browser.

- `border-radius`: Rendered as square corners. Acceptable on outer wrapper for Gmail/web
  preview, but never use it as the sole visual indicator of a UI element.
- `box-shadow`: Ignored entirely.
- `background-image` on `<div>`: Unreliable. Use `bgcolor` HTML attribute on `<table>` cells
  as a fallback if a colored cell background is critical.
- `max-width` on `<div>`: Usually respected, but wrap in a `<table>` with `width` attribute
  for guaranteed behavior.
- `padding` shorthand: Use `padding-top`, `padding-right`, etc. on `<td>` elements for
  maximum Outlook compatibility. Shorthand is fine on `<div>`.

---

## Proven Safe Patterns

### Colored header band
```html
<div style="background:#003366;padding:28px 36px 24px;">
  <div style="font-family:Arial,Helvetica,sans-serif;font-size:11px;color:#7aabcc;
              letter-spacing:2px;text-transform:uppercase;margin-bottom:6px;">Agency Name</div>
  <div style="font-size:24px;font-weight:700;color:#ffffff;line-height:1.25;">Document Title</div>
</div>
```

### Data table with alternating rows
```html
<table style="width:100%;border-collapse:collapse;font-size:14px;">
  <tr style="background:#f0f4f8;">
    <td style="padding:10px 14px;font-family:Arial,Helvetica,sans-serif;font-weight:700;
               color:#003366;border:1px solid #dde3ea;">Column A</td>
    <td style="padding:10px 14px;font-family:Arial,Helvetica,sans-serif;font-weight:700;
               color:#003366;border:1px solid #dde3ea;">Column B</td>
  </tr>
  <tr>
    <td style="padding:10px 14px;border:1px solid #dde3ea;color:#333;">Value</td>
    <td style="padding:10px 14px;border:1px solid #dde3ea;color:#333;">Value</td>
  </tr>
  <tr style="background:#f9f9f7;">
    <td style="padding:10px 14px;border:1px solid #dde3ea;color:#333;">Value</td>
    <td style="padding:10px 14px;border:1px solid #dde3ea;color:#333;">Value</td>
  </tr>
</table>
```

### Callout / highlight box
```html
<div style="background:#eef5fb;border-left:4px solid #003366;padding:18px 20px;
            margin-bottom:32px;">
  <div style="font-family:Arial,Helvetica,sans-serif;font-size:11px;font-weight:700;
              color:#003366;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:8px;">
    Label
  </div>
  <p style="margin:0;font-size:14px;line-height:1.7;color:#333;">Content here.</p>
</div>
```

### Section heading with rule
```html
<div style="font-family:Arial,Helvetica,sans-serif;font-size:10px;font-weight:700;
            color:#003366;letter-spacing:2px;text-transform:uppercase;
            border-bottom:2px solid #003366;padding-bottom:6px;margin-bottom:14px;">
  01 &nbsp;Section Title
</div>
```

### Meta bar (version, date, status)
Use inline `<span>` elements separated by `margin-right`, inside a light-background `<div>`.
Do not use a table for this — spans are sufficient and cleaner.

---

## Pre-Flight Checklist Comment Block

Every PRD HTML file must begin with this comment block immediately after `<head>`:

```html
<!--
  PRD PRE-FLIGHT CHECKLIST
  Generated by [Your Agency]
  ─────────────────────────────────────────────
  Before sending this email:
  [ ] Client name is correct throughout
  [ ] Project name matches what was discussed
  [ ] Version number and date are current
  [ ] All scope items reflect the actual agreement
  [ ] Open questions are still open (remove any that are resolved)
  [ ] Next step language matches where you are in the conversation
  [ ] Proofread once before pasting into email client
  ─────────────────────────────────────────────
  PASTE INSTRUCTIONS:
  1. Open this file in any web browser
  2. Select All (Cmd+A on Mac / Ctrl+A on Windows)
  3. Copy (Cmd+C / Ctrl+C)
  4. Paste into Gmail or Outlook compose window
  The formatting will carry over automatically.
  ─────────────────────────────────────────────
  FONT NOTE: [note any brand fonts that were replaced with web-safe fallbacks]
  BRAND COLORS: [note primary/accent hex values used]
-->
```
