# Use the Jenkins LTS image (Trixie-based)
FROM jenkins/jenkins:lts

USER root

# Prevent interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install prerequisites and Docker
RUN apt-get update -y && \
    apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release && \
    # Add Docker GPG key
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    # ✅ Use bookworm instead of trixie
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
    https://download.docker.com/linux/debian bookworm stable" > /etc/apt/sources.list.d/docker.list && \
    apt-get update -y && \
    apt-get install -y docker-ce docker-ce-cli containerd.io && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Add Jenkins user to Docker group
RUN groupadd -f docker && usermod -aG docker jenkins

# Docker volume for DinD
RUN mkdir -p /var/lib/docker
VOLUME /var/lib/docker

USER jenkins