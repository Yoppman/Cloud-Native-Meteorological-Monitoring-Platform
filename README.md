
# Cloud-Native Meteorological Monitoring Platform

## Overview

This project provides a cloud-native platform for monitoring meteorological data such as earthquakes, reservoir levels, and electricity usage. It leverages Docker containers for separation of concerns, making the application modular, scalable, and easy to deploy. The platform includes both frontend and backend services that interact with a PostgreSQL database, with data visualized through Grafana and monitored by Prometheus.

## Architecture



The application is containerized using Docker Compose and consists of five core containers:
- **Container-1 (Database)**: A PostgreSQL database that handles data read and write operations.
- **Container-2 (Reservoir)**: Responsible for fetching and processing reservoir data.
- **Container-3 (Earthquake)**: Manages earthquake data processing.
- **Container-4 (Electricity)**: Collects and processes electricity data.
- **Container-5 (Frontend)**: Interacts with the backend containers to display meteorological data to users.

![Architecture Diagram](Container_Architecture.png)

## Backend

### Structure

The backend handles data collection, processing, and serving API requests for the frontend. It consists of Python scripts that interact with the database and perform specific tasks such as crawling meteorological data.

**Backend Directory Structure**:
```
backend/
├── __pycache__/                # Cached Python files
├── data/db/                    # PostgreSQL configuration
├── grafana/                    # Grafana setup for visualization
├── prometheus/                 # Prometheus for monitoring
├── Dockerfile_*                # Docker setup for each service (earthquake, reservoir, electricity, etc.)
├── earthquake.py               # Script for earthquake data processing
├── electricity.py              # Script for electricity data processing
├── reservoir.py                # Script for reservoir data processing
├── test_*.py                   # Unit tests for backend services
├── requirements.txt            # Python dependencies
```

### Key Features
- **Data Crawling**: The backend services fetch meteorological data from external sources and store it in the PostgreSQL database.
- **Monitoring**: Prometheus collects metrics, and Grafana visualizes the data.

### Running the Backend

1. Build the Docker containers:
   ```bash
   docker-compose up --build
   ```
2. View logs to check the status of each container:
   ```bash
   docker-compose logs
   ```

## Frontend

### Structure

The frontend is a React-based application that fetches data from the backend containers and displays it in a user-friendly interface.

**Frontend Directory Structure**:
```
frontend/
├── public/                     # Static files
├── src/                        # React source files
│   ├── App.js                  # Main application component
│   ├── components/             # Reusable UI components
│   ├── services/               # API calls to backend services
├── Dockerfile                  # Docker setup for the frontend
├── package.json                # Frontend dependencies
```

### Key Features
- **Visualization**: Fetches data from the backend and displays it to the user.
- **Real-time Monitoring**: Integrates with the backend to visualize real-time meteorological data.

### Running the Frontend

1. Navigate to the `frontend` directory:
   ```bash
   cd frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run the application:
   ```bash
   npm start
   ```

## Cloud Deployment

### Docker Compose

The project uses Docker Compose to orchestrate the backend, frontend, and supporting services (PostgreSQL, Grafana, Prometheus).

1. **Build and Run** the containers:
   ```bash
   docker-compose up --build
   ```
2. **Access Services**:
   - Frontend: [http://localhost:3000](http://localhost:3000)
   - Grafana: [http://localhost:3001](http://localhost:3001)
   - Prometheus: [http://localhost:9090](http://localhost:9090)

### Monitoring and Visualization
- **Prometheus**: Collects metrics from the backend containers.
- **Grafana**: Displays real-time data visualizations from Prometheus.