# 🚀 Automated Windows Environment Provisioner

Unleash the power of automated Windows environment provisioning! This project is a robust, container-native solution for effortlessly spinning up pre-configured Windows operating systems, from client editions like Windows 7 to the latest server releases, all driven by a powerful, script-based automation engine. Say goodbye to manual installations and hello to reproducible, on-demand Windows environments.

## Short Description
This project provides a comprehensive framework for automating the installation and configuration of a wide range of Windows operating systems within containerized or virtualized environments. Leveraging Docker, Kubernetes, and specialized XML unattended installation files, it enables developers, testers, and IT professionals to quickly deploy custom Windows instances tailored to specific needs, dramatically accelerating development, testing, and deployment workflows.

## ✨ Key Features
*   **Broad Windows OS Support:** Provision Windows Vista, 7, 8.1, 10, 11, and Server editions from 2008 R2 up to 2025.
*   **Container-Native Workflows:** Built with Docker and Docker Compose for seamless environment packaging and deployment.
*   **Kubernetes Ready:** Deploy Windows environments at scale using provided Kubernetes configurations.
*   **Automated Unattended Installations:** Utilizes `AutoUnattend.xml`-like configuration files to streamline the OS setup process.
*   **Extensive Customization:** Easily adapt and extend provisioning logic using a suite of shell scripts for intricate setups (e.g., Samba, power management).
*   **CI/CD Integration:** Ready for automated builds, checks, and deployments via GitHub Actions workflows.
*   **Enhanced Developer Experience:** Includes Dev Container support for a consistent, isolated development environment.
*   **Dependency Security:** Integrates Dependabot and Renovate for proactive dependency management and security updates.

## Who is this for?
*   **Developers:** Quickly set up consistent Windows development or testing environments.
*   **QA Engineers:** Automate the creation of test beds for various Windows versions and configurations.
*   **DevOps Engineers:** Standardize the deployment of Windows-based services and applications in containerized infrastructures.
*   **IT Professionals:** Generate specialized Windows images for specific use cases or virtual desktop infrastructure.
*   **Security Researchers:** Rapidly deploy sandboxed Windows instances for analysis.

## Technology Stack & Architecture
*   **Core Automation:** Shell Scripting (`src/*.sh`)
*   **Configuration:** XML-based Unattended Setup (`assets/*.xml`)
*   **Containerization:** Docker (`Dockerfile`, `compose.yml`)
*   **Orchestration:** Kubernetes (`kubernetes.yml`)
*   **Development Environment:** Dev Containers (`.devcontainer.json`)
*   **CI/CD & Automation:** GitHub Actions (`.github/workflows/`)
*   **Dependency Management:** Dependabot, Renovate

## 📊 Architecture & Database Schema
This project's architecture focuses on a robust provisioning pipeline rather than a traditional database schema. The core flow orchestrates the build, configuration, and deployment of Windows environments.

```mermaid
graph TD
    A[Developer/User Request] --> B(Initiate Docker Build/Run);
    B --> C[Dockerfile Executes Base Image Setup];
    C --> D{Select Windows Version & Edition};
    D --> E[Load Corresponding Unattend XML (assets/*.xml)];
    E --> F[Execute src/define.sh: OS Configuration];
    F --> G[Execute src/install.sh: Feature Installation];
    G --> H[Execute src/samba.sh: Network Sharing Setup];
    H --> I[Execute src/entry.sh: Startup Services & Tasks];
    I --> J(Provisioned & Configured Windows Environment);
    J --> K[Ready for Use/Deployment];
```

## ⚡ Quick Start Guide
To get started, ensure you have Docker installed on your system.

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/windows.git
    cd windows
    ```
2.  **Build the Docker Image:**
    This command builds the base image that will orchestrate your Windows provisioning.
    ```bash
    docker build -t automated-windows-provisioner .
    ```
3.  **Run with Docker Compose (Example: Windows 10 x64):**
    Modify `compose.yml` or create a new one to specify the desired XML configuration file from the `assets/` directory. For instance, to provision `win10x64.xml`:
    ```yaml
    # Example compose.yml snippet
    version: '3.8'
    services:
      windows-vm:
        image: automated-windows-provisioner
        environment:
          - WINDOWS_CONFIG_FILE=/app/assets/win10x64.xml # Adjust as needed
        # Add necessary volume mounts or network configurations for your VM/container setup
    ```
    Then, execute:
    ```bash
    docker compose up
    ```
    The provisioning process will begin, creating your customized Windows environment. Refer to the `src/` directory for detailed scripting logic and the `assets/` directory for available Windows configurations.

## 📜 License
This project is licensed under the **MIT License**. See `license.md` for full details.
