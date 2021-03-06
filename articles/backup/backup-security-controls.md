---
title: Controles de seguridad
description: Obtenga información sobre los controles de seguridad que se usan en el servicio de Azure Backup. Estos controles ayudan al servicio a evitar, detectar y responder a las vulnerabilidades de seguridad.
ms.topic: conceptual
ms.date: 09/23/2019
ms.openlocfilehash: 0e3f5ce942ea8aef9bf5eb98883ae1e72a7ab239
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2020
ms.locfileid: "74172133"
---
# <a name="security-controls-for-azure-backup"></a>Controles de seguridad para Azure Backup

En este artículo se explican los controles de seguridad integrados en Azure Backup.

[!INCLUDE [Security controls Header](../../includes/security-controls-header.md)]

## <a name="network"></a>Red

| Control de seguridad | Sí/No | Notas | Documentación
|---|---|--|
| Compatibilidad con punto de conexión de servicio| No |  |  |
| Compatibilidad con la inserción de redes virtuales| No |  |  |
| Compatibilidad con el aislamiento de red y los firewalls| Sí | La tunelización forzada es compatible con copia de seguridad de VM. La tunelización forzada no se admite para las cargas de trabajo que se ejecutan en VM. |  |
| Compatibilidad con la tunelización forzada| No |  |  |

## <a name="monitoring--logging"></a>Supervisión y registro

| Control de seguridad | Sí/No | Notas| | Documentación
|---|---|--|
| Compatibilidad con la supervisión de Azure (Log Analytics, Application Insights, etc.)| Sí | Log Analytics se admite mediante registros de recursos. Para más información, consulte [Supervisión de cargas de trabajo protegidas por Azure Backup con Log Analytics](https://azure.microsoft.com/blog/monitor-all-azure-backup-protected-workloads-using-log-analytics/). |  |
| Registro y auditoría del plano de administración y de control| Sí | Todas las acciones que desencadena el cliente desde Azure Portal se registran en los registros de actividad. |  |
| Registro y auditoría del plano de datos| No | No se puede acceder al plano de datos de Azure Backup directamente.  |  |

## <a name="identity"></a>Identidad

| Control de seguridad | Sí/No | Notas| | Documentación
|---|---|--|
| Authentication| Sí | La autenticación se realiza a través de Azure Active Directory. |  |
| Authorization| Sí | Se usan roles RBAC integrados y creados por el cliente. Para más información, consulte [Uso del control de acceso basado en roles para administrar puntos de recuperación de Azure Backup](/azure/backup/backup-rbac-rs-vault). |  |

## <a name="data-protection"></a>Protección de los datos

| Control de seguridad | Sí/No | Notas | | Documentación
|---|---|--|
| Cifrado del lado servidor en reposo: Claves administradas por Microsoft | Sí | Uso de cifrado del servicio de almacenamiento para las cuentas de almacenamiento. |  |
| Cifrado del lado servidor en reposo: claves administradas por el cliente (BYOK) | No |  |  |
| Cifrado de nivel de columna (Azure Data Services)| No |  |  |
| Cifrado en tránsito (por ejemplo, cifrado de ExpressRoute, cifrado en la red virtual y cifrado de red virtual a red virtual)| No | Se usa HTTPS. |  |
| Llamadas a API cifradas| Sí |  |  |

## <a name="configuration-management"></a>Administración de configuración

| Control de seguridad | Sí/No | Notas| | Documentación
|---|---|--|
| Compatibilidad con la administración de configuración (control de versiones de configuración, etc.)| Sí|  |  |

## <a name="next-steps"></a>Pasos siguientes

- Más información sobre los [controles de seguridad integrados en los servicios de Azure](../security/fundamentals/security-controls.md).
