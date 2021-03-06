---
title: Materiales de color
description: Describe el tipo de material de color.
author: jakrams
ms.author: jakras
ms.date: 02/11/2020
ms.topic: article
ms.openlocfilehash: 7cbcaefcc087c9f1c7c09668a27fbdef9a4802d3
ms.sourcegitcommit: 642a297b1c279454df792ca21fdaa9513b5c2f8b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2020
ms.locfileid: "80679166"
---
# <a name="color-materials"></a>Materiales de color

*Los materiales de color* son uno de los [tipos de material](../../concepts/materials.md) admitidos en Azure Remote Rendering. Se usan para las [mallas](../../concepts/meshes.md) que no deben recibir ningún tipo de iluminación, sino que deben tener una luminosidad completa en todo momento. Este podría ser el caso de los materiales "brillantes", como los paneles de automóviles, las bombillas o los datos que ya incorporan iluminación estática, como los modelos obtenidos mediante [fotogrametría](https://en.wikipedia.org/wiki/Photogrammetry).

Los materiales de color tienen una representación más eficiente que los [materiales de PBR](pbr-materials.md) debido a su modelo de sombreado más sencillo. También admiten diferentes modos de transparencia.

## <a name="common-material-properties"></a>Propiedades de material comunes

Estas propiedades son comunes a todos los materiales:

* **albedoColor:** Este color se multiplica con otros colores, como *albedoMap* o los *colores del vértice*. Si el elemento *transparency* está habilitado en un material, el canal alfa se usa para ajustar la opacidad. En este contexto, `1` significa totalmente opaco y `0`, completamente transparente. El valor predeterminado es el blanco.

  > [!NOTE]
  > Dado que los materiales de color no reflejan el entorno, un material de color completamente transparente se vuelve invisible. Esto es diferente para los [materiales de PBR](pbr-materials.md).

* **albedoMap:** una [textura en 2D](../../concepts/textures.md) para valores albedo por píxel.

* **alphaClipEnabled** y **alphaClipThreshold:** si *alphaClipEnabled* es true, no se dibujarán todos los píxeles en que el valor alfa de albedo sea inferior a *alphaClipThreshold*. El recorte alfa se puede usar incluso sin habilitar la transparencia y se representa mucho más rápidamente. Sin embargo, los materiales recortados alfa se siguen representando más lentamente que los materiales opacos. De forma predeterminada, el recorte alfa está deshabilitado.

* **textureCoordinateScale** y **textureCoordinateOffset:** la escala se multiplica en las coordenadas de textura UV y se le agrega el desplazamiento. Se puede usar para ajustar y desplazar las texturas. La escala predeterminada es (1, 1) y el desplazamiento, (0, 0).

* **useVertexColor:** si la malla contiene colores de vértice y esta opción está habilitada, los colores de los vértices de las mallas se multiplican en *albedoColor* y *albedoMap*. De forma predeterminada, los colores de vértice están deshabilitados.

* **isDoubleSided:** si el valor de doble cara está establecido en true, los triángulos con este material se representan aunque la cámara apunte a sus caras posteriores. Esta opción está deshabilitada de manera predeterminada. Consulte también [Representación en una sola cara](single-sided-rendering.md).

## <a name="color-material-properties"></a>Propiedades de material de color

Las propiedades siguientes son específicas de los materiales de color:

* **vertexMix:** este valor entre `0` y `1` especifica en qué medida el color del vértice de una [malla](../../concepts/meshes.md) contribuye al color final. En el valor predeterminado de 1, el color del vértice se multiplica por completo en el color albedo. Con un valor de 0, los colores de los vértices se omiten por completo.

* **transparencyMode:** al contrario de los [materiales de PBR](pbr-materials.md), los materiales de color distinguen entre diferentes modos de transparencia:

  1. **Opaque:** el modo predeterminado deshabilita la transparencia. Sin embargo, el recorte alfa todavía es posible y, si es suficiente, es la opción preferible.
  
  1. **AlphaBlended:** este modo es similar al modo de transparencia para los materiales de PBR. Debe usarse para los materiales transparentes, como el cristal.

  1. **Additive:** este modo es el modo de transparencia más sencillo y eficaz. La contribución del material se agrega a la imagen representada. Este modo se puede usar para simular objetos brillantes (pero transparentes, igualmente), como los marcadores que se usan para resaltar objetos importantes.

## <a name="next-steps"></a>Pasos siguientes

* [Materiales de PBR](pbr-materials.md)
* [Texturas](../../concepts/textures.md)
* [Mallas](../../concepts/meshes.md)
