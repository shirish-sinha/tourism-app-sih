# Yātrā AI — Intelligent Tourist Companion
### Smart India Hackathon 2026 Edition

A production-grade, AI-powered intelligent tourist companion engineered for Indian & Karnataka cultural heritage exploration. Built with an offline-first architecture, local GPU LLM inference, grounded Retrieval-Augmented Generation (RAG), multimodal epigraphy analysis, and algorithmic spatial itinerary planning.

All historical assertions, dates, architectural analyses, and monument metadata are grounded in verified datasets from the **Archaeological Survey of India (ASI)**, **UNESCO World Heritage Centre**, and **Incredible India (Ministry of Tourism)**.

---

## 🏛️ System Architecture

```
[ Frontend: Expo / React Native Web ]
   │
   ├── 🏛️ Home Dashboard (`/`) — Curated sites, audio guide player, quick action hub
   ├── 🧭 Heritage Explorer (`/explore`) — Search, filters (UNESCO, Temples, Museums)
   ├── 🤖 AI Guide Chat (`/chat`) — Grounded conversation with source citations & TTS
   ├── 🗺️ Itinerary Planner (`/itinerary`) — Spatial clustering & time-slotted schedules
   └── 📷 Vision & Epigraphy (`/vision`) — Architectural style identification & translation
   │
   ▼ HTTP / JSON
[ Backend: Node.js + Express + TypeScript ] (`http://localhost:5000`)
   │
   ├── 📚 MongoDB Database (`mongodb://127.0.0.1:27017/tourism_companion`)
   │    ├── HeritageSites (Hampi, Pattadakal, Hoysala Temples, Taj Mahal)
   │    ├── Places / POIs (Vitthala Temple, Lotus Mahal, Elephant Stables)
   │    ├── Museums & Artifacts (Archaeological Museum Hampi, etc.)
   │    ├── KnowledgeChunks (Text search & grounded historical chunks)
   │    └── Sources (ASI, UNESCO, Incredible India verified links)
   │
   └── 🧠 RAG & LLM Engine
        ├── Local GPU LLM: LM Studio / llama-server (`http://127.0.0.1:11947/v1`)
        │    Running: Qwen3-8B-Q4_K_M on NVIDIA CUDA GPU
        ├── Grounded Prompt Synthesis with source citation tracking
        └── Graceful Mock Provider fallback for network/offline demos
```

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- **Node.js** v18+ and **npm**
- **MongoDB Community Edition** running locally on port `27017`
- *(Optional for real LLM inference)*: **LM Studio** running on `http://127.0.0.1:11947/v1` with a loaded model (e.g. Qwen3-8B).

### 2. Backend Setup
```bash
cd server

# Install dependencies
npm install

# Seed the database with verified Karnataka UNESCO & Heritage data
npm run seed

# Run development server (with hot reload)
npm run dev
```
*The server will start on `http://localhost:5000` and automatically connect to MongoDB and LM Studio.*

### 3. Frontend Setup
```bash
# In the root AI-tourist-companion directory
npm install

# Start the Expo application
npx expo start
# Or start directly in web browser
npx expo start --web
```

---

## 📡 Backend API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/health` | Service health status and environment |
| `GET` | `/api/heritage` | List all UNESCO World Heritage sites |
| `GET` | `/api/heritage/:slug` | Retrieve single heritage site with cited sources |
| `GET` | `/api/places` | List monuments & points of interest (supports `nearby=lng,lat`) |
| `GET` | `/api/museums` | List museums and collections |
| `GET` | `/api/artifacts` | List catalogued archaeological artifacts |
| `GET` | `/api/ai/status` | Current LLM provider status (LM Studio GPU / Mock) |
| `POST` | `/api/ai/chat` | Grounded RAG conversation with source citations |
| `POST` | `/api/ai/story` | Curated multi-minute site narrative for audio guides |
| `POST` | `/api/ai/vision` | Architectural identification & inscription translation |
| `POST` | `/api/rag/search` | Raw knowledge chunk retrieval & relevance scoring |
| `POST` | `/api/itinerary/generate` | Spatial clustering & time-scheduled day trip planner |

---

## 🛡️ Trust & Source Attribution
Unlike generic AI chatbots that hallucinate dates and dynasties, **Yātrā AI** enforces strict provenance:
- Every chat response and audio guide story extracts relevant `KnowledgeChunks` from verified ASI / UNESCO documentation.
- Source names, organizations, and official URLs are attached to every response with a calculated confidence rating.
- Inscriptions are verified against epigraphical archives (*Epigraphia Carnatica*).
