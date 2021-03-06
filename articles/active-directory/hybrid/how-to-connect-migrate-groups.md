---
title: 'Azure AD Connect: Migración de grupos de un bosque a otro | Microsoft Docs'
description: En este artículo se describen los pasos necesarios para migrar correctamente grupos de un bosque a otro en Azure AD Connect.
services: active-directory
author: billmath
manager: daveba
ms.service: active-directory
ms.topic: reference
ms.workload: identity
ms.date: 04/02/2020
ms.subservice: hybrid
ms.author: billmath
ms.collection: M365-identity-device-management
ms.openlocfilehash: 602c60de392afbff18bc141605a936636e48dbfe
ms.sourcegitcommit: ffc6e4f37233a82fcb14deca0c47f67a7d79ce5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81729697"
---
# <a name="migrate-groups-from-one-forest-to-another-for-azure-ad-connect"></a>Migración de grupos de un bosque a otro en Azure AD Connect

En este artículo se describen los pasos necesarios para migrar correctamente los grupos de un bosque a otro, de modo que los objetos de grupo migrados coincidan con los objetos existentes en la nube.

## <a name="prerequisites"></a>Prerrequisitos

- Azure AD Connect versión 1.5.18.0 o superior
- El atributo del delimitador de origen es `mS-DS-ConsistencyGuid`

A partir de la versión 1.5.18.0, Azure AD Connect comenzó a admitir el uso de `mS-DS-ConsistencyGuid` para los grupos. Si se elige `mS-DS-ConsistencyGuid` como atributo de delimitador de origen y el valor se rellena en AD, Azure AD Connect usa el valor de `mS-DS-ConsistencyGuid` como immutableId. De lo contrario, recurre al uso de `objectGUID`. Sin embargo, tenga en cuenta que Azure AD Connect **no** vuelve a escribir el valor en el atributo `mS-DS-ConsistencyGuid` de AD.

Durante un escenario de traslado entre bosques en el que un objeto de grupo se mueve de un bosque (por ejemplo, B1) a otro bosque (por ejemplo, B2), tendremos que copiar el valor `mS-DS-ConsistencyGuid` (si está presente) o el valor `objectGUID` del objeto del bosque B1 al atributo `mS-DS-ConsistencyGuid` del objeto en B2. 

Use los siguientes scripts como guía para ver cómo puede migrar un solo grupo del bosque B1 al bosque B2. No dude en usar este ejemplo como guía para realizar la migración de varios grupos.

En primer lugar, obtenemos el `objectGUID` y `mS-DS-ConsistencyGuid` del objeto de grupo en el bosque B1. Estos atributos se exportan a un archivo CSV.
```
<#
DESCRIPTION
============
This script will take DN of a group as input.
It then copies the objectGUID and mS-DS-ConsistencyGuid values along with other attributes of the given group to a CSV file.

This CSV file can then be used as input to Export-Group script
#>
Param(
       [ValidateNotNullOrEmpty()]
       [string]
       $dn,

       [ValidateNotNullOrEmpty()]
       [string]
       $outputCsv
)

$defaultProperties = @('samAccountName', 'distinguishedName', 'objectGUID', 'mS-DS-ConsistencyGuid')
$group  = Get-ADGroup -Filter "DistinguishedName -eq '$dn'" -Properties $defaultProperties -ErrorAction Stop
$results = @()
if ($group -eq $null)
{
       Write-Error "Group not found"
}
else
{
       $objectGUIDValue = [GUID]$group.'objectGUID'
       $mSDSConsistencyGuidValue = "N/A"
       if ($group.'mS-DS-ConsistencyGuid' -ne $null)
       {
              $mSDSConsistencyGuidValue = [GUID]$group.'mS-DS-ConsistencyGuid'
       }
       $adgroup = New-Object -TypeName PSObject
       $adgroup | Add-Member -MemberType NoteProperty -Name samAccountName -Value $($group.'samAccountName')
       $adgroup | Add-Member -MemberType NoteProperty -Name distinguishedName -Value $($group.'distinguishedName')
       $adgroup | Add-Member -MemberType NoteProperty -Name objectGUID -Value $($objectGUIDValue)
       $adgroup | Add-Member -MemberType NoteProperty -Name mS-DS-ConsistencyGuid -Value $($mSDSConsistencyGuidValue)
       $results += $adgroup
}

Write-Host "Exporting group to output file"
$results | Export-Csv "$outputCsv" -NoTypeInformation

```

A continuación, usamos el archivo CSV de salida generado para marcar el atributo `mS-DS-ConsistencyGuid` en el objeto de destino en el bosque B2.


```
<#
DESCRIPTION
============
This script will take DN of a group as input and the CSV file that was generated by Import-Group script
It copies either the objectGUID or mS-DS-ConsistencyGuid value from CSV file to the given object.

#>
Param(
       [ValidateNotNullOrEmpty()]
       [string]
       $dn,

       [ValidateNotNullOrEmpty()]
       [string]
       $inputCsv
)

$group  = Get-ADGroup -Filter "DistinguishedName -eq '$dn'" -ErrorAction Stop
if ($group -eq $null)
{
       Write-Error "Group not found"
}

$csvFile = Import-Csv -Path $inputCsv -ErrorAction Stop
$msDSConsistencyGuid = $csvFile.'mS-DS-ConsistencyGuid'
$objectGuid = [GUID] $csvFile.'objectGUID'
$targetGuid = $msDSConsistencyGuid

if ($msDSConsistencyGuid -eq "N/A")
{
       $targetGuid = $objectGuid
}

Set-ADGroup -Identity $dn -Replace @{'mS-DS-ConsistencyGuid'=$targetGuid} -ErrorAction Stop

```

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](whatis-hybrid-identity.md).
