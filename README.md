# Kotsek: Real-Time Vehicle & License Plate Recognition System

This project is a full-stack web application for real-time vehicle and license plate recognition. It uses a Python backend with YOLO and PaddleOCR to process a video stream, detect vehicles, and perform Automatic Number Plate Recognition (ANPR). The results, including annotated video frames and detection data, are streamed in real-time to a Next.js web client using Socket.IO.

The entire application is containerized using Docker for easy setup and deployment.

## Features

* **Real-Time Video Processing:** Ingests a video feed and processes it frame-by-frame.
* **Object Detection:** Utilizes a YOLO model (`best.pt`) to detect vehicles and license plates in the stream.
* **License Plate Recognition (ANPR):** Employs PaddleOCR to extract alphanumeric text from the detected license plates.
* **Real-Time Streaming:** Streams annotated video and JSON detection data (label, color, confidence, coordinates, OCR text) to the client via Socket.IO.
* **Full-Stack Application:** Features a Next.js frontend and a Flask backend.
* **Containerized:** Fully containerized with Docker and managed via `docker-compose` for simple, reproducible builds.

## Tech Stack

### Backend (`flask_api`)
* **Framework:** Flask
* **Real-Time:** Flask-SocketIO
* **AI / ML:**
    * Ultralytics (YOLO) for object detection
    * PaddleOCR for ANPR/text extraction
    * OpenCV for video processing
* **Database:** Flask-SQLAlchemy, Flask-Migrate, psycopg2 (PostgreSQL)

### Frontend (`client`)
* **Framework:** Next.js
* **Language:** TypeScript
* **Real-Time:** Socket.IO Client
* **Styling:** Tailwind CSS (implied from `package.json`)

### DevOps
* **Containerization:** Docker & Docker Compose
* **Utilities:** Makefile (for command shortcuts)

## Getting Started

### Prerequisites

* [Docker](https://www.docker.com/get-started)
* [Docker Compose](https://docs.docker.com/compose/install/)

### Installation & Running

A `Makefile` is provided for convenient commands.

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/bl4ckkl1st3d/kotsek.git](https://github.com/bl4ckkl1st3d/kotsek.git)
    cd kotsek
    ```

2.  **Build the Docker Containers**
    This command will build both the `flask_api` and `client` services as defined in the `docker-compose.yaml`.
    ```bash
    make build
    ```
    *Alternatively, using Docker Compose directly:*
    ```bash
    docker-compose build
    ```

3.  **Run the Application**
    This will start both services in detached mode. The `client` service will wait for the `flask_api` to be ready before starting.
    ```bash
    make run
    ```
    *Alternatively, using Docker Compose directly:*
    ```bash
    docker-compose up -d
    ```

### Accessing the Application

Once the containers are running:

* **Frontend (Next.js):** [http://localhost:3000](http://localhost:3000)
* **Backend (Flask API):** [http://localhost:5001](http://localhost:5001)

## Available Commands

The following commands are available via the `Makefile`:

* `make build`: Build the Docker images for all services.
* `make run`: Start the services in detached mode.
* `make stop`: Stop and remove the running containers.
* `make restart`: A shortcut for `make stop` followed by `make run`.
* `make rebuild`: Stop, remove volumes, and rebuild all services from scratch.
* `make log`: View the logs for the `flask_api` service.
