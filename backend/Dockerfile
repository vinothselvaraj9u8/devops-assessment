# -------- Stage 1: Build --------
FROM python:3.12-slim AS builder

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/*

# Copy dependency file
COPY requirements.txt .

# Install python dependencies
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# -------- Stage 2: Runtime --------
FROM python:3.12-slim

# Create non-root user
RUN useradd -m appuser

WORKDIR /app

# Copy installed packages from builder
COPY --from=builder /usr/local /usr/local

# Copy project files
COPY . .

# Set permissions
RUN chown -R appuser:appuser /app

USER appuser

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
