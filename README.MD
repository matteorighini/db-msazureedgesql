# MS Azure SQL Edge Deployment with Docker Compose

This repository provides a lightweight, ready-to-use **Docker Compose** configuration to spin up an **Azure SQL Edge** instance. Azure SQL Edge is a specialized SQL engine optimized for edge workloads, supporting ARM64 and x64 architectures.

## 🚀 Quick Start

### Prerequisites

  * [Docker](https://www.docker.com/get-started) installed.
  * [Docker Compose](https://docs.docker.com/compose/install/) installed.

### Installation & Setup

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/matteorighini/db-msazureedgesql.git
    cd db-msazureedgesql/iac
    ```

2.  **Launch the Container:**

    ```bash
    docker compose --project-name='db-msazureedgesql' up
    ```

## 🛠 Configuration Details

The deployment includes the following settings in the `docker-compose.yml`:

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Image** | `mcr.microsoft.com/azure-sql-edge:latest` | The official Microsoft image. |
| **container\_name** | `db-msazureedgesql` | The docker container name that will be created. |
| **restart** | `unless-stopped` | Start policy of the container in Docker. |
| **ports** | `1433:1433` | Maps the internal SQL port to your local machine. |
| **ACCEPT\_EULA** | `Y` | Confirms acceptance of the End User License Agreement. |
| **MSSQL\_USER** | `SA` | Main user `sa` user. |
| **MSSQL\_SA\_PASSWORD** | *(Required)* | Strong password for the `sa` user. |
| **MSSQL\_PID** | `Developer` | DB licence to choose, between `Developer` and `Edge`. |
| **MSSQL\_AGENT\_ENABLED** | `TRUE` | Enable SQLServer Agent to handle T-SQL jobs. |
| **MSSQL\_COLLATION** | `SQL_Latin1_General_CP1_CI_AS` | DB collation. |


### Volume Persistence

By default, the configuration uses a named volume to ensure your databases persist even if the container is removed:

```yaml
volumes:
      - ../db:/var/opt/mssql
```

## 🔗 How to Connect

You can connect to the instance using your preferred SQL client (Azure Data Studio, SSMS, DBeaver, or VS Code) using these credentials:

  * **Server:** `localhost,1433`
  * **Username:** `sa`
  * **Password:** *[The password you set in the docker-compose.yml]*
  * **Encryption:** Trust Server Certificate = True



## 📝 License

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE).

-----

*Third-Party Software Notice: This repository utilizes the Azure SQL Edge Docker image, which is the proprietary software of Microsoft Corporation. Its use is governed by the Microsoft Software License Terms. By setting the ACCEPT_EULA variable to Y in the Docker configuration, you are formally agreeing to comply with those terms.*

*Development Use: This setup is intended for development and testing purposes only. It has not been hardened for production use. Users are responsible for implementing security best practices—including credential management, encryption, and network isolation—before deploying to any production environment.*