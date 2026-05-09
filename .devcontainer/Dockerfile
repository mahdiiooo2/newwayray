FROM debian:bookworm-slim

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    bash git curl wget unzip tzdata openssl ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Copy scripts and static config
COPY install.sh ./install.sh
COPY start.sh   ./start.sh
COPY config.json /etc/config.json

# Make scripts executable and install xray
RUN chmod +x ./install.sh ./start.sh && ./install.sh

# start.sh rewrites /etc/config.json at runtime with random UUIDs
# and the real CODESPACE_NAME hostname, then launches xray
CMD ["/app/start.sh"]
