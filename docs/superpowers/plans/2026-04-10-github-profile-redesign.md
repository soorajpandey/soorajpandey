# GitHub Profile README Redesign -- Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the generic GPRM-generated GitHub profile with a custom dark minimalist luxury README featuring animated SVG banner, typing effect, crypto/AI tech stack, featured projects, GitHub stats, and contribution snake.

**Architecture:** Single `README.md` rewrite plus one new `assets/banner.svg` file. All animations are CSS-only (no JavaScript -- GitHub strips `<script>` tags). External services: readme-typing-svg (typing effect), github-readme-stats (stats cards), github-readme-streak-stats (streak card), skillicons.dev (tech icons), shields.io (custom badges). Existing snake workflow on `output` branch is reused.

**Tech Stack:** SVG with CSS animations, GitHub-flavored Markdown, HTML (for layout), shields.io badges, skillicons.dev

---

## File Structure

```
soorajpandey/
  README.md                    -- Complete rewrite (all 8 sections from spec)
  assets/
    banner.svg                 -- New: custom animated hero banner (~250px tall, dark gradient, CSS animation)
  .github/
    workflows/
      master.yml               -- Existing: snake animation generator (no changes needed)
```

---

### Task 1: Create the animated SVG hero banner

**Files:**
- Create: `assets/banner.svg`

- [ ] **Step 1: Create the assets directory**

```bash
mkdir -p assets
```

- [ ] **Step 2: Create `assets/banner.svg`**

Write this file with the complete animated SVG. Uses `<foreignObject>` for HTML/CSS inside SVG. CSS keyframes handle the gradient animation and glow pulse. No JavaScript.

```svg
<svg width="100%" height="250" viewBox="0 0 1200 250" fill="none" xmlns="http://www.w3.org/2000/svg">
  <foreignObject width="100%" height="100%">
    <div xmlns="http://www.w3.org/1999/xhtml">
      <style>
        @keyframes gradientShift {
          0% { background-position: 0% 50%; }
          50% { background-position: 100% 50%; }
          100% { background-position: 0% 50%; }
        }
        @keyframes glowPulse {
          0%, 100% { box-shadow: inset 0 0 30px rgba(99, 102, 241, 0.08), 0 0 15px rgba(99, 102, 241, 0.05); }
          50% { box-shadow: inset 0 0 60px rgba(99, 102, 241, 0.15), 0 0 30px rgba(99, 102, 241, 0.1); }
        }
        @keyframes subtleFade {
          0%, 100% { opacity: 0.85; }
          50% { opacity: 1; }
        }
        .banner {
          width: 100%;
          height: 250px;
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
          background: linear-gradient(135deg, #0d1117 0%, #161b22 25%, #1a1040 50%, #0d1117 75%, #111827 100%);
          background-size: 400% 400%;
          animation: gradientShift 15s ease infinite, glowPulse 4s ease-in-out infinite;
          border-bottom: 1px solid rgba(99, 102, 241, 0.2);
          font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
          box-sizing: border-box;
          position: relative;
          overflow: hidden;
        }
        .banner::before {
          content: '';
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          background: radial-gradient(ellipse at 30% 50%, rgba(99, 102, 241, 0.06) 0%, transparent 70%),
                      radial-gradient(ellipse at 70% 50%, rgba(129, 140, 248, 0.04) 0%, transparent 70%);
          pointer-events: none;
        }
        .name {
          font-size: 42px;
          font-weight: 700;
          color: #ffffff;
          letter-spacing: 6px;
          text-transform: uppercase;
          margin: 0;
          z-index: 1;
          animation: subtleFade 6s ease-in-out infinite;
        }
        .subtitle {
          font-size: 16px;
          font-weight: 400;
          color: #8b949e;
          letter-spacing: 3px;
          text-transform: uppercase;
          margin-top: 12px;
          z-index: 1;
        }
        .accent-line {
          width: 60px;
          height: 2px;
          background: linear-gradient(90deg, transparent, #6366f1, transparent);
          margin-top: 16px;
          z-index: 1;
          animation: subtleFade 4s ease-in-out infinite;
        }
      </style>
      <div class="banner">
        <div class="name">Sooraj Pandey</div>
        <div class="subtitle">Building Privacy-First Systems</div>
        <div class="accent-line"></div>
      </div>
    </div>
  </foreignObject>
</svg>
```

- [ ] **Step 3: Verify the SVG renders locally**

Open `assets/banner.svg` in a browser to confirm:
- Dark gradient background animates (slow color shift)
- "SOORAJ PANDEY" in white, large, centered
- "Building Privacy-First Systems" in gray below
- Indigo accent line with fade animation
- Subtle glow pulse on the container

```bash
open assets/banner.svg  # macOS
```

- [ ] **Step 4: Commit the banner**

```bash
git add assets/banner.svg
git commit -m "feat: add custom animated SVG hero banner"
```

---

### Task 2: Write the complete README.md -- Sections 1-4 (Banner, Typing, Bio, Tech Stack)

