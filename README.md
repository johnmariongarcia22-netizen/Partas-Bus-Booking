# Partas Bus Booking

An online bus-reservation system for **Partas Transportation Company, Inc.**, a provincial bus line
running between Metro Manila (Cubao) and the Ilocos region (Laoag, Vigan, Pagudpud).

> Student project for a class requirement. It is **not** the official Partas website, and the routes,
> schedules and fares in the database are **sample data**.

## Problem being solved

Passengers on long-distance routes usually line up at the terminal to reserve seats, and staff track
reservations by hand. This system lets passengers book, change and cancel seats online, and lets the
company manage its trips and see every booking in one place.

**Who uses it**
- **Customers** register, book trips, and manage their own bookings.
- **Admin (company staff)** manage the list of trips and can view, edit or delete any booking.

## Features

**Landing page** (public, mobile-friendly)
- Business name and description, services, bus illustration, sample trips.
- Call-to-action buttons: *Register to Book*, *Login*, and *Book Now* once signed in.

**Users**
- Register (name, email, password), Login, Logout.
- Passwords are hashed with Werkzeug (scrypt); plain-text passwords are never stored.
- Two roles: **admin** and **customer**. Customers can only see and change their own bookings;
  admin pages return 403 for customers.
- Pages needing an account redirect to the login page when signed out.
- Every form carries a CSRF token.

**CRUD**
- **Bookings** (core entity): create, view, edit and delete, with validation (valid trip, date not in
  the past, 1-10 passengers, required name, PH mobile number, seats still available) and a
  confirmation dialog before delete.
- **Trips** (admin only): full CRUD as well; a trip that already has bookings cannot be deleted.
- Data is stored in SQLite (`instance/partas.db`), so it persists across restarts.

## Tech stack

Python 3.10+, Flask, SQLite (standard library), Jinja2 templates, plain HTML/CSS (no JavaScript framework).

## Setup and run

```bash
git clone <your-repo-url>
cd partas-booking
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

Open file:///C:/Users/admin/Downloads/partas_bus_booking_web_app.html. On first run the database, sample trips and the two test accounts below
are created automatically. A session secret is generated into `instance/secret.key` (git-ignored); you
can override it with the `SECRET_KEY` environment variable.

Run the automated smoke tests (uses a temporary database): `python test_app.py`

## Test accounts

| Role | Email | Password |
|---|---|---|
| Admin | admin@partas.test | Admin123! |
| Customer | juan@example.com | Customer123! |

These are demo credentials for grading only. Change them before any real deployment.

## Project structure

```
app.py            routes, validation, database setup
templates/        Jinja2 pages (base layout, landing, auth, bookings, trips)
static/           style.css and bus.svg
test_app.py       smoke tests
requirements.txt  dependencies
```

## AI tools used

- **Claude (Anthropic)**: generated the first version of the code, templates, styling, the bus
  illustration, tests and this README from the class requirements. I reviewed and tested the result.

<!-- Student: edit this section so it is accurate for you, and list any other AI tools you used. -->
