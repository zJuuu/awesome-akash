FROM nvidia/cuda:11.8.0-base-ubuntu20.04

# Set non-interactive mode
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /root


# Install necessary tools and clean up
RUN apt update && \
    apt -y install wget jq curl xz-utils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 

ENV ALGO=
ENV WALLET_ADDRESS=
ENV POOL=
ENV PASSWORD=x
ENV OPTIONS="--api 0.0.0.0:4067 --nvml 0"

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT /entrypoint.sh
