# GitHub Profile README Redesign -- Design Spec

**Date:** 2026-04-10
**Author:** Sooraj Pandey
**Status:** Approved

## Overview

Complete redesign of the GitHub profile README (soorajpandey/soorajpandey). Replace the existing GPRM-generated template with a custom, dark minimalist luxury profile that showcases a Full-Stack + Cryptography/Privacy + AI technical identity. Maximum animations, clean typography, zero emoji clutter.

## Design Principles

- **Dark minimalist luxury:** Deep blacks (#0d1117), subtle gradients, clean sans-serif typography, premium feel
- **No emojis** in headers or section titles
- **Centered layout** throughout
- **Consistent color accent:** Indigo (#6366f1) across all elements
- **Animation-heavy:** Every section has some form of motion or dynamic generation
- **Self-contained:** Minimize external service dependencies where possible

## Architecture

The profile consists of a single `README.md` file plus supporting assets:

```
soorajpandey/
  README.md              -- Main profile (complete rewrite)
  assets/
    banner.svg           -- Custom animated hero banner
  .github/
    workflows/
      master.yml         -- Snake animation generator (already exists)
```

## Section-by-Section Design

### 1. Hero Banner (Animated SVG)

**File:** `assets/banner.svg`

A custom hand-crafted SVG with embedded CSS animations using `<foreignObject>`:

- **Background:** #0d1117 with animated gradient mesh (dark purple/blue tones, slow CSS keyframe shift)
- **Primary text:** "SOORAJ PANDEY" -- clean sans-serif (system font stack), white (#ffffff), large, centered
- **Subtitle:** "Building Privacy-First Systems" -- smaller, light gray (#8b949e)
- **Accent:** Thin animated border/line with subtle glow pulse effect
- **Dimensions:** Full-width responsive, ~200-250px height
- **File size target:** Under 10KB (optimize with SVGOMG)
- **No external dependencies** -- pure SVG + CSS animation

**Embedding:**
```markdown
<div align="center">
  <img src="./assets/banner.svg" alt="Sooraj Pandey" width="100%" />
</div>
```

### 2. Typing Effect

**Service:** readme-typing-svg by DenverCoder1 (primary choice -- stable, widely used, customizable via URL params). Fallback: readme-SVG-typing-generator if DenverCoder1 service is unavailable.

**Rotating lines:**
1. "Full-Stack Engineer"
2. "Cryptography & Privacy Systems"
3. "AI/ML Integration"
4. "Building @ Zynclave"

**Styling:**
- Font: monospace
- Color: white (#ffffff)
- Background: transparent
- Size: ~22-24px
- Center aligned
- Pause duration: 1500ms between lines

### 3. Bio

Plain markdown text, centered, 2-3 lines. No emojis, no badges.

**Text:**
> Founder at Zynclave. Building privacy-first products across mobile, web, and backend. Specializing in end-to-end encryption, real-time systems, and AI-powered experiences.

### 4. Tech Stack

Uses [skillicons.dev](https://skillicons.dev) for icon rendering (dark theme). Grouped by domain.

**Languages & Frameworks:**
TypeScript, JavaScript, Swift, Kotlin, Rust, Python

**Frontend & Mobile:**
React, Next.js, Tailwind CSS, SwiftUI (text badge), Jetpack Compose (text badge)

**Backend & Infrastructure:**
Node.js, Express, GraphQL, Django, PostgreSQL, MongoDB, Redis, Docker, AWS

**Cryptography & Security (custom shields.io badges):**
Ed25519, Curve25519, Argon2, E2EE, PSI/OPRF

Badge style for crypto: `flat-square`, background `#161b22`, text color `#c9d1d9`, border color matching indigo accent.

**AI & Real-time (mix of icons + badges):**
MediaPipe, LiveKit, Socket.IO

Each group has a minimal header (`###` level) and icons on a single line.

### 5. Featured Projects

HTML table with dark-themed styling (GitHub renders HTML tables natively):

| Project | Description | Tech |
|---------|-------------|------|
| **Vync** | Verified-anonymous social platform with real-time messaging & live streaming | Next.js, GraphQL, LiveKit, SwiftUI |
| **Sanchr** | E2EE messaging & vault with zero-knowledge privacy primitives | Rust, Ed25519, PSI, OPRF, gRPC |
| **LunaBloom** | Privacy-first period tracker -- fully offline, zero network calls | Kotlin, Jetpack Compose, Room |
| **Vitara** | AI-powered fitness companion with pose detection & adaptive coaching | SwiftUI, HealthKit, MediaPipe |

Project names are plain text (bold). No repo links -- these are private/org repos under Zynclave. If any become public later, links can be added.

### 6. GitHub Stats

Three cards using github-readme-stats and github-readme-streak-stats, displayed in a responsive layout using HTML `<div>` and `<img>` tags.

**Consistent theme across all cards:**
- `bg_color=0d1117`
- `text_color=ffffff`
- `icon_color=6366f1` (indigo)
- `border_color=30363d`
- `hide_border=true`
- `ring_color=6366f1`
- `fire=6366f1`

**Layout:**
- Row 1: GitHub Stats + Streak Stats (side by side)
- Row 2: Top Languages (compact layout, centered)

### 7. Contribution Snake

Existing GitHub Action workflow generates the dark snake SVG. Embed:

```markdown
<div align="center">
  <img src="https://raw.githubusercontent.com/soorajpandey/soorajpandey/output/github-snake-dark.svg" alt="Snake animation" />
</div>
```

Verify the workflow is running and the output branch has the latest SVG.

### 8. Footer

**Socials:** Inline shields.io badges, flat-square style, dark themed (#0d1117 background):
- LinkedIn
- X (Twitter)
- Instagram

**Visitor counter:** Minimal dark theme using visitcount.itsvg.in or similar.

**Removed:** Ko-Fi donation section, GPRM credit comment.

## Content Removed (from old profile)

- All emoji-heavy headers
- "About Me" with project list (Vync App, Homeworkly, QRBob)
- Large colored social badges
- GitHub Trophies section
- Top Contributed Repo section
- Ko-Fi donation badge
- GPRM attribution comment

## Files to Create/Modify

1. **CREATE** `assets/banner.svg` -- Custom animated hero banner
2. **REWRITE** `README.md` -- Complete replacement with new design
3. **KEEP** `.github/workflows/master.yml` -- Snake workflow (verify it works)

## Testing

- Preview rendered README on GitHub (push to branch, check rendering)
- Verify SVG banner animates in GitHub's renderer (GitHub strips JavaScript but allows CSS animations in SVG `<foreignObject>`)
- Verify snake animation SVG loads from output branch
- Check dark mode / light mode appearance (design targets dark mode primarily)
- Validate all external service URLs (typing SVG, stats, streak, skillicons)

## Constraints

- GitHub README renderer strips `<script>` tags -- all animation must be CSS-only
- SVG `<foreignObject>` is supported but some CSS properties may not render
- Maximum file sizes should be reasonable (banner SVG under 10KB)
- External service availability: typing-svg, github-readme-stats, streak-stats, skillicons.dev
- Contribution snake depends on GitHub Action running successfully
