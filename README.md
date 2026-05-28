# 👗 FitVision AI — Virtual Try-On Studio

> *Because nobody wants to be the person staring sadly at an online purchase that looked way better on the model.*

FitVision AI fixes online shopping. It's an AI-powered virtual try-on web app that lets you build a personalized, true-to-scale body avatar, overlay real garments with physics-aware draping, and see exactly how clothes look on **your** actual body type before spending a single dollar.

This repository contains the **complete, production-ready frontend** built with React, TypeScript, and Tailwind CSS v4—fully optimized and architected to plug directly into a Node.js/Express and Python AI backend.

---

## ‍♀️ Why This Exists (The Problem)

Online shopping is broken, and the numbers prove it: e-commerce fashion suffers from a massive **40% return rate**, mostly due to sizing and fit issues. We buy clothes based on professional models who look nothing like us, decipher chaotic size charts, and cross our fingers.

FitVision AI flips the script:

* **Real-Scale Avatars:** Input your build parameters once to generate a proportional model that genuinely reflects your shape.
* **Physics-Aware Layering:** Drag, drop, and view realistic garment interactions on your custom avatar in real time.
* **No-Nonsense AI Insights:** Get honest feedback like *"Slightly tight across the shoulders—we suggest sizing up for a relaxed fit."*
* **Social Validation:** Save, organize, and share your curated looks with friends to vote before checking out.

---

## ✨ Feature Breakdown

### 🧍 Interactive Avatar Builder (4-Step Wizard)

An intuitive, animated onboarding flow designed to prevent user drop-off while capturing crucial body metrics:

* **Step 1: Identity & Basics:** Quick onboarding setup.
* **Step 2: Proportional Measurements:** Sliders and inputs for height, weight, chest, waist, and hips that dynamically scale the avatar.
* **Step 3: Visual Accuracy:** Choose from 6 realistic skin tones and 5 distinct structural body types.
* **Step 4: Style Alignment:** Toggle 6 aesthetic vibes to seed the personalized recommendation engine.

### 👗 Core Try-On Studio

A professional, 3-panel workspace engineered for high usability:

* **Left Panel (Garment Inventory):** Filterable catalog (Tops, Bottoms, Dresses, Jackets, Shoes, Accessories) with an integrated drag-and-drop file uploader for custom clothes.
* **Center Canvas (The Viewer):** Real-time avatar rendering with 360° rotation (Front, Side, Back, and animated spin), a 4-mode lighting simulator (Daylight, Evening, Studio, Golden Hour), and an AR camera fallback hook.
* **Right Panel (Cart & Action Matrix):** Instant outfit itemization, running price calculators, and quick-action triggers (*Save to Wardrobe*, *Add to Cart*, *Plan Outfits*).

### 🧠 Deep AI Fit Analysis

Translates complex data into clear, natural-language feedback:

* Visual fit accuracy meters (0–100%).
* Targeted diagnostics across 5 micro-zones (Shoulders, Length, Ease, Arms, Color Harmony).
* Contextual sizing recommendations based on specific item dimensions.

### 🎨 Live Color-Swap Engine

Instantly alters garment color values client-side using customized SVG/canvas blending logic, eliminating the need to download heavy, redundant image assets for simple color variants.

### 📦 Virtual Wardrobe & Planner

* **Saved Looks:** A clean grid featuring occasion tags, favorites tracking, and metadata.
* **Outfit Calendar:** A functional 7-day layout where users can drag and drop saved outfits to plan their week.
* **Try-On History:** A chronological log of every garment tested, complete with user star ratings.

### 🧬 Style DNA Profile

An evolving analytics panel that computes user preferences over time:

* **Trait Matrix:** Real-time grading across 5 core aesthetics (Streetwear, Minimalist, Athletic, Casual, Formal).
* **Color Palettes:** Tracks and displays your top 5 most-interacted colors.
* **Predictive AI Recommendations:** Highly targeted product cards complete with matching logic explanations.

---

## 🛠️ Tech Stack

| Layer | Technology | Key Use Case |
| --- | --- | --- |
| **Framework** | React 19 + TypeScript | Component architecture & absolute type-safety |
| **Build Tool** | Vite 7 | Lightning-fast HMR and optimized asset bundling |
| **Styling** | Tailwind CSS v4 | Next-gen utility-first styling with native CSS variables |
| **Animations** | Framer Motion | Smooth state transitions and micro-interactions |
| **Icons** | Lucide React | Clean, consistent vector icon library |
| **State** | Custom Stores (`useAppStore`) | Centralized, reactive application state management |

