# UI Restyle — Auto Scaling Demo Page

**Date:** 2026-05-14
**Status:** Approved

## Summary

Restyle the HTML page served by EC2 instances in `template.yaml`. No new functionality — same two sections, clean visual upgrade.

## Decisions

| Decision | Choice |
|---|---|
| Visual style | Clean Light (white cards, slate palette, `#f8fafc` page background) |
| Accent color | Orange `#f97316` / hover `#ea580c` |
| Implementation | Inline CSS inside UserData heredoc |
| Content changes | Remove description and note text from CPU Stress Test card |

## Target File

`template.yaml` — `LaunchTemplate.Properties.LaunchTemplateData.UserData` heredoc (lines 249–293).

## Layout

```
[ ● Auto Scaling Demo          ↻ 5s ]

┌─ INSTANCE INFORMATION ──────────────┐
│ Instance ID   i-0abc123def456789    │
│ Private IP    10.0.3.42             │
│ Availability Zone  [us-east-1a]     │
└─────────────────────────────────────┘

┌─ CPU STRESS TEST ───────────────────┐
│  [ 🔥 Trigger CPU Stress ]          │
└─────────────────────────────────────┘
```

## CSS Palette

| Token | Value | Usage |
|---|---|---|
| Page bg | `#f8fafc` | `<body>` background |
| Card bg | `#ffffff` | Card background |
| Border | `#e2e8f0` | Card borders, dividers |
| Title text | `#0f172a` | Page title, values |
| Label text | `#64748b` | Row labels |
| Muted text | `#94a3b8` | Card section headings, refresh badge |
| Accent | `#f97316` | Stress button, AZ badge text/border |
| AZ badge bg | `#fff7ed` | AZ badge background |
| Status dot | `#22c55e` | Green dot in header |

## Components

**Header** — green status dot + bold page title + right-aligned `↻ 5s` refresh badge (driven by existing `<meta http-equiv="refresh" content="5">`).

**Instance Information card** — three rows (Instance ID, Private IP, Availability Zone). Values right-aligned. Instance ID and Private IP in monospace. AZ rendered as orange pill badge.

**CPU Stress Test card** — section heading + full-width orange button only. No description text, no note text.

## What Does NOT Change

- Apache setup, CGI script, `/stress` alias — untouched
- `sed` placeholder substitution for `INSTANCE_ID`, `PRIVATE_IP`, `AZ` — untouched
- Auto-refresh interval (5s) — untouched
- All CloudFormation resources outside `UserData` — untouched
