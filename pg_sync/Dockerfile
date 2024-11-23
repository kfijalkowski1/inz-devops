FROM python:3.11-slim

WORKDIR /app

# RUN apt-get update && apt-get install -y \
#     build-essential \
#     && rm -rf /var/lib/apt/lists/*

# Install pg-sync
RUN pip install pgsync

# Copy schema.json and .env to the working directory
COPY schema.json /app/schema.json
COPY .env /app/.env

CMD ["bootstrap", "--config", "/app/schema.json"]
CMD ["pgsync", "--config", "/app/schema.json", "--daemon"]
