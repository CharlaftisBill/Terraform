FROM mcr.microsoft.com/devcontainers/base:debian-12

# Install dependencies and Azure CLI
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends curl gnupg lsb-release

# Install Azure CLI natively
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install Terraform (HashiCorp official repository supports multi-arch including ARM64)
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list \
    && apt-get update && apt-get install -y terraform

# Clean up apt cache to keep container size small
RUN apt-get clean && rm -rf /var/lib/apt/lists/*