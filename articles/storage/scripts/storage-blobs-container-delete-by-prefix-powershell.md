---
title: 'Ejemplo de script de Azure PowerShell: eliminación de contenedores por prefijo | Microsoft Docs'
description: Elimine contenedores de blobs de Azure Storage según un prefijo de nombre de contenedor.
services: storage
author: tamram
ms.service: storage
ms.subservice: blobs
ms.devlang: powershell
ms.topic: sample
ms.date: 06/13/2017
ms.author: tamram
ms.openlocfilehash: 73c2f221d2ac0b3ceb76e3db0fdc6379a6dd330a
ms.sourcegitcommit: 0947111b263015136bca0e6ec5a8c570b3f700ff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/24/2020
ms.locfileid: "80060877"
---
# <a name="delete-containers-based-on-container-name-prefix"></a>Eliminación de contenedores según el prefijo del nombre de contenedor

Este script elimina contenedores en Azure Blob Storage según un prefijo del nombre del contenedor.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh-az.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/storage/delete-containers-by-prefix/delete-containers-by-prefix.ps1 "Delete containers by prefix")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Ejecute el siguiente comando para quitar el grupo de recursos, contenedores restantes y todos los recursos relacionados.

```powershell
Remove-AzResourceGroup -Name containerdeletetestrg
```

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos para eliminar contenedores según el prefijo del nombre de contenedor. Cada elemento de la tabla incluye vínculos a la documentación específica del comando.

| Get-Help | Notas |
|---|---|
| [Get-AzStorageAccount](/powershell/module/az.storage/get-azstorageaccount) | Obtiene una cuenta de Storage especificada o todas las cuentas de Storage de un grupo de recursos o la suscripción. |
| [Get-AzStorageContainer](/powershell/module/az.storage/Get-AzStorageContainer) | Enumera los contenedores de almacenamiento asociados con una cuenta de almacenamiento. |
| [Remove-AzStorageContainer](/powershell/module/az.storage/Remove-AzStorageContainer) | Elimina el contenedor de almacenamiento especificado. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).

Puede encontrar ejemplos de script adicionales de PowerShell de almacenamiento en los [ejemplos de PowerShell para Azure Blob Storage](../blobs/storage-samples-blobs-powershell.md).
