# Backlink Service Project

This project is a **Backlink Service** web application that scans websites and publishes articles containing backlinks to customer sites. The application consists of the following components:
- **Backend**: A Django-based REST API running inside a Docker container.
- **Frontend**: A Vue.js web application running inside a Docker container.
- **Database**: A PostgreSQL database running inside a Docker container.

## Table of Contents

1. [Project Structure](#project-structure)
2. [Technologies Used](#technologies-used)
3. [Setting Up the Project](#setting-up-the-project)
4. [Running the Project](#running-the-project)
5. [Docker Setup](#docker-setup)
6. [Useful Commands](#useful-commands)

---

## Project Structure

. 
├── Backend/ # Django backend 
├── Frontend/ # Vue.js frontend 
├── docker-compose.yml # Docker Compose file to orchestrate services 
└── README.md # Project-level documentation

## Technologies Used

- **Backend**: Python 3.11, Django, Django REST Framework
- **Frontend**: Vue.js, Node.js
- **Database**: PostgreSQL
- **Containerization**: Docker, Docker Compose

## Setting Up the Project

### Prerequisites

Make sure you have the following installed on your machine:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Cloning the Repository

1. Clone the repository:

    git clone https://github.com/your-username/backlink-service.git
    cd backlink-service

### Environment Variables

Create a `.env` file at the root of the project with the following content:

POSTGRES_DB=mydb
POSTGRES_USER=myuser
POSTGRES_PASSWORD=mypassword
DB_HOST=db
DB_PORT=5432

## Running the Project

### Starting Services
To build and run the containers, use the following commands:

docker-compose up --build

This will:

Build the backend, frontend, and db services.
Use wait-for-it.sh to ensure the backend waits for the database to be ready.
Automatically run database migrations on the backend container.

### Accessing the Services
Backend: The Django REST API will be available at http://localhost:8001.
Frontend: The Vue.js web application will be available at http://localhost:8081.

## Docker Setup

### Backend Service
Dockerfile: The Backend/Dockerfile installs the necessary dependencies, downloads wait-for-it.sh, and starts the Django development server.
Migrations: The container automatically runs makemigrations and migrate before starting the server.

### Frontend Service
Dockerfile: The Frontend/Dockerfile installs Node.js and Vue.js dependencies, and runs the development server.

### PostgreSQL Database
Image: postgres:14
Persistent Storage: Data is stored in a Docker volume (postgres_data).

## Useful Commands

### Rebuilding Containers
If you need to rebuild the containers:

docker-compose down
docker-compose up --build

### Running Migrations Manually
If you want to run migrations manually:

docker-compose exec backend python manage.py makemigrations
docker-compose exec backend python manage.py migrate

### Accessing the Database
You can access the PostgreSQL database via the command line:

docker-compose exec db psql -U myuser -d mydb

### Cleaning Up
If you want to stop the services and clean up the resources:

docker-compose down
docker system prune