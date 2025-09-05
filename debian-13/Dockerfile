# Debian 13 (Trixie) with CI/CD tools for GitHub Actions
FROM debian:13-slim

LABEL org.opencontainers.image.source="https://github.com/a2b-technology-corporation/debian-ci-containers"
LABEL org.opencontainers.image.description="Debian 13 with CI/CD tools for GitHub Actions"
LABEL maintainer="A2B Technology Corporation"

# Prevent interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update and install packages in one layer to reduce image size
RUN apt-get update && apt-get install -y --no-install-recommends \
    # Version control
    git \
    # Network tools
    curl \
    wget \
    ca-certificates \
    openssh-client \
    # Build essentials
    make \
    gcc \
    g++ \
    # Python and Ansible
    python3 \
    python3-pip \
    python3-venv \
    ansible \
    ansible-lint \
    # Node.js
    nodejs \
    npm \
    # Utilities
    jq \
    unzip \
    zip \
    tar \
    gzip \
    bzip2 \
    xz-utils \
    # Process management
    procps \
    # Text processing
    sed \
    gawk \
    grep \
    # Editor (for potential debugging)
    vim-tiny \
    # YAML processor
    yq \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install GitHub CLI using official method
RUN mkdir -p -m 755 /etc/apt/keyrings \
    && wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
    && chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt-get update \
    && apt-get install -y gh \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set up Git safe directory for GitHub Actions
RUN git config --global --add safe.directory '*'

# Create non-root user for better security (optional, GitHub Actions overrides this)
RUN useradd -m -s /bin/bash runner

# Set working directory
WORKDIR /github/workspace

# Default to bash
SHELL ["/bin/bash", "-c"]
CMD ["/bin/bash"]