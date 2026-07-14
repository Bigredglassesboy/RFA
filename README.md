# RFA — Regenerative Fashion Archive
### Digital Research Room · Connected Visualiser · SDG Particle Sea

A live interactive research visualisation system built by [BRGB Studio](https://bigredglassesboy.com) for the University of East London. Research projects are pulled from a CKAN open data backend, colour-coded by UN Sustainable Development Goal, and rendered as a navigable particle sea — in browser and in Unreal Engine 5.

---

## Pages

| URL | What it is |
|-----|-----------|
| [`/`](https://bigredglassesboy.github.io/RFA/) | Homepage |
| [`/room/`](https://bigredglassesboy.github.io/RFA/room/) | SDG Research Room — interactive particle sea with webcam body tracking |
| [`/how/`](https://bigredglassesboy.github.io/RFA/how/) | Connected Visualiser — system architecture diagram |

---

## SDG Research Room `/room/`

A full-screen interactive particle sea where every dot is a fashion research project tagged with one or more UN SDGs.

**Interaction**
- Move your mouse across the sea to attract particles
- Enable the webcam — your body silhouette displaces the sea, wrists attract particle clusters
- Click any of the 17 SDG buttons to filter by goal
- Type in the search bar to surface matching research projects
- Hover any particle for a floating project card — title, department, SDG tags
- Use the **⊞ Distribution** panel to adjust how many projects appear per SDG

**Body tracking**
Tries to load MediaPipe Pose from CDN for real skeleton tracking. Falls back to mouse-driven demo mode if unavailable.

**Data**
Currently running on placeholder fashion research data. Production version connects to a CKAN open data instance via the `package_search` API, polling every 30 seconds.

---

## Connected Visualiser `/how/`

An interactive diagram showing the full system architecture — from research idea through infrastructure to output channels.

Click any node to expand:

- **Idea + Research & Collaboration** — the input layer
- **Siemens / CKAN → AWS → Unreal Engine 5** — the infrastructure pipeline
- **Shared Exhibition · Immersive Experience · AI Accessibility · Lab & Conferences** — the four output channels

---

## Unreal Engine 5 Build

The production installation runs in UE5 with:

- **C++ `AResearchRoomManager`** — HTTP polling, JSON parsing, particle sea lifecycle, search logic
- **17 Niagara particle systems** — one per UN SDG, CPU sim, persistent dots with drift
- **Azure Kinect (×2)** — skeleton tracking, silhouette displacement, hand attraction
- **4× short-throw projectors** — floor particle sea via nDisplay
- **UMG search panel** — keyword search, SDG filter buttons, floating project cards
- **Wall display** — GPU Niagara constellation, live SDG bar chart, project title scroller
- **CKAN backend** — datasets tagged `sdg-1` … `sdg-17`, polled via `package_search`

Full setup guide, C++ source, Niagara spec, Blueprint event graphs, and Go Live checklist in `SDGResearchRoomUE.jsx`.

---

## UN SDG Colour Reference

All 17 goal colours are sourced from the official [UN SDG Brand Guidelines 2023](https://www.un.org/sustainabledevelopment/).

| # | Goal | Hex |
|---|------|-----|
| 1 | No Poverty | `#E5243B` |
| 2 | Zero Hunger | `#DDA63A` |
| 3 | Good Health and Well-Being | `#4C9F38` |
| 4 | Quality Education | `#C5192D` |
| 5 | Gender Equality | `#FF3A21` |
| 6 | Clean Water and Sanitation | `#26BDE2` |
| 7 | Affordable and Clean Energy | `#FCC30B` |
| 8 | Decent Work and Economic Growth | `#A21942` |
| 9 | Industry, Innovation and Infrastructure | `#FD6925` |
| 10 | Reduced Inequalities | `#DD1367` |
| 11 | Sustainable Cities and Communities | `#FD9D24` |
| 12 | Responsible Consumption and Production | `#BF8B2E` |
| 13 | Climate Action | `#3F7E44` |
| 14 | Life Below Water | `#0A97D9` |
| 15 | Life on Land | `#56C02B` |
| 16 | Peace, Justice and Strong Institutions | `#00689D` |
| 17 | Partnerships for the Goals | `#19486A` |

---

## Tech Stack

**Web previs**
- Vanilla HTML/CSS/JS — no build step, single file per page
- MediaPipe Pose (CDN) — body tracking
- Canvas 2D — particle physics, floor projection, atmosphere
- GitHub Pages — hosting

**Unreal Engine build**
- UE 5.3+, C++, Niagara, UMG
- Azure Kinect SDK
- CKAN REST API
- AWS (EC2, S3, CloudFront, Lambda, RDS)
- nDisplay (multi-projector output)

---

## Project

Built by **Pat Quinnell / BRGB Studio** · University of East London  
[bigredglassesboy.com](https://bigredglassesboy.com) · [@Bigredglassesboy](https://instagram.com/bigredglassesboy)
