---
title: archivo de inclusión
description: archivo de inclusión
services: virtual-machines
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 10/30/2019
ms.author: zivr
ms.custom: include file
ms.openlocfilehash: fb2eb2d237a1245627bbdb6f4f2eacbb9966a2c6
ms.sourcegitcommit: b80aafd2c71d7366838811e92bd234ddbab507b6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81421719"
---
Si coloca las máquinas virtuales en una sola región, reducirá la distancia física entre las instancias. Además, si las coloca en una sola zona de disponibilidad, estarán todavía más cercanas físicamente. Aun así, a medida que la superficie de Azure crece, una sola zona de disponibilidad puede abarcar varios centros de datos físicos, lo que es posible que provoque una latencia de red que puede afectar al rendimiento de la aplicación. 

Para acercar las máquinas virtuales lo más posible con la menor latencia posible, debe implementarlas dentro de un grupo de selección de ubicación de proximidad.

Un grupo de selección de ubicación de proximidad es una agrupación lógica que se usa para asegurarse de que los recursos de proceso de Azure se encuentran físicamente cercanos entre sí. Los grupos de selección de ubicación de proximidad son útiles para las cargas de trabajo en las que la latencia baja es un requisito.


- Baja latencia entre máquinas virtuales independientes.
- Baja latencia entre máquinas virtuales en un único conjunto de disponibilidad o conjunto de escalado de máquinas virtuales. 
- Baja latencia entre máquinas virtuales independientes, máquinas virtuales en varios conjuntos de disponibilidad o varios conjuntos de escalado. Puede tener varios recursos de proceso en un solo grupo de selección de ubicación para reunir una aplicación de varias capas. 
- Baja latencia entre varias capas de aplicación con diferentes tipos de hardware. Por ejemplo, la ejecución del back-end con la serie M en un conjunto de disponibilidad y el front-end en una instancia de la serie D, en un conjunto de escalado, en un solo grupo de selección de ubicación de proximidad.


![Gráfico para grupos de selección de ubicación de proximidad](./media/virtual-machines-common-ppg/ppg.png)

## <a name="using-proximity-placement-groups"></a>Uso de los grupos de selección de ubicación de proximidad 

Un grupo de selección de ubicación de proximidad es un nuevo tipo de recurso de Azure. Debe crear uno para poder usarlo con otros recursos. Una vez creado, podría usarse con máquinas virtuales, conjuntos de disponibilidad o conjuntos de escalado de máquinas virtuales. Un grupo de selección de ubicación de proximidad se especifica al crear recursos de proceso que proporcionan el identificador de grupo de selección de ubicación de proximidad. 

También puede mover un recurso existente a un grupo de selección de ubicación de proximidad. Al hacerlo, debe detener (desasignar) el recurso en primer lugar, ya que se volverá a implementar posiblemente en otro centro de datos de la región para satisfacer la restricción de colocación. 

En el caso de conjuntos de disponibilidad y conjuntos de escalado de máquinas virtuales, debe establecer el grupo de selección de ubicación de proximidad en el nivel de recursos, en lugar de en las máquinas virtuales individuales. 

Un grupo de selección de ubicación de proximidad es una restricción de colocación y no un mecanismo de anclaje. Se ancla a un centro de datos específico con la implementación del primer recurso para usarlo. Una vez que todos los recursos que usan el grupo de selección de ubicación de proximidad se han detenido (desasignado) o eliminado, ya no se anclan. Por lo tanto, cuando se usa un grupo de selección de ubicación de proximidad con varias series de máquinas virtuales, es importante especificar todos los tipos necesarios al principio en una plantilla cuando sea posible o seguir una secuencia de implementación, lo que mejorará las oportunidades de una implementación correcta. Si se produce un error en la implementación, reinicie esta con el tamaño de máquina virtual que ha dado error como el primer tamaño que se va a implementar.

## <a name="what-to-expect-when-using-proximity-placement-groups"></a>Qué esperar al usar los grupos con ubicación por proximidad 
Los grupos con ubicación por proximidad ofrecen colocalización en el mismo centro de datos. Sin embargo, dado que los grupos con ubicación por proximidad representan una restricción de implementación adicional, pueden producirse errores de asignación. Hay pocos casos de uso en los que puede ver errores de asignación al usar grupos con ubicación por proximidad:

- Al solicitar la primera máquina virtual en el grupo con ubicación por proximidad, el centro de datos se selecciona automáticamente. En algunos casos, se puede generar un error en la segunda solicitud de una SKU de máquina virtual diferente si no existe en ese centro de datos. En este caso, se devuelve un error **OverconstrainedAllocationRequest**. Para evitar esto, intente cambiar el orden en el que implementa las SKU o haga que ambos recursos se implementen mediante una sola plantilla de ARM.
-   En el caso de las cargas de trabajo elásticas, en las que se agregan y quitan instancias de máquina virtual, es posible que tener una restricción de grupo con ubicación por proximidad en la implementación produzca un error al realizar la solicitud, lo que da como resultado un error **AllocationFailure**. 
- Otra manera de lograr la elasticidad consiste en detener (desasignar) e iniciar las máquinas virtuales según sea necesario. Dado que la capacidad no se conserva una vez que se detiene (desasigna) una máquina virtual, si se vuelve a iniciar, puede producirse un error **AllocationFailure**.


## <a name="best-practices"></a>Procedimientos recomendados 
- Para la latencia más baja, use grupos de selección de ubicación de proximidad junto con redes aceleradas. Para obtener más información, consulte [Creación de una máquina virtual Linux con redes aceleradas](https://docs.microsoft.com/azure/virtual-network/create-vm-accelerated-networking-cli?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [Creación de una máquina virtual Windows con redes aceleradas](/azure/virtual-network/create-vm-accelerated-networking-powershell?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- Implemente todos los tamaños de máquina virtual en una sola plantilla. Para evitar llegar a hardware que no admite todas las SKU y tamaños de máquina virtual que necesita, incluya todas las capas de aplicación en una sola plantilla de modo que se implementen todas al mismo tiempo.
- Si va a crear scripts de la implementación mediante PowerShell, la CLI o el SDK, puede producirse un error de asignación `OverconstrainedAllocationRequest`. En este caso, debe detener o desasignar todas las máquinas virtuales existentes y cambiar la secuencia en el script de implementación para que empiece con la SKU o los tamaños de máquina virtual en los que se produjo el error. 
- Al reutilizar un grupo de selección de ubicación existente del que se han eliminado máquinas virtuales, espere a que la eliminación se complete antes de agregarle máquinas virtuales.
- Si su prioridad es la latencia, coloque las máquinas virtuales en un grupo de selección de ubicación de proximidad y toda la solución en una zona de disponibilidad. En cambio, si su prioridad es la resistencia, distribuya las instancias por varias zonas de disponibilidad (un solo grupo de selección de ubicación de proximidad no puede abarcar zonas).
