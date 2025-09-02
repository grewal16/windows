# 🚀 Automated Windows Deployment & Configuration

Unleash the power of streamlined Windows environment provisioning with `windows`! This project provides a robust, containerized, and fully automated solution for deploying and configuring a wide array of Microsoft Windows operating systems, from client editions like Windows 7, 8.1, 10, and 11, to server variants up to Windows Server 2025. Say goodbye to manual installations and embrace infrastructure as code for your Windows environments.

Leveraging unattended XML answer files (`Unattend.xml`) and powerful shell scripting, this repository simplifies the creation of consistent, customized Windows setups for development, testing, or production scenarios.

## Short Description
`windows` is a container-first project that automates the unattended installation and configuration of various Windows operating systems using pre-defined XML answer files and shell scripts, encapsulated within Docker for portability and consistency.

## ✨ Key Features
*   **Broad OS Support**: Provision Windows client OS (7, 8.1, 10, 11) and server OS (2008R2, 2012R2, 2016, 2019, 2022, 2025) across various editions (Enterprise, IoT, LTSC, Evaluation).
*   **Unattended XML Configuration**: Utilizes industry-standard XML answer files for hands-off operating system setup and customization.
*   **Containerized Workflow**: Built with Docker for reproducible and isolated provisioning environments, ensuring consistent results every time.
*   **Orchestration Ready**: Includes `compose.yml` for multi-container setups and `kubernetes.yml` for scalable deployments in cloud-native environments.
*   **Robust CI/CD Pipeline**: Integrated with GitHub Actions (`build.yml`, `check.yml`, `hub.yml`, `test.yml`) for automated builds, testing, and deployment.
*   **Developer-Friendly**: Features `.devcontainer.json` for a consistent and quick development environment setup using VS Code Dev Containers.
*   **Automated Dependency Management**: Leverages Dependabot and Renovate for keeping project dependencies up-to-date and secure.
*   **Community-Oriented**: Comprehensive issue templates (`1-issue.yml`, `2-feature.yml`, `3-bug.yml`, `4-question.yml`) encourage structured contributions and feedback.

## Who is this for?
*   **DevOps Engineers**: Automate Windows VM or container provisioning as part of your CI/CD pipelines.
*   **System Administrators**: Rapidly deploy and configure standardized Windows server or client images.
*   **Developers**: Quickly spin up consistent Windows development or testing environments.
*   **QA Engineers**: Ensure reproducible test beds for Windows applications.
*   **Educators & Trainers**: Provide pre-configured Windows labs for students.

## Technology Stack & Architecture
This project is engineered with a focus on automation, portability, and infrastructure as code principles.
*   **Containerization**: Docker
*   **Orchestration**: Docker Compose, Kubernetes
*   **Automation/Scripting**: Shell Scripts (`bash`)
*   **Configuration**: XML Unattended Answer Files (`Unattend.xml`)
*   **CI/CD**: GitHub Actions
*   **Development Environment**: VS Code Dev Containers

## 📊 Architecture & Database Schema

The core architecture revolves around a containerized process that consumes pre-defined Windows XML answer files and executes shell scripts to automate the installation and initial configuration of a target Windows environment.

```mermaid
graph TD
    subgraph CI/CD (GitHub Actions)
        A[Push/PR Trigger] --> B(Check: Linting, Format)
        B --> C(Test: Script Validation)
        C --> D(Build: Docker Image)
        D --> E(Deploy: Push to Container Registry)
    end

    subgraph Provisioning Workflow (Docker Container)
        F[Docker Run / Compose / Kubernetes] --> G(Container Entrypoint: entry.sh)
        G --> H{Select Windows Version/Edition}
        H --> I(Load assets/*.xml)
        I --> J(Execute src/*.sh scripts: install.sh, define.sh, samba.sh, power.sh, etc.)
        J --> K[Automated Windows Installation/Configuration]
    end

    subgraph Development Environment
        L[VS Code Dev Container] --> M(Consistent development setup)
    end

    A --> F
    M --> J
```

## ⚡ Quick Start Guide

To get started, you'll need Docker installed on your system.

1.  **Clone the Repository**:
    ```bash
    git clone https://github.com/grewal16/windows.git
    cd windows
    ```

2.  **Build the Docker Image**:
    This will create an image that contains all the necessary scripts and a framework to process your Windows unattended XML files.
    ```bash
    docker build -t automated-windows-provisioning .
    ```

3.  **Run a Windows Provisioning Task (Example)**:
    To provision a Windows environment, you would typically mount the target Windows ISO and select one of the XML answer files from the `assets` directory. For demonstration, let's assume you have a `windows_iso.iso` at `/path/to/your/iso`.

    ```bash
    docker run -it --rm \
      -v /path/to/your/iso:/mnt/iso \
      -v "$(pwd)/assets/win11x64.xml:/mnt/unattend.xml" \
      automated-windows-provisioning
    ```
    *Note: The actual interaction with a Windows ISO and hypervisor might require more advanced setup (e.g., using `libvirt`, `qemu`, or specific cloud provider tools) which this Docker image would orchestrate. The `src` scripts are designed to work in such environments.*

4.  **Using Docker Compose (for a more complex setup)**:
    If `compose.yml` defines specific services, you can spin them up with:
    ```bash
    docker compose up -d
    ```

## 📜 License
This project is licensed under the MIT License. Refer to `license.md` for full details.
