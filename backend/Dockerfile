FROM python:3.11-slim

WORKDIR /app

# Prevent python from writing pyc files to disc and enable unbuffered terminal logging
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Install dependencies needed for compiling or connecting if necessary
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy backend source code
COPY . .

EXPOSE 8000

# Start the backend server
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]