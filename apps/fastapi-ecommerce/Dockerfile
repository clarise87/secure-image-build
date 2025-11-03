
# syntax=docker/dockerfile:1
FROM python:3.11-slim
ENV PYTHONDONTWRITEBYTECODE=1 \
PYTHONUNBUFFERED=1 \
PIP_NO_CACHE_DIR=1
# creat a non -root user
RUN useradd -m -u 1000 appuser
# set work directory
WORKDIR /app
# copy only requirement file first [for docker caching]
COPY requirements.txt ./
# install dependencies
RUN pip install --no-cache-dir -r
requirements.txt
# copy the rest of the app
COPY . ./
# Adjust permissions
RUN chown -R appuser:appuser /app
# switch to non root user
USER appuser
# expose the app port
EXPOSE 3000
# start the fastAPI aoo with uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "3000"]
