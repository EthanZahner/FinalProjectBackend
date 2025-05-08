# FinalProjectBackend
# Event Ticketing System REST API

A Node.js/Express/MongoDB REST API for an Event Ticketing System.  
Users can register, authenticate via JWT, browse events, book tickets (with seat-capacity checks), and receive QR-coded tickets (plus optional email confirmation). Admins can manage events and view booking dashboards.

---

## Table of Contents

- [Features](#features)  
- [Tech Stack](#tech-stack)  
- [Prerequisites](#prerequisites)  
- [Installation](#installation)  

---

## Features

- **User Management**: register & login with secure password hashing (bcryptjs)  
- **JWT Authentication**: stateless auth, role-based access (user vs. admin)  
- **Events CRUD**: admins can create, update, delete events; public can list & filter  
- **Ticket Booking**: users can book tickets, seat-capacity enforced  
- **QR Codes**: generate & store QR code for each booking  
- **Ticket Validation**: validate tickets by scanning booking ID  
- **Email Confirmations**: send booking receipts via Nodemailer  
- **Admin Dashboard**: view events with lists of booking users  

---

## Tech Stack

- **Node.js** & **Express**  
- **MongoDB** with **Mongoose** ODM  
- **bcryptjs** for password hashing  
- **jsonwebtoken** for JWTs  
- **qrcode** for QR code generation  
- **nodemailer** for email  
- **Render.com** for deployment  

---

## Prerequisites

- [Node.js](https://nodejs.org/) v16+  
- [npm](https://npmjs.com/)  
- A [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) cluster (or local MongoDB)  
- (Optional) A Gmail account or SMTP server for email  

---

## Installation

1. **Clone the repo**  
   ```bash
   git clone https://github.com/EthanZahner/FinalProjectBackend.git
   cd FinalyProjectBackend/ticketingSystem
2. Install dependenceis
    npm install

3.create a .env
  # .env

MONGODB_URI="mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<dbname>?retryWrites=true&w=majority"
JWT_SECRET="<your_jwt_secret>"
EMAIL_USER="<your_email_address>"
EMAIL_PASS="<your_email_password_or_app_password>"
PORT=5000        # optional, default is 5000


API Endpoints

Auth

POST	/api/auth/register	Register new user

POST	/api/auth/login	Login, receive JWT

Events (Public & Admin)

GET	/api/events	—	List all events (supports ?category= & ?date= filters)
GET	/api/events/:id	—	Get event details by ID
POST	/api/events	Admin JWT	Create a new event
PUT	/api/events/:id	Admin JWT	Update an event (cannot reduce seatCapacity below bookedSeats)
DELETE	/api/events/:id	Admin JWT	Delete event (fails if bookings exist)
GET	/api/events/report/bookings-per-event	Admin JWT	Admin dashboard: events with booking users

Bookings (User & Bonus)

GET	/api/bookings	User JWT	List bookings for current user
GET	/api/bookings/:id	User JWT	Get one booking (ownership enforced)
POST	/api/bookings	User JWT	Create a booking (seat check + QR)
GET	/api/bookings/validate/:code	(Opt’l)	Validate ticket by booking ID
