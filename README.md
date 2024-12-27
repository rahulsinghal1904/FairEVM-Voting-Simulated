# FairEVM-Voting-Simulated

## Overview
This project is a real-time polling application built with **FastAPI** for the backend, **Next.js** for the frontend, and **SQLAlchemy** ORM for database models. The application uses **Tailwind CSS** for styling and supports real-time updates via **WebSocket** connections.

---

## Features
- **Real-time polling:** Users can see live updates to polls as they occur.
- **Authentication:** Managed via FastAPI middleware with session-based cookies.
- **Database Models:** Polls, options, and votes are modeled using SQLAlchemy.
- **Frontend:** A responsive Next.js UI with Tailwind CSS styling.
- **WebSocket Updates:** Connected clients receive real-time updates when polls are updated.

---

## Tech Stack
- **Backend:** FastAPI
- **Frontend:** Next.js, Tailwind CSS
- **Database:** SQL (using SQLAlchemy for ORM)
- **WebSocket Support:** FastAPI WebSocket handlers
- **Authentication:** Session-based cookies

---

## Database Models

### 1. Poll
- Represents a poll.
- Fields: `id`, `title`, `created_at`, `updated_at`

### 2. Option
- Represents an option in a poll.
- Fields: `id`, `poll_id`, `text`

### 3. Vote
- Represents a vote on a poll option.
- Fields: `id`, `user_id`, `option_id`

---

## API Endpoints

### 1. **Get All Polls**
- **Endpoint:** `GET /polls`
- **Description:** Fetch all polls.

### 2. **Get Poll by ID**
- **Endpoint:** `GET /polls/{id}`
- **Description:** Fetch a specific poll by ID.

### 3. **Delete Poll**
- **Endpoint:** `DELETE /polls/{id}`
- **Description:** Delete a specific poll by ID.

### 4. **Post Vote**
- **Endpoint:** `POST /polls/{id}/vote`
- **Description:** Submit a vote for a poll.

### 5. **User ID from Cookie**
- **Dependency:** Extracts the user ID from a session-based cookie for authentication.

---

## WebSocket Handlers

### Functionality
1. **Separate Clients by Polls:** WebSocket connections are organized by poll IDs.
2. **Connection Management:** Validates poll ID and manages connections.
3. **Real-time Updates:** Sends updates to connected clients when votes are cast or a poll is updated.

### Handlers
- **Accept Connection:** Validates and manages client connections.
- **Poll Updates:** Broadcasts updates to connected clients.
- **Close Connection:** Closes connections when the poll ends.

---

## Frontend Implementation

### Homepage
- Displays all polls fetched from the `GET /polls` API endpoint.
- Uses a local state variable to map results to the UI.

### Poll Page
- Displays poll details and allows users to vote.
- Real-time updates are reflected using WebSocket messages.

### Delete Poll
- Uses the `DELETE /polls/{id}` endpoint to remove a poll.
- Updates the UI after successful deletion.

---

## Installation and Setup

### Prerequisites
- Python 3.8+
- Node.js 16+
- SQL Database (e.g., PostgreSQL, MySQL, SQLite)

### Backend Setup
1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd backend
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Configure the database:
   - Update the connection string in `settings.py`.
   - Run migrations:
     ```bash
     alembic upgrade head
     ```
4. Start the FastAPI server:
   ```bash
   uvicorn app.main:app --reload
   ```

### Frontend Setup
1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```

---

## Usage
1. Access the application at `http://localhost:3000`.
2. View, create, and vote on polls.
3. Watch real-time updates as other users vote.

---

## Contributing
1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature
   ```
3. Commit your changes:
   ```bash
   git commit -m "Add your feature description"
   ```
4. Push to the branch:
   ```bash
   git push origin feature/your-feature
   ```
5. Submit a pull request.
