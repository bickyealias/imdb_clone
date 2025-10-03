# IMDB Clone - Full Stack Learning Project

A full-stack IMDB clone built with TypeScript, Next.js, and PostgreSQL to learn modern web development best practices.

## 🎯 Project Goals

- Learn full-stack development with TypeScript
- Implement modern web application architecture
- Practice database design and optimization
- Build a production-ready application with testing and CI/CD

## 🏗️ System Architecture

```mermaid
flowchart TB
    subgraph Client["Client Layer"]
        A[Web Browser]
    end

    subgraph FrontendApp["React SPA"]
        B[React Application]
        C[React Router]
        D[React Query Cache]
        E[Auth Context]
    end

    subgraph BackendAPI["Backend API - Node.js + Express"]
        F[Express Server]
        G[API Routes]
        H[Auth Middleware]
        I[Prisma ORM]
    end

    subgraph External["External Services"]
        J[TMDB API]
    end

    subgraph Data["Data Layer"]
        K[("PostgreSQL")]
    end

    subgraph Deploy["Deployment"]
        L[Netlify/Vercel Frontend]
        M[Railway/Render Backend]
        N[CDN Images/Assets]
    end

    A -->|HTTPS| L
    L -->|Serve SPA| B
    B -->|Navigate| C
    B -->|API Calls| F
    B -->|Auth State| E
    B -->|State Management| D
    F -->|Handle Requests| G
    G -->|Authenticate| H
    G -->|Query| I
    I -->|SQL| K
    G -->|Fetch Movie Data| J
    B -->|Static Assets| N

    style A fill:#e1f5ff,stroke:#333,stroke-width:2px
    style B fill:#ffe1f5,stroke:#333,stroke-width:2px
    style F fill:#fffacd,stroke:#333,stroke-width:2px
    style K fill:#e1ffe1,stroke:#333,stroke-width:2px
    style J fill:#fff5e1,stroke:#333,stroke-width:2px
```

## 📊 Detailed Architecture Diagram

```mermaid
flowchart LR
    subgraph Frontend["Frontend Components"]
        A1[HomePage]
        A2[MovieDetail]
        A3[SearchPage]
        A4[ProfilePage]
    end

    subgraph API["API Layer"]
        B1["GET /api/movies"]
        B2["GET /api/search"]
        B3["POST /api/reviews"]
        B4["POST /api/auth"]
    end

    subgraph Services["Services"]
        C1[TMDB Service]
        C2[Auth Service]
        C3[Movie Service]
        C4[Review Service]
    end

    subgraph Database["Database Models"]
        D1[("Movies")]
        D2[("Users")]
        D3[("Reviews")]
        D4[("Genres")]
    end

    A1 --> B1
    A2 --> B1
    A2 --> B3
    A3 --> B2
    A4 --> B4

    B1 --> C3
    B2 --> C3
    B3 --> C4
    B4 --> C2

    C1 --> TMDB[TMDB API]
    C3 --> D1
    C3 --> D4
    C4 --> D3
    C2 --> D2

    D1 -.->|relates to| D4
    D3 -.->|belongs to| D1
    D3 -.->|belongs to| D2

    style Frontend fill:#f9f9f9,stroke:#333,stroke-width:2px
    style API fill:#e8f4f8,stroke:#333,stroke-width:2px
    style Services fill:#fff4e8,stroke:#333,stroke-width:2px
    style Database fill:#e8f8e8,stroke:#333,stroke-width:2px
```

## 📋 User Requirements

### MVP Features (Phase 1)

#### Core Viewing Experience
- ✅ Browse movies/TV shows with pagination
- ✅ Search functionality (title-based)
- ✅ View detailed movie/show information (cast, crew, ratings, synopsis)
- ✅ Display basic user ratings and reviews

#### User Management
- ✅ User registration/login (email/password)
- ✅ Basic profile management

#### Content Discovery
- ✅ Homepage with trending/popular content
- ✅ Basic filtering (genre, year)
- ✅ Simple sort options (rating, release date)

### Later Phases

