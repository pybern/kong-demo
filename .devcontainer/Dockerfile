# Use Ubuntu 22.04 as the base image
FROM ubuntu:22.04

# Install dependencies and Kong
RUN apt-get update && \
    apt-get install -y apt-transport-https curl lsb-release && \
    curl -fsSL https://download.konghq.com/gateway-3.x-ubuntu-$(lsb_release -sc)/all.asc | gpg --dearmor -o /usr/share/keyrings/kong.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/kong.gpg] https://download.konghq.com/gateway-3.x-ubuntu-$(lsb_release -sc)/ default all" | tee /etc/apt/sources.list.d/kong.list && \
    apt-get update && \
    apt-get install -y kong

# Create Kong directory and copy configurations
RUN mkdir -p /etc/kong
COPY kong.conf /etc/kong/kong.conf
COPY kong.yml /etc/kong/kong.yml

# Start Kong in the foreground
CMD ["kong", "start", "-c", "/etc/kong/kong.conf"]
