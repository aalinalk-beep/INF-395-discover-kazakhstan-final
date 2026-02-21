---
# Discover Kazakhstan - Backend Documentation

## Table of contents
1. [Project Overview](#1-project overview)
2. [Technology Stack](#2-technology stack)
3. [Setting up the local environment](#3-setting up the local environment)
4. [Application Launch](#4-application launch)
5. [Project Structure] (#5-project structure)
6. [API Endpoint Documentation](#6-api endpoint documentation)
- [Authentication](#61-authentication)
- [Hotels and Reviews](#62-hotels and Reviews)
- [Destinations](#63-destinations)
- [Bookings](#64-Reservations)
7.  [Admin Panel](#7-Admin panel)

---

## 1. Project Overview

This is a backend service for the Discover Kazakhstan travel app. It provides a REST API for managing users, hotels, destinations, reviews, and bookings. The backend is built on Django and Django REST Framework and uses JWT for authentication.

## 2. Technology stack

- **Framework**: Django
- **API**: Django REST Framework
- **Authentication**: djangorestframework-simplejwt (JWT tokens)
- **CORS**: django-cors-headers
- **Database**: SQLite 
- **Language**: Python 3

## 3. Setting up the local environment

### Preliminary requirements
-   Python 3.8+
-   `pip` 
-   `virtualenv` 

### Installation Steps

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd discover-kaz-backend
    ```

2.  **Create and activate a virtual environment:**
    ```bash
    # Create .venv
    python -m venv .venv

    # Activation on macOS / Linux
    source .venv/bin/activate

    # Activation on Windows
    .\.venv\Scripts\activate
    ```

3. **Install the dependencies:**
``bash
pip install -r requirements.txt
``

4.  **Apply database migrations:**
    This command will create tables in the database based on Django models.
    ```bash
    python manage.py migrate
    ```

5. **Create a superuser:**
This is necessary to access the Django admin panel.
    ```bash
    python manage.py createsuperuser
    ```
    Follow the instructions in the terminal to create a user.

##4. Launching the app

To start the development server, run the command:
``bash
python manage.py runserver
``
The server will be available at `http://127.0.0.1:8000 /`.

## 5. Project Structure

```
discover-kaz-backend/
├── .venv/                  # Virtual environment
,── discover_kaz_backend/ # Main project configuration
│   ├── settings.py # Project Settings
,── urls.py # Root URL routing
├── users/                  # An application for users and authentication
├── hotels/                 # An app for hotels and reviews
├── destinations/           # Application for tourist destinations
├── bookings/               # Booking app
├── manage.py # Project Management Utility
,── requirements.txt # List of dependencies
```

## 6. API Endpoint Documentation

**Base URL:** `http://localhost:8000/api`

### 6.1. Authentication

Endpoints for managing users and sessions.

#### `POST /auth/register/`
Registration of a new user.
- **Authentication:** Not required.
-   **Request Body:**
    ```json
    {
      "email": "user@example.com",
      "password": "password123",
      "name": "John Doe"
    }
    ```
-   **Success Response (201 Created):**
    ```json
    {
      "message": "User created successfully"
    }
    ```

#### `POST /auth/login/`
User login and receipt of JWT tokens.
- **Authentication:** Not required.
-   **Request Body:**
    ```json
    {
      "email": "user@example.com",
      "password": "password123"
    }
    ```
-   **Success Response (200 OK):**
    ```json
    {
      "access": "eyJ0eXAiOiJKV1QiLCJhbGc...",
      "refresh": "eyJ0eXAiOiJKV1QiLCJhbGc...",
      "user": {
        "id": "uuid-string",
        "email": "user@example.com",
        "name": "John Doe"
      }
    }
    ```

#### `GET /auth/user/`
Getting information about the currently authenticated user.
- **Authentication:** Required (Bearer Token).
-   **Headers:** `Authorization: Bearer <access_token>`
-   **Success Response (200 OK):**
    ```json
    {
      "id": "uuid-string",
      "email": "user@example.com",
      "name": "John Doe"
    }
    ```

#### `POST /auth/logout/`
User logout (adding refresh token to the blacklist).
- **Authentication:** Required (Bearer Token).
-   **Request Body:**
    ```json
    {
      "refresh": "refresh_token_string"
    }
    ```
-   **Success Response (200 OK):**
    ```json
    {
      "message": "Successfully logged out"
    }
    ```

### 6.2. Hotels and Reviews

#### `GET /hotels/`
Getting a list of all hotels with pagination.
- **Authentication:** Not required.
-   **Success Response (200 OK):**
    ```json
    {
      "count": 1,
      "next": null,
      "previous": null,
      "results": [
        {
          "id": "uuid", "name": "Hotel Name", ...
        }
      ]
    }
    ```

#### `GET /hotels/{id}/`
Getting detailed information about one hotel.
- **Authentication:** Not required.
-   **Success Response (200 OK):**
    ```json
    {
      "id": "uuid", "name": "Hotel Name", "description": "...", ...
    }
    ```

#### `GET /hotels/{id}/reviews/`
Getting a list of reviews for a specific hotel.
- **Authentication:** Not required.
-   **Success Response (200 OK):**
    ```json
    {
      "count": 1,
      "next": null,
      "previous": null,
      "results": [
        {
          "id": "uuid", "user_email": "user@example.com", ...
        }
      ]
    }
    ```

#### `POST /reviews/`
Create a new review.
- **Authentication:** Required (Bearer Token).
-   **Request Body:**
    ```json
    {
      "hotel": "hotel_uuid",
      "rating": 5,
      "title": "Great stay!",
      "content": "Loved this hotel..."
    }
    ```
-   **Success Response (201 Created):** JSON with the data of the created review.

### 6.3. Directions

#### `GET /destinations/`
Getting a list of all directions.
- **Authentication:** Not required.
-   **Success Response (200 OK):** A list of destination objects in the 'results` field.

#### `GET /destinations/{id}/`
Getting detailed information about one direction.
- **Authentication:** Not required.
-   **Success Response (200 OK):** A JSON object with direction data.

### 6.4. Reservations

#### `GET /bookings/`
Getting a list of the current user's bookings.
- **Authentication:** Required (Bearer Token).
-   **Success Response (200 OK):** A list of booking objects in the 'results` field.

#### `POST /bookings/`
Create a new booking.
- **Authentication:** Required (Bearer Token).
-   **Request Body:**
    ```json
    {
      "hotel_id": "hotel_uuid",
      "check_in": "2024-08-10",
      "check_out": "2024-08-15",
      "guests": 2,
      "total_price": 750.00,
      "guest_email": "user@example.com",
      "guest_name": "John Doe"
    }
    ```
-   **Success Response (201 Created):** JSON with the data of the created booking (status `pending').

#### `POST /bookings/{id}/cancel/`
Cancellation of the booking. The status changes to `cancelled`.
- **Authentication:** Required (Bearer Token).
-   **Success Response (200 OK):**
    ```json
    {
      "id": "uuid",
      "status": "cancelled"
    }
    ```