- ⏳ Advanced search (actors, directors, keywords- search based on few strings eg "Protagonists getting stuck on island post a shipwreck"
## 🛠️ Tech Stack

### Frontend
- **React 18+** - Component reusability, large ecosystem, hooks
- **Vite** - Fast build tool, HMR, optimized bundling
- **React Router v6** - Client-side routing, nested routes
- **TailwindCSS** - Rapid UI development, maintainable styling
- **Shadcn/ui or Material-UI** - Professional components, accessibility
- **React Query (TanStack Query)** - Server state management, caching
- **Axios** - HTTP client for API calls
- **TypeScript** - Type safety, better DX, catches errors early

### Backend
- **Node.js + Express** - Fast, unopinionated web framework
- **TypeScript** - Type safety across the stack
- **Prisma ORM** - Type-safe queries, migrations, excellent TypeScript integration
- **Express Validator** - Request validation middleware
- **Morgan** - HTTP request logger

### Database
- **PostgreSQL** - Relational data, ACID compliance, full-text search

### Authentication
- **Passport.js** - Flexible authentication middleware
- **JWT (jsonwebtoken)** - Stateless authentication tokens
- **bcrypt** - Password hashing
- **express-session** - Session management

### External APIs
- **TMDB API** - Free movie/TV data, images, metadata

### Caching/Performance
- **Redis** (Later phase) - Session storage, API response caching
- **Node-cache** (MVP) - In-memory caching

### Deployment
- **Frontend:** Netlify or Vercel - Static hosting, CDN, CI/CD
- **Backend:** Railway, Render, or Heroku - Node.js hosting with auto-deploy
- **Database:** Supabase, Railway, or Neon - PostgreSQL hosting

### Testing
- **Frontend:** Vitest + React Testing Library - Component testing
- **Backend:** Jest + Supertest - API endpoint testing
- **E2E:** Playwright - End-to-end testing

## 🚀 Execution Plan

### Phase 1: Project Setup & Infrastructure

**Initialize Backend Project**
- Create Express project with TypeScript
- Set up project structure (controllers, routes, middleware, services)
- Configure ESLint, Prettier, Husky (pre-commit hooks)
- Set up nodemon for development
- Configure CORS for frontend access

**Initialize Frontend Project**
- Create React project with Vite and TypeScript
- Set up React Router for routing
- Configure TailwindCSS
- Set up ESLint, Prettier
- Configure proxy for API calls

**Database Setup**
- Design database schema (Movies, Actors, Genres, Users, Reviews)
- Set up Prisma with PostgreSQL
- Create initial migrations
- Seed script for TMDB data

**Environment & Deployment**
- Set up environment variables for both frontend and backend
- Configure GitHub repository (monorepo or separate repos)
- Set up CI/CD pipelines

### Phase 2: Core Backend Development

**Data Layer**
- TMDB API integration service
- Database seeding scripts (popular movies/shows)
- Prisma queries for movies, search, filters

**API Routes**
- `GET /api/movies` (list with pagination)
- `GET /api/movies/:id` (movie details)
- `GET /api/search` (search functionality)
- `GET /api/genres`
- `POST /api/movies/:id/reviews` (authenticated)
- Error handling middleware
- Input validation with express-validator

**Authentication**
- Passport.js setup with Local Strategy
- JWT token generation and verification
- bcrypt password hashing
- Auth middleware for protected routes
- User registration and login endpoints

### Phase 3: Frontend Development

**Routing Setup**
- Configure React Router with nested routes
- Protected routes for authenticated users
- 404 page
- Route-based code splitting

**Layout & Navigation**
- Responsive header with search bar
- Footer
- Loading states and error boundaries
- Toast notifications setup

**Core Pages**
- Homepage (featured/trending movies)
- Movie listing page with filters
- Movie detail page (cast, crew, reviews)
- Search results page
- Login/Register pages
- User profile page

**Components**
- MovieCard component
- SearchBar with debouncing
- FilterPanel (genre, year, rating)
- ReviewList and ReviewForm
- Pagination component
- PrivateRoute wrapper component

**State Management**
- React Query/TanStack Query for server state
- Auth Context for user authentication state
- Context API for global UI state (theme, modals)

**API Integration**
- Axios instance with interceptors
- API service layer for all endpoints
- Token management and refresh logic
- Error handling and retry logic

### Phase 4: Polish & Testing

**Testing**
- Unit tests for utilities and hooks
- Component tests for key UI elements
- E2E tests for critical flows (search, view movie)

**Performance**
- Image optimization (lazy loading, WebP format)
- Code splitting and lazy loading with React.lazy
- React Query caching optimization
- Memoization with useMemo and useCallback
- Bundle size analysis and optimization

**UX Enhancements**
- Loading skeletons
- Error states with retry options
- Toast notifications
- Responsive design refinement
- Accessibility improvements (keyboard navigation, ARIA labels)

### Phase 5: Deployment & Monitoring

**Backend Deployment**
- Deploy Express API to Railway/Render
- Set up PostgreSQL database on hosting platform
- Configure environment variables
- Set up health check endpoints

**Frontend Deployment**
- Build optimized production bundle
- Deploy to Netlify or Vercel
- Configure environment variables
- Set up redirects for SPA routing

**Monitoring & Analytics**
- Set up error tracking (Sentry for both frontend and backend)
- Analytics (Google Analytics or Plausible)
- Performance monitoring (Web Vitals)
- API monitoring and logging

## 📁 Project Structure

### Option 1: Monorepo Structure
```
imdb-clone/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── ui/              # Reusable UI components
│   │   │   │   ├── Button.tsx
│   │   │   │   ├── Card.tsx
│   │   │   │   └── Input.tsx
│   │   │   ├── movies/          # Domain-specific components
│   │   │   │   ├── MovieCard.tsx
│   │   │   │   ├── MovieGrid.tsx
│   │   │   │   └── MovieDetail.tsx
│   │   │   └── layout/
│   │   │       ├── Header.tsx
│   │   │       ├── Footer.tsx
│   │   │       └── Navbar.tsx
│   │   ├── pages/               # Route components
│   │   │   ├── HomePage.tsx
│   │   │   ├── MovieDetailPage.tsx
│   │   │   ├── SearchPage.tsx
│   │   │   ├── LoginPage.tsx
│   │   │   ├── RegisterPage.tsx
│   │   │   └── ProfilePage.tsx
│   │   ├── hooks/
│   │   │   ├── useAuth.ts
│   │   │   ├── useMovies.ts
│   │   │   └── useSearch.ts
│   │   ├── services/
│   │   │   ├── api.ts           # Axios instance
│   │   │   ├── movieService.ts
│   │   │   ├── authService.ts
│   │   │   └── reviewService.ts
│   │   ├── context/
│   │   │   ├── AuthContext.tsx
│   │   │   └── ThemeContext.tsx
│   │   ├── types/
│   │   │   ├── movie.ts
│   │   │   └── user.ts
│   │   ├── utils/
│   │   │   ├── constants.ts
│   │   │   └── helpers.ts
│   │   ├── routes/
│   │   │   ├── AppRoutes.tsx
│   │   │   └── PrivateRoute.tsx
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   └── index.css
│   ├── public/
│   ├── .env.example
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   ├── tsconfig.json
│   └── package.json
│
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   │   ├── movieController.ts
│   │   │   ├── authController.ts
│   │   │   ├── reviewController.ts
│   │   │   └── userController.ts
│   │   ├── routes/
│   │   │   ├── movieRoutes.ts
│   │   │   ├── authRoutes.ts
│   │   │   ├── reviewRoutes.ts
│   │   │   └── userRoutes.ts
│   │   ├── middleware/
│   │   │   ├── auth.ts
│   │   │   ├── errorHandler.ts
│   │   │   └── validator.ts
│   │   ├── services/
│   │   │   ├── tmdbService.ts
│   │   │   ├── movieService.ts
│   │   │   └── authService.ts
│   │   ├── config/
│   │   │   ├── database.ts
│   │   │   ├── passport.ts
│   │   │   └── env.ts
│   │   ├── types/
│   │   │   └── express.d.ts
│   │   ├── utils/
│   │   │   ├── logger.ts
│   │   │   └── helpers.ts
│   │   ├── app.ts
│   │   └── server.ts
│   ├── prisma/
│   │   ├── schema.prisma
│   │   ├── migrations/
│   │   └── seed.ts
│   ├── tests/
│   │   ├── unit/
│   │   └── integration/
│   ├── .env.example
│   ├── tsconfig.json
│   └── package.json
│
├── .gitignore
└── README.md
```

### Option 2: Separate Repositories
- `imdb-clone-frontend/` - React + Vite application
- `imdb-clone-backend/` - Express API server

## 🗄️ Database Schema (Simplified MVP)

### Entity Relationship Diagram

```mermaid
erDiagram
    Movie ||--o{ Review : "has many"
    Movie ||--o{ CastMember : "has many"
    Movie }o--o{ Genre : "belongs to many"
    User ||--o{ Review : "writes many"
    Person ||--o{ CastMember : "has many"

    Movie {
        string id PK
        int tmdbId UK
        string title
        text overview
        datetime releaseDate
        string posterPath
        string backdropPath
        float rating
        int voteCount
        int runtime
        datetime createdAt
        datetime updatedAt
    }

    Genre {
        string id PK
        int tmdbId UK
        string name UK
    }

    Person {
        string id PK
        int tmdbId UK
        string name
        string profilePath
    }

    CastMember {
        string id PK
        string character
        int order
        string movieId FK
        string personId FK
    }

    User {
        string id PK
        string email UK
        string name
        string password
        string image
        datetime emailVerified
        datetime createdAt
        datetime updatedAt
    }

    Review {
        string id PK
        text content
        int rating
        string movieId FK
        string userId FK
        datetime createdAt
        datetime updatedAt
    }
```

### Prisma Schema

```prisma
model Movie {
  id          String       @id @default(cuid())
  tmdbId      Int          @unique
  title       String
  overview    String       @db.Text
  releaseDate DateTime
  posterPath  String?
  backdropPath String?
  rating      Float?
  voteCount   Int?
  runtime     Int?
  genres      Genre[]
  cast        CastMember[]
  reviews     Review[]
  createdAt   DateTime     @default(now())
  updatedAt   DateTime     @updatedAt
}

model Genre {
  id     String  @id @default(cuid())
  tmdbId Int     @unique
  name   String  @unique
  movies Movie[]
}

model Person {
  id         String       @id @default(cuid())
  tmdbId     Int          @unique
  name       String
  profilePath String?
  castRoles  CastMember[]
}

model CastMember {
  id        String @id @default(cuid())
  character String
  order     Int
  movieId   String
  personId  String
  movie     Movie  @relation(fields: [movieId], references: [id])
  person    Person @relation(fields: [personId], references: [id])

  @@unique([movieId, personId, character])
}

model User {
  id            String    @id @default(cuid())
  email         String    @unique
  name          String?
  password      String
  image         String?
  emailVerified DateTime?
  reviews       Review[]
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
}

model Review {
  id        String   @id @default(cuid())
  content   String   @db.Text
  rating    Int      @db.SmallInt // 1-10
  movieId   String
  userId    String
  movie     Movie    @relation(fields: [movieId], references: [id], onDelete: Cascade)
  user      User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  @@unique([movieId, userId])
}
```

## 🎯 Success Metrics for MVP

1. **Performance:**
   - Page load < 2s
   - Search results < 500ms
   - Lighthouse score > 90

2. **Functionality:**
   - All core features working end-to-end
   - Zero critical bugs

3. **Code Quality:**
   - 70%+ test coverage
   - No ESLint errors
   - Type-safe throughout

4. **UX:**
   - Mobile-responsive (320px - 4K)
   - Accessible (WCAG AA)
   - Intuitive navigation

## 🚦 Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL 14+
- TMDB API Key (free at https://www.themoviedb.org/settings/api)

### Installation

#### Backend Setup
```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your database and API credentials

# Run database migrations
npx prisma migrate dev

# Seed the database with sample data
npx prisma db seed

# Start the development server
npm run dev
```

Backend will run on `http://localhost:5000` (or your configured port)

#### Frontend Setup
```bash
# Navigate to frontend directory (in a new terminal)
cd frontend

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your backend API URL

# Start the development server
npm run dev
```

Frontend will run on `http://localhost:5173` (Vite default)

### Environment Variables

#### Backend (.env)
```env
# Server
PORT=5000
NODE_ENV=development

# Database
DATABASE_URL="postgresql://user:password@localhost:5432/imdb_clone"

# JWT
JWT_SECRET="your-jwt-secret-key"
JWT_EXPIRES_IN="7d"

# TMDB API
TMDB_API_KEY="your-tmdb-api-key"
TMDB_API_BASE_URL="https://api.themoviedb.org/3"

# CORS
CORS_ORIGIN="http://localhost:5173"
```

#### Frontend (.env)
```env
# API
VITE_API_BASE_URL="http://localhost:5000/api"

# Optional: TMDB for direct image URLs
VITE_TMDB_IMAGE_BASE_URL="https://image.tmdb.org/t/p"
```

## 📝 Available Scripts

### Backend
```bash
npm run dev          # Start development server with nodemon
npm run build        # Compile TypeScript to JavaScript
npm run start        # Start production server
npm run lint         # Run ESLint
npm run test         # Run tests
npm run prisma:studio # Open Prisma Studio
npm run prisma:generate # Generate Prisma Client
```

### Frontend
```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
npm run lint         # Run ESLint
npm run test         # Run tests
```

## 🧪 Testing Strategy

### Frontend Tests
- **Unit Tests:** Test utilities, hooks, and pure functions with Vitest
- **Component Tests:** Test React components in isolation with React Testing Library
- **E2E Tests:** Test critical user flows (search, view movie, create review) with Playwright

### Backend Tests
- **Unit Tests:** Test utilities and services with Jest
- **Integration Tests:** Test API routes and database operations with Supertest
- **API Tests:** Test authentication flows and protected endpoints

## 📚 Learning Resources

### Frontend
- [React Documentation](https://react.dev/)
- [Vite Documentation](https://vitejs.dev/)
- [React Router Documentation](https://reactrouter.com/)
- [TanStack Query Documentation](https://tanstack.com/query/latest)
- [TailwindCSS Documentation](https://tailwindcss.com/docs)

### Backend
- [Express.js Documentation](https://expressjs.com/)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Passport.js Documentation](http://www.passportjs.org/docs/)
- [JWT Documentation](https://jwt.io/introduction)

### General
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TMDB API Documentation](https://developer.themoviedb.org/docs)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

