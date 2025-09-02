# 🚀 Automated Windows Provisioning Framework

## Short Description
Dive into the world of effortless Windows environment management! This project delivers a robust, automated framework for building, configuring, and deploying a vast array of Windows operating systems—from classic desktops like Windows 7 and 10 to modern Windows 11 and server editions up to 2025. Leveraging unattended installation XML files, sophisticated shell scripting, and containerization, it provides a consistent, reproducible, and highly efficient way to provision customized Windows instances for development, testing, or production.

## ✨ Key Features
*   **Extensive OS Compatibility:** Support for a wide range of Windows client (7, 8.1, 10, 11) and server (2008 R2, 2012 R2, 2016, 2019, 2022, 2025) editions, including various SKUs like Enterprise, IoT, LTSC, and evaluation versions.
*   **Automated Unattended Installations:** Utilizes pre-configured XML answer files to streamline the OS installation process, minimizing manual intervention.
*   **Containerized Build Environment:** Develop and build your Windows images in a consistent, isolated environment using Docker and VS Code Dev Containers.
*   **Powerful Scripting for Customization:** A collection of `bash` scripts (`define.sh`, `install.sh`, `samba.sh`, `power.sh`, `entry.sh`) provides granular control over the provisioning lifecycle, from OS definition to post-installation setup.
*   **Network Integration Ready:** Includes `samba.sh` for easy configuration of network sharing, facilitating seamless integration into existing infrastructure.
*   **CI/CD Pipeline Integration:** Built-in GitHub Actions workflows (`build.yml`, `check.yml`, `test.yml`, `hub.yml`) ensure continuous integration, validation, and deployment readiness.
*   **Dependency Management:** Automated dependency updates via Dependabot and Renovate keep the project secure and up-to-date.
*   **Kubernetes-Ready Configuration:** `kubernetes.yml` hints at advanced orchestration capabilities, potentially for managing Windows containers or nodes within a Kubernetes cluster.

## Who is this for?
*   **DevOps Engineers:** Seeking reproducible Windows build pipelines.
*   **System Administrators:** Automating the deployment and configuration of Windows servers and desktops.
*   **Developers:** Requiring consistent, isolated Windows testing environments.
*   **IT Professionals:** Standardizing Windows image creation and provisioning.
*   **Security Researchers:** Building disposable Windows environments for analysis.

## Technology Stack & Architecture
*   **Operating Systems:** Windows (client & server, multiple versions/editions)
*   **Automation:** Bash Shell Scripting (`src/*.sh`), XML Unattended Setup Files (`assets/*.xml`)
*   **Containerization:** Docker (`Dockerfile`, `compose.yml`), VS Code Dev Containers (`.devcontainer.json`)
*   **Orchestration:** Docker Compose, Kubernetes (`kubernetes.yml`)
*   **Continuous Integration/Deployment:** GitHub Actions (`.github/workflows`)
*   **Dependency Management:** Dependabot, Renovate

## 📊 Architecture & Database Schema
This project doesn't utilize a traditional database schema. Instead, its architecture is centered around a robust provisioning workflow designed to automate the deployment and configuration of Windows operating systems. The diagram below illustrates the core process:

```mermaid
graph TD
    A[Trigger Build/Provisioning] --> B{Select Windows OS & Edition};
    B --> C["Reference Assets " (e.g., "win10x64.xml")];
    C --> D{Prepare Environment "(.devcontainer.json / Dockerfile)"};
    D --> E["Execute Entrypoint " (src/entry.sh)];
    E --> F["Define OS Parameters " (src/define.sh)];
    F --> G["Automated OS Installation " (src/install.sh)];
    G --> H{"Post-Installation Setup"};
    H --> I["Configure Network Sharing " (src/samba.sh)];
    H --> J["Manage Power States " (src/power.sh)];
    I --> K[Customized Windows Environment];
    J --> K;
    K --> L{"Optional: Orchestrate Deployment"};
    L --> M["Deploy with Docker Compose " (compose.yml)];
    L --> N["Deploy with Kubernetes " (kubernetes.yml)];
    M --> O[Ready Windows VM / Container];
    N --> O;

    subgraph CI/CD Pipeline
        P["GitHub Workflows " (.github/workflows)] --> D;
        P -.-> A;
    end
```

## ⚡ Quick Start Guide
Getting started with the Automated Windows Provisioning Framework is straightforward:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/windows.git
    cd windows
    ```

2.  **Prepare Your Environment:**
    *   **Using VS Code Dev Containers:** If you have Docker and VS Code with the Dev Containers extension installed, simply open the project in a development container. VS Code will prompt you to reopen in a container.
    *   **Using Docker Compose:**
        ```bash
        docker compose up -d
        ```
        This will spin up the containerized environment defined in `compose.yml`.

3.  **Initiate a Windows Build:**
    The core logic resides within the `src/` directory. You will typically interact with the `src/entry.sh` script, which orchestrates the calls to other scripts like `define.sh` and `install.sh`. Consult the scripts directly to understand available parameters and options for selecting your desired Windows OS and configuration.

    Example (conceptional, specific commands may vary based on `entry.sh` logic):
    ```bash
    # After entering the dev container or connecting to the Docker container
    ./src/entry.sh --os-version "win10x64" --edition "enterprise-eval"
    ```
    *Refer to the individual `src/*.sh` scripts for precise usage details and available commands.*

## 📜 License
This project is released under an open-source license. Please see the `license.md` file in the repository root for full details.
