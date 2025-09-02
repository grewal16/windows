# 🚀 Windows Automated Provisioning Toolkit

## Short Description
Unleash the power of automated Windows environment provisioning! This robust toolkit provides a streamlined, containerized, and orchestrator-ready solution for building and deploying customized Windows operating systems and server instances across a vast spectrum of versions – from the classic Windows Vista to the cutting-edge Windows 11, and server editions from 2008 R2 up to 2025. Leveraging a meticulous collection of unattended setup configuration files and intelligent shell scripting, this project empowers developers, DevOps engineers, and system administrators to effortlessly spin up consistent, tailor-made Windows environments at scale.

## ✨ Key Features
*   **Comprehensive Windows OS Support:** Provision a wide array of Windows desktop (Vista, 7, 8.1, 10, 11) and server (2008 R2, 2012 R2, 2016, 2019, 2022, 2025) editions, including evaluation, enterprise, and IoT variants.
*   **Automated Unattended Setup:** Utilizes carefully crafted XML answer files (`assets/*.xml`) to automate the entire Windows installation and configuration process, eliminating manual intervention.
*   **Containerized Build Environment:** A `Dockerfile` and `.devcontainer.json` ensure a consistent, reproducible environment for building and executing provisioning tasks, isolating dependencies and streamlining development.
*   **Orchestration Ready:** Seamlessly integrates with modern infrastructure-as-code practices through `compose.yml` for Docker Compose and `kubernetes.yml` for Kubernetes deployments, enabling scalable and resilient management of Windows instances.
*   **Robust CI/CD Pipelines:** Features comprehensive GitHub Actions workflows (`.github/workflows/`) for automated `build`, `check`, and `test` processes, ensuring code quality and deployment readiness.
*   **Intelligent Shell Scripting:** A collection of `src/*.sh` scripts (`define.sh`, `install.sh`, `entry.sh`, `samba.sh`, `power.sh`, `mido.sh`) orchestrate the provisioning logic, providing flexibility and extensibility.
*   **Dependency Management:** Automated dependency updates are managed via `dependabot.yml` and `renovate.json`, keeping the project secure and up-to-date.

## Who is this for?
*   **DevOps Engineers:** Automate the creation of test and production Windows VMs/containers for CI/CD pipelines.
*   **System Administrators:** Streamline enterprise-wide Windows deployments and standardize system configurations.
*   **Virtualization Specialists:** Quickly provision new Windows virtual machines with predefined settings.
*   **Software Developers:** Set up consistent, isolated Windows development and testing environments.
*   **IT Professionals:** Anyone looking to reduce manual effort and human error in Windows installation and configuration tasks.

## Technology Stack & Architecture
*   **Orchestration:** Docker, Docker Compose, Kubernetes
*   **Automation/Scripting:** Bash Shell Scripting (`src/*.sh`)
*   **Configuration:** XML for Windows Unattended Installation (`assets/*.xml`)
*   **Containerization:** Dockerfile, DevContainer
*   **CI/CD:** GitHub Actions
*   **Dependency Management:** Dependabot, Renovate

## 📊 Architecture & Database Schema
This project's core is a process automation pipeline, not a traditional database. The following flowchart illustrates the typical workflow for provisioning a Windows environment using this toolkit.

```mermaid
graph TD
    A["Developer/CI Trigger"] --> B{"Initialize\nContainerized Build Env"};
    B --> C["`Dockerfile` & `.devcontainer`"];
    C --> D{"Execute Provisioning Scripts\n(`src/*.sh`)"];
    D --> E["Select Windows OS/Edition\n(`assets/*.xml` config files)"];
    E --> F{"Apply Unattended\nInstallation & Customization"};
    F --> G["Provisioned Windows\nInstance/VM"];
    G -- "Deploy to" --> H["Docker Compose\n(Local/Dev)"];
    G -- "Deploy to" --> I["Kubernetes\n(Staging/Prod)"];
    A -- "Automated by" --> J["CI/CD Workflows\n(`.github/workflows`)"];
    J --> B;
```

## ⚡ Quick Start Guide
Getting started with this project is straightforward. Here's a high-level overview:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/windows.git
    cd windows
    ```

2.  **Build the Docker Image (Provisioning Environment):**
    ```bash
    docker build -t windows-provisioner .
    ```

3.  **Run a Provisioning Script (Conceptual):**
    While specific usage depends on your target environment (VM, cloud), the general idea is to mount your target directory and run one of the `src/*.sh` scripts, referencing an `assets/*.xml` file.
    ```bash
    # Example: Run a script to generate/apply a Windows 11 configuration
    docker run -v /path/to/your/output:/output windows-provisioner /src/install.sh --template assets/win11x64.xml --output /output/autounattend.xml
    ```
    *Refer to the individual `src/*.sh` scripts for detailed command-line arguments and capabilities.*

## 📜 License
This project is distributed under the MIT License. A copy of the license can be found in the `license.md` file in the root of the repository.
