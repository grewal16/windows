# 🚀 Automated Windows Environments & Containerization

Welcome to a powerful toolkit designed for seamlessly provisioning, configuring, and deploying a vast array of Windows environments. This project liberates developers and system administrators from manual setup headaches, offering a fully automated, containerized approach to managing Windows instances, from classic Vista to the latest Windows 11 and Server 2025 editions. Leverage modern DevOps practices to achieve consistent, repeatable, and scalable Windows deployments.

## Short Description
This repository provides a comprehensive solution for creating automated, containerized Windows environments. Utilizing Docker and Kubernetes, it enables rapid deployment of pre-configured Windows versions (client and server), powered by extensive XML configuration assets and robust shell scripting for ultimate customization and consistency.

## ✨ Key Features
*   **Extensive Windows Support:** Deploy virtually any Windows version, including client editions (Vista, 7, 8.1, 10, 11) and server editions (2008 R2, 2012 R2, 2016, 2019, 2022, 2025) across various editions (Enterprise, Evaluation, IoT, LTSC, Ultimate, Hyper-V).
*   **Containerized Workflows:** Utilize `Dockerfile` for building consistent Windows images, ready for deployment with Docker or container orchestration platforms.
*   **Orchestration Ready:** Deploy with ease using `compose.yml` for local development or scale with `kubernetes.yml` for production-grade environments.
*   **Declarative Configuration:** Leverages a rich set of XML assets (`assets/*.xml`) to define precise, unattended installation and configuration settings for each Windows variant.
*   **Powerful Automation Scripts:** A suite of shell scripts (`src/*.sh`) streamlines tasks such as environment definition, entrypoint execution, installation routines, power management, and SMB (Samba) share configuration.
*   **Developer Experience Focused:** Includes `.devcontainer.json` for immediate, consistent development environments in VS Code.
*   **Robust CI/CD & Dependency Management:** Integrated GitHub Actions workflows (`.github/workflows/*.yml`), Dependabot, and Renovate ensure code quality, automated testing, and up-to-date dependencies.

## Who is this for?
*   **DevOps Engineers:** Automate the provisioning of Windows test and deployment environments.
*   **System Administrators:** Rapidly deploy and manage consistent Windows server instances.
*   **Software Developers:** Obtain quick, reproducible Windows development and testing environments.
*   **QA & Testers:** Standardize testbeds across different Windows operating systems.
*   **IT Educators & Trainers:** Provide pre-configured Windows labs for students.

## Technology Stack & Architecture
*   **Containerization:** Docker
*   **Orchestration:** Docker Compose, Kubernetes
*   **Automation:** Bash Shell Scripting (`src/*.sh`)
*   **Configuration:** XML Configuration Files (`assets/*.xml`)
*   **CI/CD:** GitHub Actions
*   **Dependency Management:** Dependabot, Renovate
*   **Development Environment:** VS Code Dev Containers

## 📊 Architecture & Database Schema
This project's architecture focuses on an automated pipeline for generating and deploying highly configurable Windows environments. There is no traditional database schema, but rather a process flow for building and managing containerized Windows instances.

```mermaid
graph TD
    A[Start: User/CI Trigger] --> B{Choose Windows Version & Edition};
    B --> C[Select assets/*.xml Config];
    C --> D[Combine with src/*.sh Scripts];
    D --> E[Build Docker Image using Dockerfile];
    E --> F{Deployment Target?};
    F -- Local Dev/Test --> G[Run with Docker Compose (compose.yml)];
    F -- Scalable/Production --> H[Deploy to Kubernetes (kubernetes.yml)];
    G --> I[Running Windows Container];
    H --> I;
    I --> J[Access & Interact];
```

## ⚡ Quick Start Guide
To get started with building and running your first automated Windows environment:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/windows.git
    cd windows
    ```

2.  **Build a Windows Docker Image:**
    The `Dockerfile` in this repository can be used to build your custom Windows container image. You'll typically need to provide an ISO or similar Windows installation media, which will be referenced by the `assets/*.xml` files.
    *(Note: Specific build commands depend on how the Dockerfile is designed to consume the XML assets and Windows media. Assuming the Dockerfile is set up to utilize the scripts and assets within the context.)*

    ```bash
    # Example: Build a generic Windows container.
    # The actual Dockerfile might require specific build arguments for different Windows versions.
    docker build -t my-windows-env .
    ```

3.  **Run with Docker Compose (Local Development):**
    If `compose.yml` is configured for a specific Windows environment, you can launch it easily:

    ```bash
    docker compose up -d
    ```

4.  **Deploy to Kubernetes (Advanced):**
    For orchestrating deployments, use the provided `kubernetes.yml` file:

    ```bash
    kubectl apply -f kubernetes.yml
    ```
    Ensure your Kubernetes cluster is configured to run Windows containers if you're deploying actual Windows OS containers.

## 📜 License
This project is released under a Standard Open Source License. For full details, please refer to the `license.md` file in the repository root.
