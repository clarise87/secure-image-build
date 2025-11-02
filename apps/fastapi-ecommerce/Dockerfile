
# syntax=docker/dockerfile:1
FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1

# Install dependencies for building Python packages
RUN apt-get update && apt-get install -y gcc libffi-dev build-essential

# Create app directory
WORKDIR /app

# Create and use a non-root user
RUN useradd -m -u 1000 appuser

# Copy requirements file
COPY requirements.txt ./

# Upgrade pip and install requirements
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt

# Copy all project files
COPY . ./

# Set ownership to non-root user
RUN chown -R appuser:appuser /app

USER appuser

EXPOSE 3000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "3000"]
