# VR Gym Experience

## Overview

This is a VR fitness application that provides an immersive virtual gym environment where users can perform workout exercises. Built with React, Three.js, and WebXR technologies, the application allows users to interact with workout equipment in both standard browser mode and VR headset mode. The system tracks workout metrics including reps, time, and calories burned while providing a visually engaging 3D gym environment.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Core Technologies**
- React 18 with TypeScript for UI components and type safety
- Vite as the build tool and development server with custom configuration for 3D assets
- Three.js via `@react-three/fiber` for 3D rendering and scene management
- `@react-three/drei` for common 3D helpers and utilities
- `@react-three/xr` for WebXR integration enabling VR headset support
- `@react-three/postprocessing` for visual effects and rendering enhancements

**State Management**
- Zustand for application state with multiple specialized stores:
  - `useWorkoutStore`: Manages exercise tracking (current exercise, reps, calories, timing)
  - `useGame`: Controls game phases (ready, playing, ended) with subscribeWithSelector middleware
  - `useAudio`: Handles audio playback and mute state for background music and sound effects
- State stores follow a functional, immutable update pattern with clear action methods

**UI Component System**
- Radix UI primitives for accessible, unstyled component foundations
- shadcn/ui design system for pre-built styled components
- Tailwind CSS for utility-first styling with custom theme configuration
- CSS variables for dynamic theming (colors, spacing, border radius)
- Component library includes: dialogs, buttons, cards, forms, navigation, and more

**3D Scene Architecture**
- Modular component structure for 3D elements:
  - `GymEnvironment`: Renders gym floor, walls, ceiling, and workout areas
  - `WorkoutEquipment`: Interactive 3D equipment (dumbbells) with hover states
  - `VRCamera`: Handles camera controls and WASD keyboard movement
  - `WorkoutUI`: Overlay UI displaying exercise metrics
- Texture loading for realistic materials (wood flooring, asphalt workout areas)
- Interactive 3D objects with click/hover event handlers
- OrbitControls for desktop camera navigation

**VR/XR Implementation**
- XR store managing VR session state
- "Enter VR" button for headset mode activation
- Dual rendering mode supporting both browser and VR display
- Touch-action controls for mobile/VR input handling

### Backend Architecture

**Server Framework**
- Express.js with TypeScript for HTTP server
- Custom middleware for request/response logging with timing information
- Development mode with Vite middleware integration for HMR
- Production mode serving static built assets

**Storage Layer**
- In-memory storage implementation (`MemStorage`) for development
- Interface-based design (`IStorage`) allowing easy swap to database
- User management with CRUD operations (get, create, find by username)
- Auto-incrementing ID generation for in-memory records

**Database Schema**
- Drizzle ORM for type-safe database operations
- PostgreSQL dialect configuration
- User table schema with username/password fields
- Zod integration for runtime validation of insert operations
- Migration support with `drizzle-kit` for schema changes

**Build & Deployment**
- Separate build processes for client (Vite) and server (esbuild)
- ESM module format throughout the codebase
- TypeScript path aliases (`@/` for client, `@shared/` for shared code)
- Production server runs compiled JavaScript from dist directory

### External Dependencies

**Database**
- Neon Serverless Postgres (`@neondatabase/serverless`) for PostgreSQL database
- Drizzle ORM for database queries and migrations
- Connection via `DATABASE_URL` environment variable

**3D Graphics & VR**
- Three.js for WebGL rendering
- React Three Fiber for React integration with Three.js
- React Three Drei for Three.js helpers and utilities
- React Three XR for WebXR VR support
- GLSL shader support via `vite-plugin-glsl`

**UI Component Libraries**
- Radix UI component primitives (20+ component packages)
- Inter font family via `@fontsource/inter`
- Tailwind CSS for styling
- class-variance-authority and clsx for conditional styling
- cmdk for command menu components

**Developer Tools**
- TypeScript for static typing
- Vite runtime error modal plugin (`@replit/vite-plugin-runtime-error-modal`)
- PostCSS with Autoprefixer for CSS processing
- tsx for TypeScript execution in development

**Asset Management**
- Support for 3D model formats: `.gltf`, `.glb`
- Support for audio formats: `.mp3`, `.ogg`, `.wav`
- Texture image loading for materials
- Font file support (JSON format for Three.js)