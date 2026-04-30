# Flask EC2 Deployment Project

## Project Overview
## Project Overview
This project demonstrates a production-style deployment of a Flask web application on AWS EC2 using Gunicorn, Nginx, and systemd.

The application is also containerized with Docker, orchestrated with Docker Compose, and integrated with GitHub Actions CI/CD for automated testing and deployment.

## Tech Stack
- Python 3
- Flask
- Gunicorn
- Nginx
- systemd
- Docker
- Docker Compose
- GitHub Actions
- AWS EC2 (Ubuntu)
- Git + GitHub

## Architecture
Client (Browser) → Nginx (Reverse Proxy) → Gunicorn (WSGI Server) → Flask Application

### Docker Runtime Architecture
Client → Docker Container → Gunicorn → Flask Application

### CI/CD Workflow
Developer Push → GitHub Actions CI → GitHub Actions CD → AWS EC2 Deployment

## Features
- Flask web application
- Health check endpoint: `/health`
- Gunicorn as WSGI server
- Nginx reverse proxy
- systemd service management
- Docker support
- Docker Compose support
-- GitHub Actions CI/CD pipeline
- Deployment on AWS EC2

## Endpoints

### GET /
Returns:

```text
OK 
```

GET /health

Returns:

```text
{"status":"ok"}
```

## Deployment Steps

### 1. Clone repository
```text
git clone https://github.com/nikanikanikaa98-byte/flask-aws-ec2-docker-deployment.git
cd flask-aws-ec2-docker-deployment
```

### 2. Create virtual environment
```text
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies
```text
pip install -r requirements.txt
```

### 4. Run with Gunicorn
```text
gunicorn --workers 3 --bind 127.0.0.1:5000 wsgi:app
systemd Service 
```

This project is configured to run with systemd on Ubuntu.

### Example service startup check:

```text
sudo systemctl status myapp
```

## Docker Support 

This project can also be run inside a Docker container.

### Build Docker image

```text
docker build -t flask-docker-app .
```

### Run Docker container

```text
docker run -d -p 5001:5000 --name flask-container flask-docker-app
```

### Test Docker container

```text
curl http://127.0.0.1:5001/
curl http://127.0.0.1:5001/health
```

Expected responses:

```text
/ → OK
/health → {"status":"ok"}
```

## Docker Compose Support

This project can also be started with Docker Compose.

### Run with Docker Compose
```bash
docker compose up -d 
```

## CI/CD

This project includes a GitHub Actions CI/CD pipeline.

### CI
On every push to `main`, GitHub Actions:
- installs dependencies
- checks Flask app import
- builds Docker image
- starts the app with Docker Compose
- tests the `/health` endpoint

### CD
After successful CI, GitHub Actions:
- connects to the EC2 server over SSH
- pulls the latest code from GitHub
- installs dependencies
- restarts the `myapp` systemd service
## Project Files

- app.py
- wsgi.py
- requirements.txt
- Dockerfile
- .dockerignore
- README.md
- `.github/workflows/ci.yml` — CI pipeline with GitHub Actions
- `.github/workflows/cd.yml` — CD pipeline for EC2 deployment
## What I Learned
- How to deploy a Flask application on AWS EC2
- How to configure Gunicorn as a production WSGI server
- How to use Nginx as a reverse proxy
- How to manage application startup with systemd
- How to containerize a Python web application with Docker
- How to work with Linux-based deployment workflows

## Notes

This project started as a basic Flask deployment on EC2 and was later improved with Docker support for containerized execution.
