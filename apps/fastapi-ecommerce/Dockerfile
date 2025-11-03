
# syntax=docker/dockerfile:1
FROM python:3.11-slim
ENV PYTHONDONTWRITEBYTECODE=1 \
PYTHONUNBUFFERED=1 \
PIP_NO_CACHE_DIR=1
RUN useradd -m -u 1000 appuser
WORKDIR /app
# copy only requirments first, then install dependencies
COPY requirements.txt ./
RUN pip install --upgrade pip && \ 
pip install  --no-cache-dir -r
requirements.txt
# then copy the rest of the project files
COPY . .
RUN chown -R appuser:appuser /app
USER appuser
EXPOSE 3000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "3000"]
