# ---------- build stage ----------
FROM python:3.12-slim AS build
WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends gcc \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip wheel --no-cache-dir --wheel-dir /wheels -r requirements.txt

# ---------- runtime stage ----------
FROM python:3.12-slim
WORKDIR /app

# create non-root user
RUN useradd -m appuser
RUN mkdir -p /data && chown -R appuser:appuser /data
USER appuser

COPY --from=build /wheels /wheels
RUN pip install --no-cache-dir /wheels/*

COPY --chown=appuser:appuser . .

EXPOSE 8000
CMD ["python","manage.py","runserver","0.0.0.0:8000"]
