# Discover Kazakhstan - Frontend

React + TypeScript + Vite is an application for the tourist website of Kazakhstan.

## Requirements

- Node.js (v18 or higher)
- npm or yarn

## Installation

1. Install the dependencies:
```bash
npm install
```

2. Create a `.env` file based on `.env.example`:
``bash
cp .env.example .env
```

3. Configure the environment variables in `.env`:
```
VITE_API_BASE_URL=http://localhost:8000/api
```

## Launch

To run in development mode:
```bash
npm run dev
```

To build the production version:
```bash
npm run build
```

To preview the production build:
```bash
npm run preview
```

## API Structure

The frontend expects the following endpoints from the Django backend:

### Authentication
- `POST /api/auth/register/` - User registration
- `POST /api/auth/login/` - User login (returns access and refresh tokens)
- `POST /api/auth/logout/` - User logout
- `GET /api/auth/user/` - Getting the current user (requires a token)

### Hotels
- `GET /api/hotels/` - List of all hotels
- `GET /api/hotels/:id/` - Hotel details
- `GET /api/hotels/:id/reviews/` - Hotel reviews

### Directions
- `GET /api/destinations/` - List of destinations
- `GET /api/destinations/:id/` - Details of the destination

### Reservations
- `GET /api/bookings/` - User's booking list (requires a token)
- `POST /api/bookings/` - Booking creation (requires a token)
- `PATCH /api/bookings/:id/` - Booking update (requires a token)
- `POST /api/bookings/:id/cancel/` - Cancellation of the reservation (requires a token)

### Reviews
- `POST /api/reviews/` - Creating a review (requires a token)

## Authentication

The application uses JWT tokens for authentication:
- The access token is saved in localStorage
- The token is sent in the header `Authorization: Bearer <token>`

## Technology

- React 19
- TypeScript
- Vite
- React Router v6
- Tailwind CSS
- Lucide Icons

## API Service

All the logic of working with the API is encapsulated in `/src/services/api.ts'. This service:
- Handles all HTTP requests to the backend
- Automatically adds an authentication token
- Handles errors

## Project structure

```
src/
├── components/       # Reusable components
├── contexts/        # React contexts (AuthContext)
├── pages/           # Application Pages
├── services/        # API services
├── types/           # TypeScript types
├── App.tsx # Main Component
└── main.tsx # Entry point
```



- All API requests go through the service in `src/services/api.ts`
- Authentication is managed via the 'AuthContext`
- To add new API endpoints, extend the 'ApiService` class
- The data types are located in `src/types/index.ts`