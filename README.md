# Discover Kazakhstan

Discover Kazakhstan is a full-stack tourism web application for exploring destinations, hotels, and events in Kazakhstan. Users can view tourism information, use an interactive map, register/login, create bookings, and leave hotel reviews.

---

## Problem Definition

Tourism information in Kazakhstan is often spread across different websites and platforms. Users may struggle to find reliable information about destinations, hotels, events, and booking options in one place.

Discover Kazakhstan solves this problem by providing a centralized tourism platform with structured data and a simple user interface.

---

## Project Objective

The main objective of this project is to create a tourism platform where users can:

- explore destinations in Kazakhstan;
- view hotels and hotel details;
- check events on an interactive map;
- register and log in;
- create and manage bookings;
- write hotel reviews.

---

## Technology Stack

### Frontend

- React
- TypeScript
- Vite
- TailwindCSS
- React Router
- Axios
- Leaflet / React Leaflet
- OpenStreetMap

### Backend

- Python
- Django 5.2.8
- Django REST Framework
- Simple JWT
- SQLite
- Django CORS Headers

---

## Main Features

- Destination listing and details
- Hotel listing and details
- Event map with Leaflet and OpenStreetMap
- User registration and login
- JWT authentication
- Hotel booking
- Booking cancellation
- Hotel reviews
- Django admin panel
- Seed data for demo content

---

## Project Structure

```text
discover-kazakhstan/
├── README.md
├── setup.py
├── discover-kaz-backend/
│   ├── manage.py
│   ├── requirements.txt
│   ├── discover_kaz_backend/
│   ├── users/
│   ├── hotels/
│   ├── destinations/
│   ├── events/
│   ├── bookings/
│   └── media/
└── discover-kaz-frontend/
    ├── package.json
    ├── vite.config.ts
    ├── index.html
    └── src/
        ├── components/
        ├── pages/
        ├── contexts/
        ├── utils/
        ├── App.tsx
        └── main.tsx
```

## Installation Requirements

Before running the project, install:

- Python 3.11 or 3.12 recommended
- Node.js 18+
- npm
- Git

Check versions:

```bash
python3 --version
node --version
npm --version
git --version
```
---

## Backend Setup

Open terminal in the project folder:

```bash
cd discover-kaz-backend
```
Create and activate virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```
Install dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```
Run migrations:

```bash
python manage.py migrate
```
Seed database:

```bash
python manage.py seed_data
```
Run backend server:

```bash
python manage.py runserver
```
Backend runs at:

http://localhost:8000

Django Admin:

http://localhost:8000/admin

API:

http://localhost:8000/api

## Frontend setup

Open a new terminal.

Go to the frontend folder:

```bash
cd discover-kaz-frontend
```

Install dependencies:

```bash
npm install --legacy-peer-deps
```

If React Leaflet dependency conflict appears, install compatible versions:

```bash
npm install react@18.2.0 react-dom@18.2.0 react-router-dom@6.30.1 react-leaflet@4.2.1 leaflet@1.9.4 lucide-react axios --legacy-peer-deps
npm install -D @types/react@18.2.66 @types/react-dom@18.2.22 @types/leaflet@1.9.12 --legacy-peer-deps
``` 

Clear Vite cache if needed:

```bash
rm -rf node_modules/.vite
```

Run frontend:

```bash
npm run dev
```

Frontend will run at:

http://localhost:5173

## Running the Project

To run the project correctly, use two terminals.

Terminal 1: Backend
```bash
cd discover-kaz-backend
source .venv/bin/activate
python manage.py runserver
```

Backend:

http://localhost:8000
Terminal 2: Frontend
```bash
cd discover-kaz-frontend
npm run dev
```

Frontend:

http://localhost:5173

Both servers must be running at the same time.

## Seed Database Manually

If pages show:

No destinations found
No hotels found
No events found

it means the database is empty.

Run this in the backend terminal:

```bash
cd discover-kaz-backend
source .venv/bin/activate
python manage.py migrate
python manage.py seed_data
python manage.py runserver
```

Then check API data in the browser:

http://localhost:8000/api/destinations/
http://localhost:8000/api/hotels/
http://localhost:8000/api/events/

After that, open the frontend again:

http://localhost:5173

## Database Content

After running seed_data, the database contains sample tourism data.

Tourist Destinations
* Charyn Canyon
* Big Almaty Lake
* Medeu Ice Skating Rink
* Altyn-Emel National Park
* Kolsai Lakes
* Hotels
* The Ritz-Carlton, Almaty
* InterContinental Almaty
* Rixos Almaty Hotel
* Hotel Dostyk
* Hotel Kazakhstan
* Shymbulak Mountain Resort
* Events
* Almaty Marathon 2025
* Spirit of Tengri
* Apple Fest

The project also includes image files in the backend media folder.

## API Endpoints
Authentication
| Method | Endpoint              | Description                      |
| ------ | --------------------- | -------------------------------- |
| POST   | `/api/auth/register/` | Register new user                |
| POST   | `/api/auth/login/`    | Login user and receive JWT token |
| POST   | `/api/auth/logout/`   | Logout user                      |
| GET    | `/api/auth/user/`     | Get current authenticated user   |
