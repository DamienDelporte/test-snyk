FROM debian:bullseye
ARG NODE_SHA256=c3fd89a768e40a2fd8008919100bd283e6e9aec742eddeb1d494eb2a626466dc
SHELL ["/bin/bash", "-euo", "pipefail", "-c"]

RUN apt-get update \
  && apt-get install --no-install-recommends -y curl ca-certificates \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir /app
WORKDIR /app
RUN NODE_VERSION="16.2.0" \
  && curl -s -f -o /node.tar.gz -q "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz" \
  && echo "${NODE_SHA256} /node.tar.gz" | sha256sum -c - \
  && cd /usr/local/ \
  && tar xzf /node.tar.gz \
  && mv "node-v${NODE_VERSION}-linux-x64" node
ENV PATH="/usr/local/node/bin:${PATH}"
RUN npm install https-proxy-agent@5.0.0