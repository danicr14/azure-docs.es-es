---
title: Localización de Azure Media Player
description: Compatibilidad con varios idiomas para usuarios de configuraciones regionales que no estén en inglés.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: reference
ms.date: 04/20/2020
ms.openlocfilehash: 34805c4eaae5d969fc2338c24f9f92404e065d15
ms.sourcegitcommit: acb82fc770128234f2e9222939826e3ade3a2a28
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81725881"
---
# <a name="localization"></a>Localización #

La compatibilidad con varios idiomas permite a los usuarios de configuraciones regionales distintas del inglés interactuar de forma nativa con el reproductor. Azure Media Player creará una instancia con un diccionario global de idiomas, que localizará los mensajes de error basados en el idioma de la página. Un desarrollador también puede crear una instancia del reproductor con un idioma establecido. El idioma predeterminado es el inglés (en).

> [!NOTE]
> Esta característica está todavía en pruebas y, como tal, está sujeta a errores.

```html
    <video id="vid1" class="azuremediaplayer amp-default-skin" data-setup='{"language":"es"}'>...</video>
```

Actualmente, Azure Media Player admite los siguientes idiomas con sus códigos de idioma correspondientes:

| Idioma            | Código | Idioma                | Código   | Idioma                | Código         |
|---------------------|------|-------------------------|--------|-------------------------|--------------|
| Inglés {predeterminado}   | en   | Croata                | hr     | Rumano                | ro           |
| Árabe              | ar   | Húngaro               | hu     | Eslovaco                  | sk           |
| Búlgaro           | bg   | Indonesio              | id     | Esloveno                 | sl           |
| Catalán             | ca   | Islandés               | is     | Serbio (cirílico)      | sr-cyrl-cs   |
| Checo               | cs   | Italiano                 | it     | Serbio (latino)         | sr-latn-rs   |
| Danés              | da   | Japonés                | ja     | Ruso                 | ru           |
| Alemán              | de   | Kazajo                  | kk     | Sueco                 | sv           |
| Griego               | el   | Coreano                  | ko     | Tailandés                    | th           |
| Español             | es   | Lituano              | lt     | Tagalo                 | tl           |
| Estonio            | et   | Letón                 | lv     | Turco                 | tr           |
| Vasco              | eu   | Malayo               | ms     | Ucraniano               | uk           |
| Persa               | fa   | Noruego (bokmal)     | nb     | Urdu                    | ur           |
| Finés             | fi   | Neerlandés                   | nl     | Vietnamita              | vi           |
| Francés              | fr   | Noruego (Nynorsk)     | nn     | Chino (simplificado)    | zh-hans      |
| Gallego            | gl   | Polaco                  | pl     | Chino (tradicional)   | zh-hant      |
| Hebreo              | he   | Portugués (Brasil)     | pt-br  |                         |              |
| Hindi               | hu   | Portugués (Portugal)   | pt-pt  |                         |              |


> [!NOTE]
> Si no desea que se produzca ninguna localización, debe aplicar el idioma inglés.

## <a name="next-steps"></a>Pasos siguientes ##

- [Inicio rápido de Azure Media Player](azure-media-player-quickstart.md)