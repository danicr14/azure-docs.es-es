---
title: Oferta de imágenes de contenedor de Azure | Azure Marketplace
description: Información general del proceso de publicación de una oferta de contenedor en Azure Marketplace.
author: dsindona
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
ms.date: 11/02/2018
ms.author: dsindona
ms.openlocfilehash: 81908de5c2fb3960684ed6cf37952e8815d8a5d5
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "82148310"
---
# <a name="containers"></a>Contenedores

> [!IMPORTANT]
> A partir del 13 de abril de 2020, se comenzará a trasladar la administración de las ofertas de contenedores de Azure al Centro de partners. Después de la migración, las ofertas se crearán y administrarán en el Centro de partners. Siga las instrucciones que se indican en [Creación de una oferta de contenedor de Azure](https://docs.microsoft.com/azure/marketplace/partner-center-portal/create-azure-container-offer) para administrar las ofertas migradas.

<table> <tr> <td>En esta sección se explica cómo publicar una imagen de contenedor en <a href="https://azuremarketplace.microsoft.com">Azure Marketplace</a>.  
El tipo de oferta de contenedor admite imágenes de contenedor de Docker aprovisionadas como instancias de <a href="https://docs.microsoft.com/azure/aks/index">Azure Kubernetes Service</a> o <a href="https://docs.microsoft.com/azure/container-instances/container-instances-overview">Azure Container Instances</a> y hospedadas en un repositorio de <a href="https://docs.microsoft.com/azure/container-registry">Azure Container Registry</a>. </td> <td><img src="./media/container-icon.png"  alt="Azure container icon" /></td> </tr> </table>

## <a name="offer-components"></a>Componentes de la oferta

En esta sección se describen los elementos de la publicación de un contenedor, y está pensada como una guía para el publicador en Azure Marketplace. La publicación se divide en las siguientes partes principales:

- [Requisitos previos](./cpp-prerequisites.md): se enumeran los requisitos técnicos y empresariales antes de crear o publicar una oferta de contenedor.
- [Creación de la oferta](./cpp-create-offer.md): se enumeran los pasos necesarios para crear una entrada de oferta de contenedor mediante Cloud Partner Portal.
- [Preparación de los recursos técnicos](./cpp-create-technical-assets.md): este paso se refiere a cómo crear los recursos técnicos para una solución de contenedor como una oferta en Azure Marketplace.
- [Publicación de la oferta](./cpp-publish-offer.md): se refiere a cómo enviar la oferta para publicarla en Azure Marketplace.

## <a name="container-publishing-process"></a>Proceso de publicación del contenedor

En el diagrama siguiente se ilustran los pasos generales de la publicación de una oferta de máquina virtual.
![Pasos para publicar una oferta](./media/containers-offer-process.png)

Los pasos generales para la publicación de una oferta de contenedor son:

1. Crear la oferta: proporcione información detallada sobre la oferta. Esta información incluye: la descripción de la oferta, materiales de marketing, información de soporte técnico y especificaciones de recursos.
2. Crear los recursos empresariales y técnicos: creación de los recursos empresariales (documentos legales y materiales de marketing) y los recursos técnicos de la solución asociada (las imágenes de contenedor hospedadas en Azure Container Registry).
3. Crear las SKU: cree las SKU asociadas a la oferta. Se necesita una SKU única para cada imagen que se vaya a publicar.
4. Certificar y publicar la oferta: después de completar la oferta y los recursos técnicos, puede enviar la oferta. Este envío inicia el proceso de publicación. Durante este proceso, la solución se prueba, se valida, se certifica y luego se publica en Azure Marketplace.

## <a name="next-steps"></a>Pasos siguientes

Antes de considerar estos pasos, debe cumplir los [requisitos técnicos y empresariales](./cpp-prerequisites.md) para publicar un contenedor en Microsoft Azure Marketplace.
