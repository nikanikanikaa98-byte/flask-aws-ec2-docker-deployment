# Flask EC2 Deployment Project

## Project Overview
This project demonstrates a production-style deployment of a Flask web application on AWS EC2 using Gunicorn, Nginx, and systemd.

The application can also be packaged and run inside a Docker container, which makes the project more portable and closer to a real-world deployment workflow.

## Tech Stack
- Python 3
- Flask
- Gunicorn
- Nginx
- systemd
- Docker
- AWS EC2 (Ubuntu)
- Git + GitHub

## Architecture
Client (Browser) → Nginx (Reverse Proxy) → Gunicorn (WSGI Server) → Flask Application

### Docker Runtime Architecture
Client → Docker Container → Gunicorn → Flask Application

## Features
- Flask web application
- Health check endpoint: `/health`
- Gunicorn as WSGI server
- Nginx reverse proxy
- systemd service management
- Docker support
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

### Docker Support 

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

## Project Files
- app.py
- wsgi.py
- requirements.txt
- Dockerfile
- .dockerignore
- README.md

## What I Learned
- How to deploy a Flask application on AWS EC2
- How to configure Gunicorn as a production WSGI server
- How to use Nginx as a reverse proxy
- How to manage application startup with systemd
- How to containerize a Python web application with Docker
- How to work with Linux-based deployment workflows

## Notes

This project started as a basic Flask deployment on EC2 and was later improved with Docker support for containerized execution.