**Files:**
- Rewrite: `README.md`

- [ ] **Step 1: Replace `README.md` with sections 1-4**

Write the first half of the README. This includes the hero banner embed, typing effect, bio, and tech stack with all icon URLs.

```markdown
<div align="center">
  <img src="./assets/banner.svg" alt="Sooraj Pandey" width="100%" />
</div>

<div align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=22&pause=1500&color=FFFFFF&center=true&vCenter=true&random=false&width=500&lines=Full-Stack+Engineer;Cryptography+%26+Privacy+Systems;AI%2FML+Integration;Building+%40+Zynclave" alt="Typing SVG" />
  </a>
</div>

<br/>

<div align="center">
  <i>Founder at Zynclave. Building privacy-first products across mobile, web, and backend.<br/>Specializing in end-to-end encryption, real-time systems, and AI-powered experiences.</i>
</div>

<br/>

---

### Languages

<div align="center">
  <img src="https://skillicons.dev/icons?i=ts,js,swift,kotlin,rust,python&theme=dark" alt="Languages" />
</div>

### Frontend & Mobile

<div align="center">
  <img src="https://skillicons.dev/icons?i=react,nextjs,tailwind&theme=dark" alt="Frontend" />
  &nbsp;&nbsp;
  <img src="https://img.shields.io/badge/SwiftUI-000000?style=flat-square&logo=swift&logoColor=F05138" alt="SwiftUI" />
  <img src="https://img.shields.io/badge/Jetpack_Compose-4285F4?style=flat-square&logo=jetpackcompose&logoColor=white" alt="Compose" />
</div>

### Backend & Infrastructure

<div align="center">
  <img src="https://skillicons.dev/icons?i=nodejs,express,graphql,django,postgres,mongodb,redis,docker,aws&theme=dark" alt="Backend" />
</div>

### Cryptography & Security

<div align="center">
  <img src="https://img.shields.io/badge/Ed25519-161b22?style=flat-square&logoColor=c9d1d9&color=161b22" alt="Ed25519" />
  <img src="https://img.shields.io/badge/Curve25519-161b22?style=flat-square&logoColor=c9d1d9&color=161b22" alt="Curve25519" />
  <img src="https://img.shields.io/badge/Argon2-161b22?style=flat-square&logoColor=c9d1d9&color=161b22" alt="Argon2" />
  <img src="https://img.shields.io/badge/E2EE-161b22?style=flat-square&logoColor=c9d1d9&color=161b22" alt="E2EE" />
  <img src="https://img.shields.io/badge/PSI%2FOPRF-161b22?style=flat-square&logoColor=c9d1d9&color=161b22" alt="PSI/OPRF" />
</div>

### AI & Real-time

<div align="center">
  <img src="https://img.shields.io/badge/MediaPipe-0097A7?style=flat-square&logo=google&logoColor=white" alt="MediaPipe" />
  <img src="https://img.shields.io/badge/LiveKit-FF4785?style=flat-square&logoColor=white" alt="LiveKit" />
  <img src="https://skillicons.dev/icons?i=socketio&theme=dark&perline=1" alt="Socket.IO" height="48" />
</div>
```

- [ ] **Step 2: Commit sections 1-4**

```bash
git add README.md
git commit -m "feat: rewrite README with banner, typing, bio, and tech stack"
```

---

### Task 3: Write README.md -- Sections 5-8 (Projects, Stats, Snake, Footer)

**Files:**
- Modify: `README.md` (append to existing content from Task 2)

- [ ] **Step 1: Append sections 5-8 to `README.md`**

Add the featured projects table, GitHub stats cards, contribution snake, and footer below the tech stack section.

