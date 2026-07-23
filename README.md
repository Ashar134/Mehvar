<p align="center">
  <img src="./assets/banner.svg" alt="SAGE Demo" width="100%">
</p>


# Mehvar

> *"Mehvar" - the axis, the pivot, the foundation on which everything turns.*

A web-based construction project bidding platform that connects clients and builders through transparent, competitive, and trust-driven collaboration.

---

## What is Mehvar?

Construction projects fail not because of bad builders - they fail because the right builder never found the right client.

**Mehvar** is built to fix that.

It is a platform where clients post their projects and builders compete for them - not through backroom deals or referral chains, but through open, merit-based bidding. Every proposal, every rating, every completed project lives on the platform. The result is an ecosystem where trust is earned publicly and work is won fairly.

---

## The Problem It Solves

| Challenge | How Mehvar Addresses It |
|---|---|
| Clients don't know who to trust | Builder ratings and reviews are visible before a bid is accepted |
| Builders waste time chasing unserious clients | Clients post structured projects with budgets and timelines |
| Payments feel risky without contracts | Stripe-integrated payments release only upon project milestones |
| No material sourcing in one place | A live vendor marketplace connects builders with suppliers |
| Profiles feel anonymous and generic | Rich customizable profiles for both clients and builders |

---

## Core Features

### Post and Bid System
Clients describe their project - type, budget, timeline, location - and publish it. Builders review the brief and submit detailed proposals including their estimated cost and delivery timeline. The client evaluates all bids side by side and awards the project.

### Transparent Bidding
Every bid is visible in its relevant context. Builders compete on merit. No hidden negotiations, no favoritism by default - just proposals that speak for themselves.

### Review and Rating System
After a project is completed, both parties leave reviews. Ratings accumulate on builder profiles over time, creating a public track record that new clients can rely on. Builders with better histories naturally rise above the rest.

### Vendor Marketplace
A dedicated marketplace for construction materials and accessories. Builders can browse products by category, see vendor contact details, and source materials without leaving the platform.

### Secure Payments via Stripe
Payment processing is handled through the Stripe API. Clients are charged only when a project reaches agreed-upon milestones, and the payment flow is designed to protect both sides.

### Profile Management
Clients and builders each have their own profile space - including company name, location, specialization, experience, and a profile picture. These are not vanity pages; they are trust signals that influence bidding decisions.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3, Flask |
| Frontend | HTML, CSS, Jinja2 Templates |
| Database | MySQL (via SQLAlchemy ORM) |
| Payment Gateway | Stripe API |
| Auth | Werkzeug password hashing, Flask sessions |

---

## Project Structure

```
Mehvar/
├── app/
│   ├── __init__.py           # App factory, blueprint registration
│   ├── models.py             # SQLAlchemy models (User, Client, Builder, Project, Bid, ...)
│   ├── routes/
│   │   ├── auth_routes.py    # Signup, login, logout
│   │   ├── client_routes.py  # Client dashboard, project posting, bid review
│   │   └── builder_routes.py # Builder dashboard, bidding, marketplace
│   ├── templates/
│   │   ├── auth/             # Login and signup pages
│   │   ├── client/           # Client-facing views
│   │   └── builder/          # Builder-facing views
│   └── static/               # CSS, JS, images
├── config.py                 # Database URI, secret keys, Stripe config
├── run.py                    # App entry point
├── seed_marketplace.py       # Script to populate marketplace with sample data
└── ClickNBuild.sql           # Full database dump with schema and seed data
```

---

## Data Models at a Glance

```
User ──┬──> Client ──> Project ──> Bid <── Builder
       │                     └──> Review
       │                     └──> Payment
       └──> Builder ──> VendorMarketplace
```

- **User** - shared authentication entity (email, hashed password, role)
- **Client** - company info, location, project history
- **Builder** - specialization, experience, ratings, earnings
- **Project** - type, budget, timeline, status, assigned builder
- **Bid** - cost estimate, proposal text, status per builder
- **Review** - bidirectional (client reviews builder, builder reviews client)
- **Payment** - tracked per project, integrated with Stripe
- **VendorMarketplace** - product listings with category, price (PKR), vendor info

---

## Getting Started

### Prerequisites

- Python 3.8+
- MySQL (running locally or remotely)
- pip

### 1. Clone the Repository

```sh
git clone https://github.com/Ashar134/Mehvar.git
cd Mehvar
```

### 2. Install Dependencies

```sh
pip install flask flask_sqlalchemy pymysql werkzeug stripe
```

### 3. Configure the Application

Open `config.py` and update the following:

```python
SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://your_user:your_password@localhost/ClickNBuild'
SECRET_KEY = 'your-secret-key'
STRIPE_SECRET_KEY = 'your-stripe-secret-key'
STRIPE_PUBLISHABLE_KEY = 'your-stripe-publishable-key'
```

### 4. Set Up the Database

Import the provided SQL dump to create and seed the database:

```sh
mysql -u root -p -e "CREATE DATABASE ClickNBuild;"
mysql -u root -p ClickNBuild < ClickNBuild.sql
```

Alternatively, to seed only the marketplace:

```sh
python seed_marketplace.py
```

### 5. Run the Application

```sh
python run.py
```

The app will be available at `http://127.0.0.1:5000`.

---

## User Roles

**Client**
- Register an account with the Client role
- Post construction projects with details and budget
- Review incoming bids from builders
- Accept a bid and initiate payment
- Mark a project complete and leave a review

**Builder**
- Register an account with the Builder role
- Browse open projects and submit bids
- Manage active bids from the dashboard
- Mark projects complete after delivery
- Build a public track record through ratings

---

## Application Routes

| Route | Role | Description |
|---|---|---|
| `/signup` | Public | Registration and login page |
| `/register` | Public | Form POST - creates new user |
| `/login` | Public | Form POST - authenticates user |
| `/logout` | Authenticated | Clears session |
| Client routes | Client | Home, project posting, bid management |
| Builder routes | Builder | Dashboard, bidding, marketplace |

---

## Security Notes

- Passwords are hashed using `werkzeug.security.generate_password_hash` (PBKDF2-SHA256)
- Sessions are server-side using Flask's signed cookie mechanism
- Stripe test mode is used by default - switch to live keys for production
- The `SECRET_KEY` in `config.py` **must** be replaced before any production deployment

---

## Built By

Developed as part of a 6th Semester Web Engineering course project.

The name *Mehvar* (محور) is an Urdu and Persian word meaning **axis** or **pivot** - the central point around which everything revolves. In construction, the foundation is everything. This platform was built with that same principle in mind: reliable infrastructure that people can build on top of.

---

## License

This project is for academic and demonstration purposes. All rights reserved by the original authors.
