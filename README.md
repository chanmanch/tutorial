
```markdown
# ICN Docker Setup Guide

This guide provides step-by-step instructions to set up the ICN software in a separate Docker container within a GitHub Codespace, ensuring that existing containers remain unaffected.

## Prerequisites

- A GitHub Codespace environment with Docker installed and running.
- Access to ICN installation permissions.

## Setup Instructions

### Step 1: Create a Dockerfile for the ICN Setup

1. **Navigate to your project directory** in the Codespace terminal.

2. **Create a new folder** named `icn-docker`:

   ```bash
   mkdir icn-docker
   cd icn-docker
   ```

3. Inside `icn-docker`, create a **Dockerfile** with the following content:

   ```Dockerfile
   # Use a base image with an updated GLIBC version
   FROM ubuntu:latest

   # Update and install necessary packages
   RUN apt-get update && \
       apt-get install -y curl bash

   # Set a working directory (optional)
   WORKDIR /app

   # Run the ICN installation command
   CMD ["bash", "-c", "curl -o- https://console.icn.global/downloads/install/start.sh | bash -s -- -p aa95f"]
   ```

4. **Save the Dockerfile** in the `icn-docker` folder.

### Step 2: Build and Run the ICN Installer Container

1. **Navigate to the `icn-docker` directory** (if not already there):

   ```bash
   cd icn-docker
   ```

2. **Build the Docker image** with a unique name, like `icn_installer`:

   ```bash
   docker build -t icn_installer .
   ```

3. **Run the ICN installer container**:

   ```bash
   docker run --name icn_container icn_installer
   ```

   This command will create and run a separate Docker container for the ICN setup, ensuring your existing containers remain unaffected.

### Step 3: Verify the Installation

1. **Check the container logs** to verify the ICN software setup:

   ```bash
   docker logs icn_container
   ```

2. **Re-run the installation** if needed by removing the existing container and starting it again:

   ```bash
   docker rm icn_container
   docker run --name icn_container icn_installer
   ```

---

## Troubleshooting

- **Container Logs**: If issues arise during the setup, use `docker logs icn_container` to review the log output for more details.
- **Memory Management**: If the container experiences memory limitations, consider adjusting Docker's resource allocations or optimizing memory usage for other containers.

---

This setup allows you to install and run ICN within a separate Docker container without disrupting your existing environment. Feel free to reach out for further support if needed.
```

This `README.md` is now formatted for easy readability on GitHub, with clear code blocks and step-by-step instructions. Let me know if you’d like any adjustments!
