# Rapid-Shield-NEXUS
Rapid Shield NEXUS is a AI integrated software that uses and mimics patterns, integrates real time data and location and tracks your 24/7 safety. It aims to provide rapid responses in terms of hospitality, security and social community. It uses CV, ML and statistical model and aims to provide aids under 3 min to save social and public order.
# RapidShield — Diamond Elite Hackathon Version

## Goal
Transform the existing single-file HTML prototype into a full-stack, hackathon-winning "Diamond Elite" platform with:
- **Google Maps** with live geolocation pins for staff/incidents
- **Real-time sensor data** simulation via WebSockets (Node.js backend)
- **CCTV panel** with live feed simulation (canvas-based video simulation + RTSP ready)
- **AI Triage** with streaming Gemini API calls (backend)
- **Elite glassmorphism UI** with 3D cards, animated gradients, particle effects
- **Full backend** — Node.js + Express + Socket.io for real-time data push

---

## Architecture Overview

```
Browser (Frontend)
  ├── index.html          ← Premium glassmorphism UI (single page)
  ├── style.css           ← Diamond elite design system
  ├── app.js              ← Frontend logic, Maps SDK, Socket.io client
  └── cctv.js             ← CCTV canvas simulation

Node.js Backend (server.js)
  ├── Express HTTP server
  ├── Socket.io server    ← Real-time push: sensor data, new incidents
  ├── /api/triage         ← Gemini AI triage endpoint
  ├── /api/incidents      ← REST CRUD for incidents
  └── /api/dispatch       ← Dispatch logic + response tracking

Google Services
  ├── Maps JavaScript API  ← Live property map with custom markers
  ├── Geolocation API      ← Browser native (staff GPS tracking)
  └── Gemini API           ← AI triage recommendations
```

---

## Proposed Changes

### Backend — NEW Files

#### [NEW] server.js
- Express HTTP server (port 3000)
- Socket.io real-time engine
- Simulated sensor data emitter every 2.5s (smoke, temp, CO2, motion)
- Simulated new incident generator (random every 30–90s)
- `/api/triage` — proxies to Gemini API with incident context
- `/api/incidents` — in-memory incident store (CRUD)
- `/api/dispatch` — marks dispatch, pushes to all connected clients
- Serves static frontend files

#### [NEW] package.json
- express, socket.io, node-fetch, cors, dotenv

#### [NEW] .env
- `GEMINI_API_KEY=your_key_here`
- `GOOGLE_MAPS_KEY=your_key_here`
- `PORT=3000`

---

### Frontend — REPLACE/NEW Files

#### [NEW] index.html
Complete rewrite with:
- **Particle.js background** on the nav header
- **Glassmorphism cards** with blur + gradient borders
- **5 screens**: Dashboard, Live Map, Guest SOS, AI Triage, Analytics
- Google Maps embed with custom styled map (dark theme)
- CCTV panel with canvas-based simulation of multiple feeds
- Animated incident cards with severity pulse rings
- Premium stat counters with number animation on load

#### [NEW] style.css
- Full design token system (CSS custom properties)
- Glassmorphism mixins
- 3D card hover transforms
- Animated gradient backgrounds
- Micro-animation library (fade-in, slide-up, pulse)
- Dark mode base with neon accent colors

#### [NEW] app.js
- Socket.io client connection to backend
- Google Maps initialization with custom dark theme + markers
- Real-time sensor chart updates (Chart.js)
- Geolocation tracking (navigator.geolocation.watchPosition)
- Incident feed management
- CCTV canvas simulation (multiple feeds, motion detection overlay)
- Gemini AI triage fetch calls

---

## Key "Wow" Features for Judges

| Feature | Implementation |
|---|---|
| Google Maps live | Maps JS API with custom dark tiles, animated incident rings |
| Staff geolocation | navigator.geolocation → socket → map pin updates |
| CCTV simulation | HTML5 Canvas with noise/grain + motion detection overlay |
| Real-time sensors | Socket.io push → live gauge/chart updates |
| Gemini AI Triage | Backend Gemini API call → streamed recommendation |
| SOS countdown | Animated countdown with geolocation capture |
| Predictive risk | Bar + gauge charts with animated fill on load |
| Audit log | Exportable table with CSV download |

---

## Open Questions

> [!IMPORTANT]
> Do you have a **Google Maps API key** and **Gemini API key** ready? If not, the Maps will use a free public tile fallback (OpenStreetMap via Leaflet.js) and Gemini will return simulated responses.

> [!IMPORTANT]
> Should this run on **localhost only** (hackathon demo) or do you need it deployed to a cloud URL (e.g., Google Cloud Run / Vercel)? I'll set it up for localhost with easy deploy instructions.

---

## Verification Plan

### Automated
- `npm install` → `node server.js` → confirm server starts on port 3000
- Browser open `http://localhost:3000` → all 5 screens render
- Socket.io connection confirmed in browser console

### Manual / Demo
- Live sensor gauges fluctuate every 2.5s automatically
- "Simulate New Alert" button triggers real-time cross-client push
- Google Maps shows animated incident pins
- CCTV canvas shows simulated feeds
- SOS button triggers countdown + backend socket broadcast
- AI Triage shows Gemini recommendation (or smart simulation fallback)
