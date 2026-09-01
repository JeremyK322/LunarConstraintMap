# Lunar Constraint Map

## Making Due Regard Visible

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Three.js](https://img.shields.io/badge/Three.js-r160-000000.svg)](https://threejs.org/)
[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)](https://github.com/jeremyk322/LunarConstraintMap)

An open, public map of the Moon that makes due regard visible.

The map is an interactive 3D web application that visualizes spatial constraints, heritage sites, resource zones, and regulatory status across the lunar surface. It overlays every known category of lunar constraint on a single spatial reference frame, making the spatial dimension of existing legal obligations legible. It does not create new law. It does not enforce anything. It turns on the lights.

**Live Demo:** [https://jeremyk322.github.io/LunarConstraintMap/](https://jeremyk322.github.io/LunarConstraintMap/)

---

## Overview

The Moon is not crowded yet, but it will be. The most contested assets are not only water ice and metals. They are landing sites, stable orbits, radio-quiet zones, sites of scientific interest, heritage, view, spectrum. These are resources in every meaningful sense, and they are already scarce.

The Lunar Constraint Map (LCM) makes the spatial dimension of existing legal obligations visible. It serves as a shared reference frame for international coordination, operationalizing what already exists in the Outer Space Treaty framework.

---

## Features

### 3D Globe Navigation
- Rotate: Click and drag with left mouse button
- Zoom: Scroll wheel
- Touch: Drag to rotate, pinch to zoom
- Crosshair: Targeting reticle at screen center (toggle in Settings)

### Layers Panel

The layers panel provides resource category filtering and master governance overlays for regulatory and technical evaluation:

**Physical Features** (Maria, Major Craters, Mountain Ranges, Basins, Valleys)
**Extractable** (Water Ice PSR, Helium-3 Regions, Mineral & Metal Regions)
**Spatial** (Landing Sites, Launch Sites, Orbits, Lagrange Points)
**Environmental** (PSR Fragile, High Scientific Interest, Radio Quiet Zone, Contamination-Sensitive)
**Heritage** (Historic spacecraft and impact locations)
**Intangible** (Political Sites, Scientific Data Value)

Orbit feature navigation: Click any orbit feature (e.g., Gateway / NRHO Orbit) in the layer menu to frame the full orbital trajectory at distance 6.5, highlight orbital satellites, and generate reports without requiring surface Lat/Lon coordinates.

### Governance Overlays

| Overlay | Description |
|---------|-------------|
| **Assessment Status** | Renders confidence in the existing record across four states: Unassessed, Under Assessment, Assessed Open, Assessed Protected. Sites under active review carry provisional protection notices requiring public justification before proceeding. Assessment status is metadata about the record, not a verdict on the ground. |
| **Operational Activity** | Displays planned and active lunar missions with surface operating radii. Where footprints overlap, the map renders the intersection with a neutral hatched pattern and opens an Article IX coordination note in the sidebar. The overlap is a fact to be examined, not a fault to be flagged. |
| **Dynamic Harms** | Computes procedural environmental footprints for Plume Surface Interaction (PSI-v1.2), Volatile Contamination (CONTAM-v1.0), and Transient EMI (EMI-v1.1) attached to operating assets. Off by default. |
| **Disputes and Salience** | Challenged designations carry a small corner mark. The dispute register shows the challenger, the justification, and the response deadline. Visual weight by stroke thickness and dash style reflects whether a designation has survived challenge. No recency badges. |

### Planning Mode

Click the **Plan** button to plan a site at your current camera location. Move the camera to your desired landing location using orbit and zoom controls. Click "Plan" to open the planning form with current coordinates pre-filled.

Fill in the details: Name, Actor, State Party, Radius, Color, Tier, Description. The State Party is a free-text field - type any country or entity responsible under Article VI. Tier selection determines priority (Tier 1 = highest, Tier 3 = lowest). Click "Check Conflicts & Place" to generate a conflict report. Review the OST analysis showing Articles 6, 9, and 11 implications. Confirm to place the site at your camera's location. Manage sites from the Planning section in the Layers panel. Data persistence: Your planned sites are saved in local storage.

**Tier System:**
- Tier 1 - Critical constraints requiring mandatory Article IX consultation
- Tier 2 - Significant interests requiring due regard and coordination
- Tier 3 - General activities with standard Article XI notification

### Information Panels

| Panel | Content |
|-------|---------|
| **Bottom-Right Telemetry HUD** | Feature name, category, tier or status, and state responsible at the screen center. Overlapping features at the center point are listed with an Article IX coordination note. |
| **State Legend** | Article VI State Parties color-coded by responsibility |

### Feature Reports

The popup shows four things: the feature name, its category, its tier, and what that tier means.

The Report button freezes the map and opens the full record, including:
- Source and evidence grade (A/B/C)
- Assessment status and date
- Designation authority
- State responsibility under Article VI
- Applicable legal instruments
- Dispute status and details
- Plain language summary

The report opens in a new window and can be printed or copied. Every report ends with the honesty footer: *Absence from this report does not mean an area is free of constraint. This report is a rendering of the current record, not a legal determination.*

---

## Technology Stack

| Technology | Purpose |
|------------|---------|
| Three.js (r160) | 3D rendering engine |
| OrbitControls | Camera navigation and interaction |
| GLTFLoader | Custom lunar mesh loading |
| HTML5 / CSS3 | UI and styling |
| ES Modules | Modular JavaScript architecture |
| Local Storage | User site persistence |

---

## Project Structure

```
LunarConstraintMap/
├── index.html                      # Main application
├── moonLayers.js                   # Feature data, layer definitions, state definitions
├── README.md                       # This file

```

---

## Data Model

### Features

Every feature in the LCM carries structured metadata:

```javascript
{
  "id": "apollo_11",
  "name": "Apollo 11 (Tranquility Base)",
  "lat": 0.674,
  "lon": 23.473,
  "radius_km": 10,
  "tier": 1,                    // 1=Protected, 2=Coordination Required, 3=Open
  "state": "USA",               // Article VI responsible State
  "articles": [6, 9],           // Relevant OST articles
  "tags": ["heritage", "crewed"],
  "source": "NASA Apollo Mission Report",
  "evidence_grade": "A",        // A=Direct measurement, B=Regulatory, C=Unverified
  "review_status": "assessed_protected",
  "assessed_on": "pending",
  "event_date": "1969-07-20",
  "designation_authority": "Proposed by map contributors",
  "disputed": false,
  "dispute_details": null,
  "mission_status": "completed"
}
```

### State Parties

Supports Article VI responsibility mapping:

| State | Color |
|-------|-------|
| United States | #2b82c9 |
| Russia (successor to USSR) | #cc0000 |
| Russian Federation | #e63946 |
| China (CNSA) | #ffb703 |
| India (ISRO) | #fb8500 |
| Japan (JAXA / Commercial) | #ff4d6d |
| South Korea (KARI) | #00a896 |
| ESA (Member States) | #00b4d8 |
| Israel | #48cae4 |
| Pakistan (SUPARCO) | #2a9d8f |

---

## User Guide

### Basic Controls

| Action | Control |
|--------|---------|
| Rotate globe | Click + drag |
| Zoom | Scroll wheel |
| Reset view | Settings → Reset View |
| Auto-rotate | Settings → Auto-rotate toggle |
| Lock poles | Settings → Lock N/S Pole |
| Crosshair | Settings → Crosshair toggle |
| Surface Click Selection | Settings → Surface Click Selection toggle |

### Planning a Site

1. Navigate to your desired location using orbit controls
2. Click the Plan button
3. Fill in the form:
   - Site Name (required)
   - Actor / Operator (required)
   - State Party (Article VI responsibility - free text)
   - Latitude (auto-filled from camera position)
   - Longitude (auto-filled from camera position)
   - Radius (km) (default: 5)
   - Color (default: #00ff88)
   - Constraint Tier (1, 2, or 3)
   - Description
   - Notes
4. Click Check Conflicts & Place
5. Review the OST analysis report showing Articles 6, 9, and 11 implications
6. Confirm to place the site

### Generating Reports

- Click on any feature on the Moon (Surface Click Selection must be enabled in Settings)
- The popup shows name, category, tier, and meaning
- Click Report for the full record
- Reports can be printed or copied

### Layer Management

- Global checkbox: Toggle all resource layers on or off simultaneously without resetting governance modes
- Category accordion: Expand or collapse resource categories
- Discs toggle: Toggle visual 3D surface discs for each category independently
- Feature-level toggles: Individual feature visibility
- Governance overlays: Assessment Status, Operational Activity, Dynamic Harms, Disputes
- Orbit Feature Navigation: Click any orbit feature to frame the full orbital trajectory

---

## Data Sources

Each feature carries a source field. Key sources include:

| Source | Description |
|--------|-------------|
| IAU Gazetteer of Planetary Nomenclature | Official planetary feature names and locations |
| NASA / LRO LOLA / GRAIL | Topographic and gravity data |
| CNSA Mission Briefings | Chinese lunar exploration documentation |
| ISRO Mission Reports | Indian Space Research Organisation data |
| ESA Science Operations | European Space Agency mission data |
| NASA CLPS Program Office | Commercial Lunar Payload Services documentation |
| JAXA Press Releases | Japanese Aerospace Exploration Agency data |
| ITU Radio Regulations | Spectrum protection for radio astronomy |
| COPUOS Conference Room Papers | UN Committee on the Peaceful Uses of Outer Space |

---

## Legal Foundation

The Lunar Constraint Map operationalizes existing international law — it does not create new law.

### Outer Space Treaty (OST) Framework

| Article | Provision | Application |
|---------|-----------|-------------|
| **Article VI** | States bear international responsibility for national activities in space | Every feature carries its responsible State Party |
| **Article IX** | Due regard for other states' interests; consultation required for harmful interference | Overlap detection and coordination awareness |
| **Article XI** | Information sharing with UN Secretary-General and scientific community | Public baseline for transparency |

A state cannot have reason to believe it will interfere with something it cannot see. The map makes the reason to believe visible.

---

## Research Context

The framework is presented in the paper:

**"Making Due Regard Visible: A Constraint Mapping Framework for Lunar Governance"**

Accepted for the **25th Australian Space Research Conference**
*29 September – 1 October 2026, Adelaide*

Full text to follow after the conference.

---

## Contributing

We welcome contributions. Please review the guidelines below.

### Ways to Contribute
- Add or update feature data
- Improve UI/UX
- Fix bugs
- Enhance documentation
- Add new features or layers

### Data Contribution Guidelines
1. Source every feature with a verifiable reference
2. Include evidence grade: A (direct measurement), B (regulatory), C (unverified)
3. Specify review status: unassessed, under_assessment, assessed_open, assessed_protected
4. Identify State responsibility under Article VI where applicable
5. Note disputes and designation authority

---

## License

This project is licensed under the MIT License.

---

## Citation

If you use this work in research or derivative projects, please cite it as:

```
Lunar Constraint Map (Version 2.0.0) [Software]. (2026).
Available at: https://github.com/jeremyk322/LunarConstraintMap
```

For academic citations:

```
Author(s). (2026). "Making Due Regard Visible: A Constraint Mapping Framework
for Lunar Governance." 25th Australian Space Research Conference, Adelaide.
```

---

## Acknowledgments

- IAU for maintaining the Gazetteer of Planetary Nomenclature
- NASA / LRO / LOLA / GRAIL teams for providing open lunar data
- CNSA, ISRO, JAXA, ESA, Roscosmos, KARI for mission transparency
- Australian Space Research Conference for the platform to present this work

---

## Disclaimer

Absence from this map does not mean an area is free of constraint. This map is a rendering of the current record, not a legal determination. It does not adjudicate, license, prohibit, or tell you where to land. It is a shared reference frame for coordination and transparency.

---

## Contact

- GitHub Issues: https://github.com/jeremyk322/LunarConstraintMap/issues

---

**Lunar Constraint Map — Making Due Regard Visible**
