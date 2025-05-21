# Humidifier Control App

## Overview

This is a web application for controlling ultrasonic humidifiers via Bluetooth. The app allows users to connect to their humidifier device, set operation duration, start/stop the device, and monitor its status in real-time. 

The application consists of a React frontend and an Express backend, using Drizzle ORM for database interactions. It features a clean, modern UI built with Radix UI components (via shadcn/ui).

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

The application follows a modern web architecture with the following key components:

1. **Frontend**: React application with TypeScript, built using Vite
   - Uses React context for state management
   - Implements React Query for data fetching
   - Employs shadcn/ui components for UI elements
   - Custom Bluetooth integration via Web Bluetooth API

2. **Backend**: Express.js server
   - REST API for basic health checks and device compatibility
   - Serves the frontend application in production
   - Includes storage layer for user management
   
3. **Database**: Uses Drizzle ORM
   - PostgreSQL compatible schema definition
   - Currently uses in-memory storage in development
   - Ready for PostgreSQL integration

4. **Build & Development**: 
   - Vite for frontend development and building
   - TypeScript for type safety across the application
   - ESBuild for server compilation

## Key Components

### Frontend Components

1. **HumidifierContext** (`client/src/context/HumidifierContext.tsx`)
   - Central state management for humidifier operations
   - Handles Bluetooth connection, device control, and error management
   - Provides context hooks for components to access shared state

2. **Bluetooth Service** (`client/src/lib/bluetoothService.ts`)
   - Handles Web Bluetooth API interactions
   - Manages device discovery, connection, and command sending

3. **UI Components**
   - Core operational components:
     - `BluetoothConnect`: Initiates device connection
     - `TimePicker`: UI for setting operation duration
     - `TimerDisplay`: Shows remaining time with circular progress
     - `ConnectionStatus`: Visual indicator of connection state
   - UI library: Comprehensive set of shadcn/ui components 

### Backend Components

1. **Express Server** (`server/index.ts`)
   - Main application server with middleware setup
   - Request logging and error handling

2. **API Routes** (`server/routes.ts`)
   - Health check endpoint
   - Bluetooth compatibility information

3. **Storage** (`server/storage.ts`)
   - User management interface
   - In-memory implementation for development

4. **Database Schema** (`shared/schema.ts`)
   - User table definition using Drizzle ORM
   - Validation schemas using Zod

## Data Flow

1. **Device Connection**:
   - User initiates connection through the UI
   - Frontend uses Web Bluetooth API to discover and connect to the humidifier
   - Connection status is stored in the HumidifierContext and displayed to the user

2. **Device Control**:
   - User sets desired operation time using the TimePicker
   - Start/Stop commands are sent directly to the device over Bluetooth
   - Operation status and remaining time are tracked in the frontend context

3. **User Management** (prepared but not fully implemented):
   - User data would be stored in the PostgreSQL database
   - Authentication and session management are set up but not completely implemented

## External Dependencies

### Frontend
- React and React DOM for UI rendering
- React Query for data fetching
- shadcn/ui (based on Radix UI) for UI components
- Web Bluetooth API (browser native) for device communication

### Backend
- Express.js for the server framework
- Drizzle ORM for database operations
- Zod for schema validation

## Deployment Strategy

The application is configured for deployment on Replit with:

1. **Development Mode**:
   - `npm run dev` starts both frontend and backend in development mode
   - Vite handles hot module replacement for the frontend
   - Backend auto-reloads on changes

2. **Production Build**:
   - `npm run build` compiles both frontend and backend:
     - Frontend: Vite builds optimized assets
     - Backend: ESBuild bundles the server code
   - `npm run start` runs the production build

3. **Database**:
   - The application is ready to use PostgreSQL but currently uses in-memory storage
   - Drizzle ORM is configured for database migrations and schema management

## Getting Started

To run the application:

1. Ensure PostgreSQL is set up and DATABASE_URL is set in the environment
2. Run `npm run dev` to start the development server
3. For production deployment, run `npm run build` followed by `npm run start`

Note that Web Bluetooth API has limited browser support:
- Works on Chrome (Desktop & Android), Edge (Chromium-based), Opera, and Samsung Internet
- Does not work on Safari or Firefox by default