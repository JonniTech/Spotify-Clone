<div align="center">

<h1>TEVIFY</h1>

<img src="src/assets/Tevify-image.png" alt="Tevify — Music Streaming Application" width="100%" />

### A Modern Music Streaming Experience

[![React](https://img.shields.io/badge/React_19-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS_4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vite.dev)
[![Zustand](https://img.shields.io/badge/Zustand-433E38?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZD0iTTEyIDJDNi40OCAyIDIgNi40OCAyIDEyczQuNDggMTAgMTAgMTAgMTAtNC40OCAxMC0xMFMxNy41MiAyIDEyIDJ6IiBmaWxsPSJ3aGl0ZSIvPjwvc3ZnPg==&logoColor=white)](https://zustand-demo.pmnd.rs)

**Tevify** is a feature-rich, Spotify-inspired music streaming web application built with modern web technologies. It delivers a premium listening experience through the Jamendo Creative Commons music catalog, featuring real-time playback, library management, artist discovery, and a fully responsive mobile-first design.

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Table of Contents

- [Aim](#aim)
- [Problem Statement](#problem-statement)
- [Solution](#solution)
- [Features](#features)
- [Architecture](#architecture)
- [User Flow](#user-flow)
- [Data Flow](#data-flow)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [API Reference](#api-reference)
- [License](#license)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Aim

Tevify aims to deliver a **production-grade music streaming web application** that replicates the core user experience of Spotify while leveraging openly licensed music from Jamendo. The project serves as both a fully functional product and a technical reference for building complex, state-driven media applications with modern React patterns.

**Key Objectives:**
- Provide seamless music discovery, search, and playback across all devices
- Implement persistent user libraries with liked songs, saved albums, and followed artists
- Achieve visual and functional parity with industry-leading music streaming platforms
- Maintain a responsive, accessible, and performant user interface

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Problem Statement

The current landscape of music streaming presents several challenges for both users and developers:

| Problem | Impact |
|---------|--------|
| **Platform Lock-in** | Major streaming platforms require paid subscriptions and proprietary ecosystems |
| **Limited Open-Source Alternatives** | Few open-source music players offer a modern, Spotify-caliber user experience |
| **Creative Commons Discoverability** | Millions of freely licensed tracks on Jamendo lack an intuitive discovery interface |
| **Mobile-First Gap** | Many web-based music players are built desktop-first, leaving mobile users with degraded experiences |
| **State Complexity** | Managing global playback state, queues, and user libraries across a single-page application is architecturally challenging |

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Solution

Tevify addresses each of these challenges through a carefully architected application:

```
Problem                          Solution
-------------------------------  ----------------------------------------
Platform lock-in                 Free, open-source, no account required
Limited open-source players      Full-featured SPA with Spotify-level UX
CC music discoverability         Integrated Jamendo API with smart search
Mobile-first gap                 Responsive design with compact mini-player
State complexity                 Zustand stores with localStorage persistence
```

**Tevify bridges the gap** between professional streaming platforms and open-source music players by combining Creative Commons music with a premium, responsive interface.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Features

### Core Playback
- Global audio player with play, pause, skip, previous, shuffle, and repeat controls
- Real-time progress tracking with seekable progress bar
- Volume control with mute toggle
- Queue management with track ordering
- Compact mobile mini-player with progress line indicator

### Music Discovery
- Trending and popular tracks on the home feed
- Popular artists with circular card browsing
- Popular albums and new releases
- Genre-based exploration across 16 music categories
- Real-time debounced search with instant results

### Library Management
- Like/unlike songs with animated heart toggle (persisted to localStorage)
- Save/unsave albums to personal collection
- Follow/unfollow artists
- Dedicated "Liked Songs" playlist with purple gradient header
- Filter tabs (All, Playlists, Artists, Albums) in Your Library

### Pages
- **Home** -- Time-based greeting, trending tracks, popular artists, albums, genre sections
- **Search** -- Real-time search with 16 color-coded genre tiles
- **Artist** -- Artist profile, popular tracks (expandable), discography, follow button
- **Album** -- Album art, tracklist, save button, release info
- **Genre** -- Color-coded gradient header with filtered tracks
- **Playlist** -- Mosaic cover art, tracklist, playback controls
- **Library** -- Tabbed view of all saved content
- **Liked Songs** -- Dedicated playlist with Spotify-style purple gradient

### Design
- Figtree typography (closest match to Spotify's Circular Sp)
- Dark theme with Spotify-inspired green accent (`#1DB954`)
- Framer Motion animations throughout
- Glassmorphism and backdrop blur effects
- Skeleton loading states on all pages

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Architecture

### High-Level System Architecture

```mermaid
graph TB
    subgraph Client["Client Layer"]
        UI["React 19 UI"]
        Router["React Router v7"]
        Zustand["Zustand Stores"]
    end

    subgraph State["State Management"]
        PS["playerStore"]
        LS["libraryStore"]
        LC["localStorage"]
    end

    subgraph Services["Service Layer"]
        API["Jamendo API Service"]
    end

    subgraph External["External"]
        Jamendo["Jamendo API v3.0"]
        CDN["Jamendo CDN"]
    end

    UI --> Router
    UI --> Zustand
    Zustand --> PS
    Zustand --> LS
    LS --> LC
    UI --> API
    API --> Jamendo
    PS --> CDN
```

### Component Architecture

```mermaid
graph TD
    App["App.tsx"] --> AppLayout["AppLayout"]
    AppLayout --> Sidebar["Sidebar (Desktop)"]
    AppLayout --> TopBar["TopBar"]
    AppLayout --> Outlet["Router Outlet"]
    AppLayout --> Player["MusicPlayer"]
    AppLayout --> MobileNav["MobileNav (Mobile)"]

    Outlet --> Home["HomePage"]
    Outlet --> Search["SearchPage"]
    Outlet --> Artist["ArtistPage"]
    Outlet --> Album["AlbumPage"]
    Outlet --> Genre["GenrePage"]
    Outlet --> Playlist["PlaylistPage"]
    Outlet --> Library["LibraryPage"]
    Outlet --> Liked["LikedSongsPage"]

    Home --> TrackCard["TrackCard"]
    Home --> ArtistCard["ArtistCard"]
    Home --> AlbumCard["AlbumCard"]
    Artist --> TrackListItem["TrackListItem"]
    TrackListItem --> LikeButton["LikeButton"]
    Player --> LikeButton
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## User Flow

```mermaid
flowchart LR
    A["Open App"] --> B["Home Page"]
    B --> C{"User Action"}

    C --> D["Search Music"]
    C --> E["Browse Genre"]
    C --> F["View Library"]

    D --> G["View Results"]
    G --> H["Play Track"]
    G --> I["Visit Artist"]
    G --> J["Visit Album"]

    E --> K["Genre Page"]
    K --> H

    I --> L["Artist Page"]
    L --> H
    L --> M["Follow Artist"]
    L --> N["View Discography"]
    N --> J

    J --> O["Album Page"]
    O --> H
    O --> P["Save Album"]

    H --> Q["Like Song"]
    Q --> R["Liked Songs Page"]

    F --> R
    F --> S["Saved Albums"]
    F --> T["Followed Artists"]
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Data Flow

```mermaid
sequenceDiagram
    participant U as User
    participant C as Component
    participant S as Jamendo Service
    participant API as Jamendo API
    participant PS as playerStore
    participant LS as libraryStore
    participant LS2 as localStorage

    U->>C: Navigate to page
    C->>S: Fetch data (tracks/albums/artists)
    S->>API: GET /v3.0/tracks?client_id=...
    API-->>S: JSON response
    S-->>C: Parsed data
    C-->>U: Render content

    U->>C: Click play
    C->>PS: playTrackFromQueue(track, queue)
    PS-->>C: Update currentTrack, isPlaying
    C-->>U: Audio begins, UI updates

    U->>C: Click like
    C->>LS: toggleLike(track)
    LS->>LS2: Persist to localStorage
    LS-->>C: Update liked state
    C-->>U: Heart animation
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Tech Stack

<div align="center">

| Layer | Technology | Purpose |
|:------|:-----------|:--------|
| **Framework** | ![React](https://img.shields.io/badge/React_19-61DAFB?style=flat-square&logo=react&logoColor=black) | Component-based UI with hooks |
| **Language** | ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) | Type-safe development |
| **Build Tool** | ![Vite](https://img.shields.io/badge/Vite_6-646CFF?style=flat-square&logo=vite&logoColor=white) | Lightning-fast HMR and bundling |
| **Styling** | ![Tailwind](https://img.shields.io/badge/Tailwind_CSS_4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white) | Utility-first CSS framework |
| **UI Components** | ![shadcn/ui](https://img.shields.io/badge/shadcn/ui-000000?style=flat-square&logo=shadcnui&logoColor=white) | Accessible, composable primitives |
| **State** | ![Zustand](https://img.shields.io/badge/Zustand-433E38?style=flat-square) | Lightweight global state management |
| **Routing** | ![React Router](https://img.shields.io/badge/React_Router_7-CA4245?style=flat-square&logo=reactrouter&logoColor=white) | Client-side navigation |
| **Animation** | ![Framer Motion](https://img.shields.io/badge/Framer_Motion-0055FF?style=flat-square&logo=framer&logoColor=white) | Spring-based animations |
| **Icons** | ![React Icons](https://img.shields.io/badge/React_Icons-E91E63?style=flat-square&logo=react&logoColor=white) | Ionicons icon set |
| **Typography** | ![Google Fonts](https://img.shields.io/badge/Figtree-4285F4?style=flat-square&logo=googlefonts&logoColor=white) | Spotify Circular Sp alternative |
| **API** | ![Jamendo](https://img.shields.io/badge/Jamendo_API_v3-2ECC40?style=flat-square) | Creative Commons music catalog |
| **Persistence** | ![localStorage](https://img.shields.io/badge/localStorage-FF6F00?style=flat-square) | Client-side library persistence |

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Project Structure

```
tevify/
├── public/
├── src/
│   ├── assets/
│   │   └── Tevify-image.png         # App logo
│   ├── components/
│   │   ├── layout/
│   │   │   ├── AppLayout.tsx         # Root layout shell
│   │   │   ├── Sidebar.tsx           # Desktop navigation + library
│   │   │   ├── TopBar.tsx            # Header with mobile logo
│   │   │   └── MobileNav.tsx         # Bottom tab bar
│   │   ├── player/
│   │   │   └── MusicPlayer.tsx       # Dual desktop/mobile player
│   │   ├── ui/                       # shadcn/ui primitives
│   │   ├── AlbumCard.tsx             # Square album card
│   │   ├── ArtistCard.tsx            # Circular artist card
│   │   ├── LikeButton.tsx            # Animated heart toggle
│   │   ├── TrackCard.tsx             # Grid track card
│   │   └── TrackListItem.tsx         # Row track item with like
│   ├── pages/
│   │   ├── HomePage.tsx              # Landing with discovery sections
│   │   ├── SearchPage.tsx            # Search + genre browsing
│   │   ├── ArtistPage.tsx            # Artist detail + discography
│   │   ├── AlbumPage.tsx             # Album detail + tracklist
│   │   ├── GenrePage.tsx             # Genre category tracks
│   │   ├── PlaylistPage.tsx          # Playlist detail
│   │   ├── LibraryPage.tsx           # Your Library (tabbed)
│   │   └── LikedSongsPage.tsx        # Liked songs collection
│   ├── services/
│   │   └── jamendo.ts                # Jamendo API client (15 endpoints)
│   ├── stores/
│   │   ├── playerStore.ts            # Playback state (Zustand)
│   │   └── libraryStore.ts           # Library state (Zustand + persist)
│   ├── lib/
│   │   └── utils.ts                  # Utility functions
│   ├── App.tsx                       # Route definitions
│   ├── main.tsx                      # Entry point
│   └── index.css                     # Global styles + theme tokens
├── index.html                        # HTML template
├── vite.config.ts                    # Vite configuration
├── tailwind.config.ts                # Tailwind configuration
├── tsconfig.json                     # TypeScript configuration
├── package.json
├── GUIDE.md                          # Project requirements doc
└── .env                              # VITE_JAMENDO_CLIENT_ID
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Getting Started

### Prerequisites

- **Node.js** >= 18.0
- **npm** >= 9.0
- A free [Jamendo API](https://developer.jamendo.com/v3.0) client ID

### Installation

```bash
# Clone the repository
git clone https://github.com/JonniTech/Spotify-Clone.git
cd Spotify-Clone

# Install dependencies
npm install

# Configure environment variables
cp .env.example .env
```

Add your Jamendo API client ID to `.env`:

```env
VITE_JAMENDO_CLIENT_ID=your_client_id_here
```

### Development

```bash
# Start development server
npm run dev
```

The app will be available at `http://localhost:5174`

### Production Build

```bash
# Build for production
npm run build

# Preview production build
npm run preview
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## API Reference

Tevify interfaces with the **Jamendo API v3.0** through the following endpoints:

| Function | Endpoint | Description |
|----------|----------|-------------|
| `getPopularTracks` | `/tracks` | Fetch trending tracks by popularity |
| `getTracksByTag` | `/tracks` | Filter tracks by genre tag |
| `searchTracks` | `/tracks` | Full-text search across track catalog |
| `getArtist` | `/artists` | Fetch artist profile and metadata |
| `getArtistTracks` | `/artists/tracks` | Get all tracks by a specific artist |
| `getArtistAlbums` | `/artists/albums` | Get discography for an artist |
| `getPopularArtists` | `/artists` | Discover trending artists |
| `getAlbum` | `/albums` | Fetch album metadata |
| `getAlbumTracks` | `/albums/tracks` | Get tracklist for an album |
| `getPopularAlbums` | `/albums` | Fetch popular albums |
| `searchAlbums` | `/albums` | Search albums by name |
| `getPopularPlaylists` | `/playlists` | Discover curated playlists |
| `getPlaylistTracks` | `/playlists/tracks` | Get tracks in a playlist |
| `getNewReleases` | `/albums` | Fetch recently released albums |

All requests are authenticated via the `client_id` query parameter from the environment variable.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## Responsive Design

Tevify follows a mobile-first responsive strategy:

| Breakpoint | Layout |
|:-----------|:-------|
| `< 768px` (Mobile) | Bottom tab nav, compact mini-player, Tevify logo in header, 2-column grids |
| `>= 768px` (Desktop) | Left sidebar with library, full 3-column player, 5-column grids |

### Mobile Mini-Player
The mobile player displays as a compact bar above the bottom navigation, featuring:
- Track artwork and title
- Like button
- Play/pause toggle
- Thin green progress line at the top edge

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## License

This project is open source and available under the [MIT License](LICENSE).

Music content is provided by [Jamendo](https://www.jamendo.com) under Creative Commons licenses.

<div align="center">

---

**Built with precision by NYAGANYA**

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/JonniTech)

</div>
