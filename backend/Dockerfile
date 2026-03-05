FROM python:3.12-slim AS quality
WORKDIR /app

# Patch sécurité OS (glibc, etc.) demander par Trivy
RUN apt-get update \
 && apt-get upgrade -y \
 && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app ./app
RUN ruff check app && black --check app


# Image docker propre apres les tests de qualités
FROM python:3.12-slim
WORKDIR /app

# Patch sécurité OS (glibc, etc.) demander par Trivy
RUN apt-get update \
 && apt-get upgrade -y \
 && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app ./app

EXPOSE 8000
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
