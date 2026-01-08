FROM node:22-bookworm-slim

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    bash \
    ca-certificates \
    git \
    jq \
    ripgrep \
    curl \
    nano \
    python3 \
    python3-pip \
    make \
    g++ \
    openssh-server \
  && rm -rf /var/lib/apt/lists/*

ENV PNPM_HOME=/pnpm
ENV PATH="${PNPM_HOME}:${PATH}"

RUN npm install -g pnpm@9.12.3 \
  && mkdir -p /pnpm \
  && pnpm config set global-bin-dir /pnpm \
  && pnpm add -g clawdhub

RUN pip3 install --no-cache-dir --break-system-packages homeassistant-cli

# Install gog CLI (Google Workspace: Gmail, Calendar, Drive, Contacts, Sheets, Docs)
ARG GOG_VERSION=0.4.2
ARG TARGETARCH
RUN ARCH=$(echo ${TARGETARCH:-$(uname -m)} | sed 's/aarch64/arm64/;s/x86_64/amd64/') \
  && curl -fsSL "https://github.com/steipete/gogcli/releases/download/v${GOG_VERSION}/gogcli_${GOG_VERSION}_linux_${ARCH}.tar.gz" \
     | tar xz -C /usr/local/bin gog \
  && chmod +x /usr/local/bin/gog

WORKDIR /opt/clawdbot

COPY run.sh /run.sh
RUN chmod +x /run.sh

CMD [ "/run.sh" ]
