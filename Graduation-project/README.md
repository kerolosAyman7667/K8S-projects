# BridgeX - Graduation Project

## Project Overview
BridgeX is a robust application deployed on Kubernetes. 

## Technology Stack & Tools

### Security & Secret Management
*   **HashiCorp Vault**: Implemented for centralized, secure secret management.
*   **Secrets Store CSI Driver**: Integrates Vault with Kubernetes to inject secrets (DB credentials, API keys, Certificates) directly into pods as volumes, ensuring no sensitive data is stored in plain text manifests.

### Storage
*   **TrueNAS**: Provides the underlying NFS storage infrastructure.
*   **Democratic CSI**: A CSI driver utilized to dynamically provision and manage persistent volumes (PVCs) backed by TrueNAS NFS shares.

### Backend & Data Services
*   **Backend Service**: Custom application (`bridgex/backend`) handling core business logic, authentication (JWT), and file processing.
*   **MySQL 8.0**: Relational database deployed as a StatefulSet to ensure data persistence and ordered deployment.
*   **Redis**: In-memory data structure store deployed as a StatefulSet for high-performance caching.
*   **Gotenberg**: A Docker-powered stateless API for converting files (HTML, Markdown, Word) to PDF.

### Frontend & Proxy
*   **Frontend**: React/Vite application served via **Nginx**, configured with reverse proxy rules for API and WebSocket connections.
*   **Caddy**: Versatile web server used to serve static documentation and handle routing.

### Scalability & Operations
*   **Horizontal Pod Autoscaler (HPA)**: Configured for the backend service to automatically scale the number of pods based on CPU utilization metrics.
*   **Vertical Pod Autoscaler (VPA)**: Implemented for the MySQL database to automatically adjust CPU and memory requests/limits based on usage patterns.
