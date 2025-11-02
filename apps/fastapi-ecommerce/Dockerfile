# syntax=docker/dockerfile:1
FROM python:3.10-slim

# Install system packages needed for pip and Python builds
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy requirements and install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
# Create virtualenv
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install --upgrade pip setuptools wheel
pip install -r requirements.txt
pip install --no-cache-dir -r requirements.txt
set -e  # Exit immediately if a command fail
pip install -r requirements.txt | tee install.log
