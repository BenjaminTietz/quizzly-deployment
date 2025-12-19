# ===============================
# Backend Dockerfile (Django)
# ===============================

FROM python:3.12-slim

# Prevent Python from writing pyc files
ENV PYTHONDONTWRITEBYTECODE=1
# Ensure logs are flushed directly
ENV PYTHONUNBUFFERED=1

# Set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    ffmpeg \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY backend/requirements.txt .
RUN pip install --upgrade pip && pip install -r requirements.txt

# Copy backend source code
COPY backend/ .

# Expose application port
EXPOSE 8000

# Start Django with Gunicorn
CMD ["gunicorn", "quizzly_backend.wsgi:application", "--bind", "0.0.0.0:8000"]
