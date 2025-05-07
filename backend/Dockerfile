# Use a slim Python base image
FROM python:3.10-slim

# Copy and install system packages (ffmpeg, etc.)
COPY apt-packages.txt .
RUN apt-get update \
    && xargs -a apt-packages.txt apt-get install -y \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy and install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of your backend code
COPY . .

# Expose the port Railway will use
ENV PORT 8000
EXPOSE 8000

# Start the app with Gunicorn
CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:8000", "--workers", "4"]