---

## 🚀 Getting Started

### Prerequisites

* Node.js 18+
* npm, yarn, or pnpm

### Quick Start Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/fitvision-ai.git
cd fitvision-ai

# Install dependencies cleanly
npm install

# Fire up the local development server
npm run dev

```

The app will instantly launch on `http://localhost:5173`.

---

## 📁 Project Structure

```
fitvision-ai/
├── public/
│   └── images/            # Static assets, garment mockups, and fallback graphics
├── src/
│   ├── components/
│   │   ├── LandingPage.tsx     # High-conversion product entry page
│   │   ├── AvatarBuilder.tsx   # 4-step user setup wizard
│   │   ├── TryOnStudio.tsx      # Core 3-panel interaction workspace
│   │   ├── VirtualWardrobe.tsx  # Outfit calendar, history logs, and saved looks
│   │   ├── StyleDNA.tsx         # User metrics and analytics panel
│   │   ├── Navigation.tsx       # Smooth floating app navigation dock
│   │   └── Toast.tsx            # Global notification event broker
│   ├── store/
│   │   └── appStore.ts          # Centralized reactive state engine
│   ├── data/
│   │   └── garments.ts          # Strongly-typed seed dataset for testing
│   ├── types/
│   │   └── index.ts             # Global TypeScript interface manifest
│   ├── App.tsx                  # Base application wrapper & view router
│   └── index.css                # Global styles and Tailwind configuration
└── index.html

```

---

## 🌐 Hackathon Architecture: Production Blueprint

This frontend was built from the ground up to support clean decoupling. To scale this into a full-stack production platform, hook into the following endpoints:

### 1. Recommended Production Architecture

```
[ Client: React 19 / Vite ]
           │ (HTTPS / WebSockets)
           ▼
[ API Gateway: Node.js + Express ] ──► [ Database: PostgreSQL / Prisma ]
           │
           │ (Internal gRPC / HTTP Fetch)
           ▼
[ AI Inference Pipeline: Python FastAPI ]
           ├──► Rembg (Instant background isolation)
           └──► IDM-VTON / Stable Diffusion (Virtual Try-on Diffusion models)

```

### 2. Standard API Routing Contract

```
POST   /api/avatar           # Persists user-defined structural metrics
POST   /api/garments/upload  # Ingests user clothing images -> runs background removal
POST   /api/tryon            # Combines avatar matrix + garment matrices for image generation
GET    /api/fit-analysis     # Evaluates item geometry vs avatar measurements
POST   /api/color-swap       # Runs runtime hue-shifting on standard assets
GET    /api/style-dna        # Aggregates user telemetry into style vectors

```

### 3. Transitioning to Live Backend Data

Upgrading from mock data to live server infrastructure is as simple as updating `src/store/appStore.ts`.

```typescript
// Local Mock Mutation
const saveOutfit = (name: string, occasion: string) => {
  setSavedOutfits(prev => [...prev, { name, occasion, id: Date.now().toString() }]);
};

// Production Server Sync
const saveOutfit = async (name: string, occasion: string) => {
  const response = await fetch('/api/outfit/save', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name, occasion, items: selectedGarments })
  });
  const realNewOutfit = await response.json();
  setSavedOutfits(prev => [...prev, realNewOutfit]);
};

```

---

## 🎨 Design System & Core Principles

* **Immersive Premium Aesthetic:** Utilizing deep, clean dark-mode canvases with vibrant, high-end accents. Fashion is visual; the interface mimics a modern magazine rather than a generic database.
* **Intentional Motion:** Every animation is tied directly to user feedback—fit scores fill dynamically, cards move smoothly during layout transitions, and menus slide on demand.
* **Contextual Viewports:** Complex panels are progressively disclosed to avoid user fatigue, ensuring an approachable workflow.

---

## 🤝 Contributing

1. Fork the project
2. Create a feature branch (`git checkout -b feature/cool-new-upgrade`)
3. Commit your changes (`git commit -m 'feat: add awesome new feature'`)
4. Push to your branch (`git push origin feature/cool-new-upgrade`)
5. Open a formal Pull Request

---

## 📄 License

Distributed under the MIT License. Use it to learn, build a product, scale a project, or showcase your portfolio.

---
