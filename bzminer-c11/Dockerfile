FROM nvidia/cuda:11.8.0-base-ubuntu20.04

# Set non-interactive mode
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /root


# Install necessary tools and clean up
RUN apt update && \
    apt -y install wget jq curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 

ENV ALGO=
ENV WALLET_ADDRESS=
ENV POOL=
ENV PASSWORD=x
ENV OPTIONS="--http_enabled 1 --http_address 0.0.0.0 --http_port 4067"

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT /entrypoint.sh
