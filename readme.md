# 🚀 Windows OS Automation Framework

Unleash the power of fully automated Windows operating system provisioning! This robust framework provides a streamlined, containerized approach to deploying a vast array of Windows client and server editions, from legacy systems to the latest releases, all through unattended configuration. Say goodbye to manual installations and hello to reproducible, efficient, and scalable Windows environment setups.

## Short Description

This project offers a comprehensive, Docker-centric solution for automating the deployment of diverse Windows operating systems. Leveraging an extensive library of unattended XML configuration files and intelligent shell scripting, it transforms the traditionally complex task of Windows installation into a simple, repeatable container operation.

## ✨ Key Features

*   **Broad OS Support:** Deploy a wide spectrum of Windows versions, including Windows 7, 8.1, 10, 11, and Server editions (2008 R2 to 2025), encompassing various editions (Enterprise, IoT, LTSC, etc.) and architectures (x64, x86).
*   **Containerized Deployments:** Built on Docker, ensuring consistent and isolated deployment environments. Seamlessly integrate with Docker Compose and Kubernetes for scalable orchestration.
*   **Unattended Installation:** Utilize a rich collection of `.xml` assets to perform fully automated, hands-off Windows installations, eliminating manual intervention.
*   **Robust Automation Scripts:** Powerful shell scripts (`entry.sh`, `install.sh`, `define.sh`, `samba.sh`) orchestrate the entire provisioning process, including initial setup and network configuration.
*   **CI/CD Ready:** Integrate effortlessly with GitHub Actions for automated builds, testing, and continuous deployment workflows, ensuring project integrity and up-to-date images.
*   **Developer-Friendly:** Includes `.devcontainer.json` for a consistent, pre-configured development environment, accelerating contributor onboarding.
*   **Community-Driven:** Comprehensive issue templates (`1-issue.yml`, `2-feature.yml`, `3-bug.yml`, `4-question.yml`) foster clear communication and collaborative development.

## Who is this for?

*   **DevOps Engineers:** Automate the provisioning of Windows VMs for CI/CD pipelines, testing, and development environments.
*   **System Administrators:** Streamline the deployment of new Windows servers and workstations across your infrastructure.
*   **IT Professionals:** Create reproducible and standardized Windows images for consistent organizational rollouts.
*   **Developers:** Quickly spin up isolated Windows environments for cross-platform application testing or development.
*   **Researchers/Educators:** Provision specific Windows versions rapidly for experimental setups or classroom environments.

## Technology Stack & Architecture

This project is engineered for maximum flexibility and automation:

*   **Containerization:** Docker, Docker Compose, Kubernetes
*   **Scripting:** Bash (for core automation logic)
*   **Configuration:** Unattended Windows XML Answer Files (`.xml`)
*   **CI/CD:** GitHub Actions (for automated build, test, and deployment)
*   **Development:** Dev Containers

## 📊 Architecture & Database Schema

This project's architecture revolves around a dynamic, script-driven containerized deployment pipeline, rather than a traditional database schema. The core flow involves leveraging Docker to encapsulate the Windows installation logic and a vast library of unattended XML configuration files.

```mermaid
graph TD
    A[User/CI System] --> B(Clone Repository);
    B --> C{Select Windows Version/Edition: <br/> `assets/*.xml`};
    C --> D(Dockerfile & <br/> `src/*.sh` scripts);
    D --> E[Build Docker Image];
    E --> F[Run Container <br/> (e.g., `docker run`, `docker-compose up`, `kubectl apply`)]
    F --> G[Automated Unattended Installation of Windows OS];
    G --> H[Ready-to-Use Windows VM/Container];

    subgraph Automation & Maintenance
        I[GitHub Actions Workflows] --> J[Automated Build];
        J --> K[Automated Testing];
        K --> L[Docker Hub/Registry Push];
        L --> E;
    end
    I --> D;
    I --> F;
```

## ⚡ Quick Start Guide

To get started with automating your Windows deployments:

1.  **Prerequisites:** Ensure you have [Docker](https://docs.docker.com/get-docker/) installed. For orchestrating multiple containers, [Docker Compose](https://docs.docker.com/compose/install/) is recommended. For Kubernetes, `kubectl` and a cluster are needed.

2.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/windows.git
    cd windows
    ```

3.  **Build Your Docker Image:**
    This command builds the base image containing the necessary scripts and assets.
    ```bash
    docker build -t windows-auto-deploy .
    ```

4.  **Initiate a Windows Deployment:**
    Choose an XML asset from the `assets/` directory (e.g., `win10x64.xml`) and run the container, passing the desired XML file as an argument. The `entry.sh` script handles the rest.

    ```bash
    docker run --privileged -v /var/run/libvirt/libvirt-sock:/var/run/libvirt/libvirt-sock \
    -v $(pwd)/assets/win10x64.xml:/app/config.xml windows-auto-deploy /app/config.xml
    ```
    *Note: The `--privileged` flag and `libvirt-sock` volume mount are examples for specific virtualization scenarios. Adjust your `docker run` command based on your target virtualization environment (e.g., QEMU/KVM, VirtualBox, Hyper-V).*

    For detailed usage and advanced options, refer to the `src/entry.sh` script and the example `compose.yml` and `kubernetes.yml` files.

## 📜 License

This project is licensed under the MIT License.
