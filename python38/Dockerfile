# Start from the latest version of the Azure DevOps agent image
FROM 704909879244.dkr.ecr.eu-west-1.amazonaws.com/azure-devops-agent-generic:0.0.1

# Install Python 3.8 and the necessary dependencies
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        software-properties-common python3.8 python3.8-venv && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Add custom capability
ENV AGENT_CAPABILITY=python38

# Create a virtual environment and activate it
RUN python3.8 -m venv /venv
ENV PATH=/venv/bin:$PATH