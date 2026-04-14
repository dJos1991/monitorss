# MonitoRSS Codebase Overview

## Project Description
MonitoRSS (formerly Discord.RSS) is a comprehensive solution for delivering highly-customized news feeds (RSS, Atom, JSON) to Discord. It allows users to monitor various sources and format the delivery to Discord channels with extensive filtering and template options.

## Architecture
The project is structured as a **monorepo** of microservices, primarily using **TypeScript**.

### Core Services
- **`backend-api`**: The central API serving the control panel and managing core business logic. Built with **Fastify**.
- **`user-feeds`**: Service dedicated to handling user-specific feed logic, built with **NestJS**.
- **`user-feeds-next`**: Likely a newer iteration of the user-feeds service.
- **`feed-requests`**: Handles the fetching and processing of feed requests, built with **NestJS**.
- **`discord-rest-listener`**: Manages interactions with the Discord API.
- **`bot-presence`**: Manages the bot's status and presence on Discord.
- **`logger`**: A shared internal package for consistent logging across services.

## Tech Stack

### Languages
- **TypeScript** (Primary)
- **JavaScript**

### Backend
- **Runtime**: Node.js
- **Frameworks**: 
  - **Fastify** (Backend API)
  - **NestJS** (User Feeds, Feed Requests)
- **Databases**:
  - **MongoDB**: Primary database for the backend API (using Mongoose).
  - **PostgreSQL**: Used by microservices (using Mikro-ORM).
  - **Redis**: Caching layer for feed requests.
- **Message Broker**: **RabbitMQ** for inter-service communication.

### Frontend (Control Panel)
- **Framework**: **React**
- **Build Tool**: **Vite**
- **UI Library**: **Chakra UI**
- **State Management**: **TanStack Query** (React Query)
- **Form Management**: **React Hook Form** with **Yup** validation.
- **Routing**: **React Router**

### Build & Infrastructure
- **Orchestration**: **Docker Compose** is used to coordinate all services and databases.
- **Package Management**: npm (individual `package.json` in each service/package).

## Development & Build Commands
The project relies heavily on Docker for local development and production.

- **Start all services**: `docker compose up -d`
- **Build Services**: Individual services have a `npm run build` command which typically runs `tsc` (TypeScript compiler) or `nest build`.
- **Frontend Build**: `npm run build` within `services/backend-api/client` uses Vite.

## Testing
- **End-to-End**: **Playwright**
- **Frontend Units**: **Vitest**
- **Backend Units**: Node.js native test runner and NestJS testing utilities.
