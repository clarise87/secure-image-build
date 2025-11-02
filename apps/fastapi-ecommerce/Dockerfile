# syntax=docker/dockerfile:1
FROM python:3.11-slim
ENV PYTHONDONTWRITEBYTECODE=1 \
PYTHONUNBUFFERED=1 \
PIP_NO_CACHE_DIR=1
# install dependencies for building python packages
RUN apt-get update && apt-get install -y gcc libffi-dev build-essential
# creat app directory
WORKDIR/APP
RUN useradd -m -u 1000 appuser
WORKDIR /app
COPY requirements.txt ./
# upgrade pip and install requirments
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirments.txt
# copy all project files including requirments.txt
COPY . ./
# creat and use a non-root user
RUN useradd -m -u 1000 appuser
RUN chown -R appuser:appuser /app
USER appuser
EXPOSE 3000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "3000"]
