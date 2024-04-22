# Inventory

## Virtual machines

| Property     | Description                                      |
| ------------ | ------------------------------------------------ |
| Name         | app-database                                     |
| Domain       | app-database042343.westeurope.cloudapp.azure.com |
| Machine type | Standard A4 v2                                   |
| Memory       | 8 GiB                                            |
| CPU          | 4 vCPU                                           |
| Usage        | Instance for mysql host.                         |

---

| Property     | Description                                    |
| ------------ | ---------------------------------------------- |
| Name         | app-docker                                     |
| Domain       | app-docker025984.westeurope.cloudapp.azure.com |
| Machine type | Standard A4 v2                                 |
| Memory       | 8 GiB                                          |
| CPU          | 4 vCPU                                         |
| Usage        | Manage all internal tools.                     |

---

| Property     | Description                                 |
| ------------ | ------------------------------------------- |
| Name         | app-web                                     |
| Domain       | app-web812909.westeurope.cloudapp.azure.com |
| Machine type | Standard A4 v2                              |
| Memory       | 8 GiB                                       |
| CPU          | 4 vCPU                                      |
| Usage        | Launch web application                      |

## Users

| Syntax      | Description                                               |
| ----------- | --------------------------------------------------------- |
| Name        | admuser                                                   |
| Permissions | Sudoers                                                   |
| Usage       | User as admin user, only for installing new applications. |

| Syntax      | Description                                                          |
| ----------- | -------------------------------------------------------------------- |
| Name        | lostops                                                              |
| Permissions | Use Docker, make basic commands                                      |
| Usage       | Used for managing docker containers, that are used on rootless mode. |