```markdown

---

### Featured Projects

<div align="center">

| Project | Description | Tech |
|:--------|:------------|:-----|
| **Vync** | Verified-anonymous social platform with real-time messaging & live streaming | Next.js, GraphQL, LiveKit, SwiftUI |
| **Sanchr** | E2EE messaging & vault with zero-knowledge privacy primitives | Rust, Ed25519, PSI, OPRF, gRPC |
| **LunaBloom** | Privacy-first period tracker -- fully offline, zero network calls | Kotlin, Jetpack Compose, Room |
| **Vitara** | AI-powered fitness companion with pose detection & adaptive coaching | SwiftUI, HealthKit, MediaPipe |

</div>

---

### GitHub Stats

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=soorajpandey&show_icons=true&include_all_commits=true&count_private=true&bg_color=0d1117&text_color=ffffff&icon_color=6366f1&title_color=ffffff&hide_border=true&ring_color=6366f1" alt="GitHub Stats" height="180" />
  &nbsp;&nbsp;&nbsp;
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=soorajpandey&background=0d1117&stroke=30363d&ring=6366f1&fire=6366f1&currStreakNum=ffffff&sideNums=ffffff&currStreakLabel=8b949e&sideLabels=8b949e&dates=8b949e&hide_border=true" alt="Streak Stats" height="180" />
</div>

<br/>

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=soorajpandey&layout=compact&include_all_commits=true&count_private=true&bg_color=0d1117&text_color=ffffff&icon_color=6366f1&title_color=ffffff&hide_border=true" alt="Top Languages" height="180" />
</div>

---

### Contribution Graph

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/soorajpandey/soorajpandey/output/github-snake-dark.svg" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/soorajpandey/soorajpandey/output/github-snake.svg" />
    <img alt="Snake animation" src="https://raw.githubusercontent.com/soorajpandey/soorajpandey/output/github-snake-dark.svg" />
  </picture>
</div>

---

<div align="center">
  <a href="https://linkedin.com/in/soorajpandey001">
    <img src="https://img.shields.io/badge/LinkedIn-0d1117?style=flat-square&logo=linkedin&logoColor=8b949e" alt="LinkedIn" />
  </a>
  &nbsp;
  <a href="https://x.com/soorajpandey001">
    <img src="https://img.shields.io/badge/X-0d1117?style=flat-square&logo=x&logoColor=8b949e" alt="X" />
  </a>
  &nbsp;
  <a href="https://instagram.com/sooraj_pandey_">
    <img src="https://img.shields.io/badge/Instagram-0d1117?style=flat-square&logo=instagram&logoColor=8b949e" alt="Instagram" />
  </a>
</div>

<br/>

<div align="center">
  <img src="https://visitcount.itsvg.in/api?id=soorajpandey&label=Profile%20Views&color=6&icon=1&pretty=true" alt="Profile Views" />
</div>
```

- [ ] **Step 2: Commit sections 5-8**

```bash
git add README.md
git commit -m "feat: add projects, stats, snake, and footer to README"
```

---

### Task 4: Verify snake workflow and final review

**Files:**
- Read-only check: `.github/workflows/master.yml`
- Read-only check: output branch files

- [ ] **Step 1: Verify snake SVG files exist on the output branch**

```bash
git ls-tree origin/output
```

Expected output should include:
- `github-snake.svg`
- `github-snake-dark.svg`
- `ocean.gif`

These files already exist (verified during planning).

- [ ] **Step 2: Verify the workflow file is correct**

Read `.github/workflows/master.yml` and confirm:
- Triggers on push and schedule (hourly cron)
- Uses `Platane/snk@v3`
- Outputs both light and dark SVGs to `dist/`
- Pushes to `output` branch via `crazy-max/ghaction-github-pages@v3.1.0`

No changes needed -- workflow is already configured correctly.

- [ ] **Step 3: Open the SVG banner in a browser for final visual check**

```bash
open assets/banner.svg
```

Confirm: gradient animates, text is visible, glow pulse works, accent line fades.

- [ ] **Step 4: Review the full README.md for completeness**

Read through the entire README and verify all 8 sections are present in order:
1. Hero banner (SVG embed)
2. Typing effect (demolab.com URL)
3. Bio (centered italic text)
4. Tech stack (5 subsections with icons/badges)
5. Featured projects (4-row table)
6. GitHub stats (3 cards)
7. Contribution snake (picture element with light/dark sources)
8. Footer (3 social links + visitor counter)

- [ ] **Step 5: Push to a branch for GitHub preview**

```bash
git push origin master
```

Then visit https://github.com/soorajpandey to verify:
- Banner SVG renders and animates
- Typing SVG cycles through all 4 lines
- Skillicons load correctly
- Shields.io crypto badges render with dark background
- GitHub stats cards show data with correct theme
- Snake SVG loads from output branch
- Social links in footer work
- Visitor counter renders

---

### Task 5: Fix any rendering issues (conditional)

This task only applies if GitHub's preview reveals problems.

**Common issues and fixes:**

- [ ] **If SVG banner doesn't animate:** GitHub may strip some CSS properties. Simplify the `@keyframes` rules -- remove `box-shadow` animations, keep only `background-position` shifts. Test with minimal CSS and add back properties one at a time.

- [ ] **If `<foreignObject>` doesn't render text:** Replace with native SVG `<text>` elements instead:
```svg
<text x="600" y="110" text-anchor="middle" fill="#ffffff" font-size="42" font-weight="700" font-family="-apple-system, sans-serif" letter-spacing="6">SOORAJ PANDEY</text>
<text x="600" y="145" text-anchor="middle" fill="#8b949e" font-size="16" font-weight="400" font-family="-apple-system, sans-serif" letter-spacing="3">BUILDING PRIVACY-FIRST SYSTEMS</text>
```

- [ ] **If skillicons.dev returns wrong/missing icons:** Check available icons at `https://skillicons.dev/icons?i=LIST&theme=dark`. Replace unsupported icons with shields.io badges using the same dark style.

- [ ] **If stats cards don't load:** The vercel.app instances can be slow or rate-limited. Wait and refresh. If persistent, consider deploying a personal instance of github-readme-stats.
