FROM python:3.9-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Install needed system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    libxml2-dev \
    libxslt-dev \
    libssl-dev \
    build-essential \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# coping the repo into continer
COPY . /app/

# Installing dependencies
RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# Install the custom Cryptography library from the local folder
#RUN pip install /app/cryptography-master

VOLUME ["/app"]

CMD ["python", "ADFSpoof.py"]