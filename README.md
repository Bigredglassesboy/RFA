# RFA: Regenerative Fashion Archive

The RFA maps fashion research by UN Sustainable Development Goal. Each research project is one dot, coloured by its SDG, and you can search and filter the whole archive in the browser or walk through it in a physical room.

Built by [BRGB Studio](https://brgb.uk) with the University of East London. The research comes from BA and MA Fashion students, BA Game Design students, and industry and community partners.

## Pages

| Page | What's there |
|------|--------------|
| [`/`](https://bigredglassesboy.github.io/RFA/) | The particle sea: search, SDG filters, webcam body tracking |
| [`/room3d/`](https://bigredglassesboy.github.io/RFA/room3d/) | A 3D model of the research room you can walk around |
| [`/room/`](https://bigredglassesboy.github.io/RFA/room/) | Room setup notes: projectors, Kinects, installation |
| [`/how/`](https://bigredglassesboy.github.io/RFA/how/) | How the system fits together |

## The particle sea `/`

Every dot on screen is a research project, tagged with one or more SDGs.

- Move the mouse and the dots drift towards it
- Turn on the webcam and your body pushes the dots aside, while your wrists pull them in
- Click one of the 17 SDG buttons to show only that goal's projects
- Type in the search bar to find projects by title, department or keyword
- Hover over a dot to see its title, department and SDGs
- Open **Distribution** to change how many projects sit under each goal

Body tracking uses MediaPipe Pose, loaded from a CDN. If that fails to load, the mouse stands in for the body.

The archive currently runs on placeholder projects. The live version will pull from a CKAN instance through its `package_search` API, checking for new projects every 30 seconds.

## The research room `/room3d/`

The archive is designed to fill an 8m × 6m room. Four projectors hang in a cluster from the centre of the ceiling, one aimed at each wall, so the dots cover all four walls. A PC in the middle of the room runs the search, and a small SDG bar chart sits on the east wall.

The 3D model lets you try this before it's built:

- Drag to look around, scroll or pinch to zoom
- Switch between the **Wide**, **Visitor**, **PC**, **Dollhouse** and **Plan** views
- Search and filter as you would on the main page. Matching dots light up and the rest fade, and the bar chart and PC screen follow along.
- Tap the floor to move the visitor. They cast a shadow on the wall they face, the dots move out of the way of their body, and they gather around the raised hand.
- Tap a dot to see its project

It works best on a laptop. It loads three.js and its font online, so open it through GitHub Pages or a local server, not by double-clicking the file.

## How it fits together `/how/`

A clickable diagram of the whole system:

1. A research idea plus research and collaboration
2. Siemens CKAN, then AWS, then Unreal Engine 5
3. Four outputs: shared exhibitions, the immersive room, AI accessibility, and labs and conferences

## The Unreal Engine 5 build

The physical room is being built in UE5:

- A C++ `AResearchRoomManager` that polls CKAN, parses the JSON, runs the particle sea and handles search
- 17 Niagara systems, one per SDG, with persistent dots that drift
- Two Azure Kinects for skeleton tracking. The body pushes dots aside and the hands pull them in.
- Four projectors in the ceiling cluster, one per wall, driven through nDisplay
- The PC station, with UMG search, SDG filter buttons and project cards
- The SDG bar chart inset on the east wall, which updates with each search
- CKAN datasets tagged `sdg-1` to `sdg-17`, read through `package_search`

The setup guide, C++ source, Niagara spec and Blueprint graphs are in `SDGResearchRoomUE.jsx`.

## SDG colours

Goal names and colours follow the [UN SDG Brand Guidelines 2023](https://www.un.org/sustainabledevelopment/).

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

## Built with

**Web:** plain HTML, CSS and JavaScript with no build step and one file per page. MediaPipe Pose for body tracking, Canvas 2D for the particle sea, three.js for the 3D room, hosted on GitHub Pages.

**Unreal:** UE 5.3+ with C++, Niagara, UMG and nDisplay. Azure Kinect SDK, the CKAN REST API, and AWS (EC2, S3, CloudFront, Lambda, RDS).

## Credits

Pat Quinnell, BRGB Studio, with the University of East London.
[brgb.uk](https://brgb.uk) · [@bigredglassesboy](https://instagram.com/bigredglassesboy)
