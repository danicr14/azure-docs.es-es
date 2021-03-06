---
title: 'Creación de una oferta de servicios de consultoría en el Centro de partners: Azure Marketplace'
description: En este artículo se explica cómo publicar una oferta de servicios de consultoría en Azure Marketplace o en AppSource mediante el Centro de partners.
author: anbene
ms.author: mingshen
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
ms.date: 04/06/2020
ms.openlocfilehash: eff37750f0580a28c9644ee1ffb7fe4e95038709
ms.sourcegitcommit: af1cbaaa4f0faa53f91fbde4d6009ffb7662f7eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2020
ms.locfileid: "81869790"
---
# <a name="create-a-consulting-service-offer"></a>Creación de una oferta de servicios de consultoría

> [!IMPORTANT]
> Estamos trasladando la administración de las ofertas de servicios de consultoría de Cloud Partner Portal al Centro de partners. Hasta que se migren las ofertas, siga las instrucciones de [Oferta de servicios de consultoría de Azure y Dynamics 365](https://docs.microsoft.com/azure/marketplace/cloud-partner-portal/consulting-services/cloud-partner-portal-consulting-services-publishing-offer) para Cloud Partner Portal para administrar las ofertas.

En este artículo se explica cómo publicar una oferta de servicios de consultoría en [Azure Marketplace](https://azuremarketplace.microsoft.com/) o en [AppSource](https://appsource.microsoft.com/). Lista de ofertas de servicios de consultoría basadas en Microsoft [Dynamics 365](https://dynamics.microsoft.com/) y Power Platform en AppSource. Lista de ofertas de servicios de consultoría basadas en Microsoft Azure en Azure Marketplace.

Para crear una oferta de servicios de consultoría en Azure Marketplace o en los servicios de consultoría de AppSource, primero debe [tener una cuenta de publicador en el Centro de partners](https://docs.microsoft.com/azure/marketplace/partner-center-portal/create-account) y la cuenta debe estar inscrita en el programa de Marketplace comercial. Antes de crear la oferta, revise los requisitos previos en [Requisitos previos de los servicios de consultoría](https://docs.microsoft.com/azure/marketplace/partner-center-portal/consulting-service-prerequisites).

## <a name="publishing-benefits"></a>Ventajas de publicación

Ventajas de publicar en Marketplace comercial:

- Promocionar la empresa con la marca de Microsoft.
- Llegar potencialmente a más de 100 millones de usuarios de Office 365 y Dynamics 365 en AppSource y a más de 200 000 organizaciones en Azure Marketplace.
- Recibir clientes potenciales de alta calidad de estos mercados.
- Promocionar sus servicios mediante los equipos de campo y televenta de Microsoft.

## <a name="create-a-new-offer"></a>Crear una nueva oferta

Después de cumplir los requisitos descritos anteriormente, siga estos pasos para crear una oferta de servicios de consultoría.

1. Inicie sesión en el [Centro de partners](https://partner.microsoft.com) y, después, seleccione **Panel** en el menú superior.
2. En la barra de navegación izquierda, seleccione **Marketplace comercial** y, después, seleccione **Información general**.

    :::image type="content" source="media/cs-menu-overview.png" alt-text="Muestra el menú de Marketplace comercial":::

3. Seleccione **+ Nueva oferta** y, a continuación, seleccione **Servicio de consultoría**.

    :::image type="content" source="media/cs-menu-newoffer.png" alt-text="Muestra el botón para crear una nueva oferta.":::

4. Escriba un **Identificador de oferta**. Se trata de un identificador único para cada oferta de su cuenta.

    - Este identificador es visible para los clientes en la dirección web de la oferta de Marketplace.
    - Use solo letras minúsculas, números, guiones y caracteres de subrayado, pero no espacios. La longitud está limitada a 50 caracteres. Por ejemplo, si escribe **test-offer-1**, la dirección URL de la oferta será `https://azuremarketplace.microsoft.com/marketplace/../test-offer-1`.
    - El identificador de oferta no se puede cambiar después de seleccionar **Crear**.

5. Escriba un **Alias de la oferta**. Este es el nombre que se usa para hacer referencia a la oferta en el Centro de partners.

    - Este nombre no se usa en Marketplace. Es diferente del nombre de la oferta y de otros valores que se muestran a los clientes. Puede usar este campo para asignar un nombre a la oferta que le resulte más útil para identificar la oferta internamente; no se muestra a los clientes.
    - El alias de la oferta no se puede cambiar después de seleccionar **Crear**.

Después de escribir estos dos valores, seleccione **Crear** para continuar en la página **Configuración de la oferta**.

## <a name="offer-setup"></a>Configuración de la oferta

Después de escribir un identificador de oferta y un alias de la oferta, el Centro de partners crea una borrador de la oferta y muestra la página **Configuración de la oferta**. Siga estos pasos para configurar la oferta.

### <a name="connect-lead-management"></a>Conexión de administración de clientes potenciales

Al publicar la oferta en Marketplace con el Centro de partners, _debe_ conectarla a un sistema de administración de relaciones con clientes (CRM) o de automatización de marketing. Esto le permite recibir información de contacto del cliente en cuanto alguien expresa interés en el producto o lo usa.

1. Seleccione **Conectar** para especificar dónde quiere que se envíen los clientes potenciales. El Centro de partners admite los siguientes sistemas:

    - [Dynamics 365](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-lead-management-instructions-dynamics) for Customer Engagement
    - [Marketo](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-lead-management-instructions-marketo)
    - [Salesforce](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-lead-management-instructions-salesforce)

    > [!NOTE]
    > Si su sistema CRM no aparece en la lista anterior, use [Tabla de Azure](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-lead-management-instructions-azure-table) o [Punto de conexión HTTPS](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-lead-management-instructions-https) para almacenar los datos del cliente potencial y, a continuación, exporte los datos al sistema CRM.

2. Conecte su oferta al destino de clientes potenciales cuando publique la oferta en el Centro de partners.
3. Compruebe que la conexión al destino de clientes potenciales está configurada correctamente. Después de publicarla en el Centro de partners, se valida la conexión y se le envía un cliente potencial de prueba. Mientras hace una vista previa de la oferta antes de publicarla, también puede probar la conexión de los clientes potenciales tratando de adquirir la oferta en el entorno de versión preliminar.
4. Asegúrese de que la conexión con el destino de clientes potenciales permanece actualizada para que no pierda ningún cliente potencial.

Estos son algunos recursos adicionales de administración de clientes potenciales:

- [Introducción a la administración de clientes potenciales](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-get-customer-leads)
- [Preguntas frecuentes de la administración de clientes potenciales](https://docs.microsoft.com/azure/marketplace/lead-management-for-cloud-marketplace#frequently-asked-questions)
- [Errores comunes de la configuración de clientes potenciales](https://docs.microsoft.com/azure/marketplace/lead-management-for-cloud-marketplace#common-lead-configuration-errors-during-publishing-on-cloud-partner-portal)
- [Introducción a la administración de clientes potenciales](https://assetsprod.microsoft.com/mpn/cloud-marketplace-lead-management.pdf) en formato PDF (asegúrese de que el bloqueador de elementos emergentes está desactivado)

Seleccione **Guardar borrador** antes de continuar con la siguiente sección, Propiedades.

### <a name="properties"></a>Propiedades

Esta página le permite establecer el producto principal más relacionado con el servicio de consultoría, establecer un tipo de servicio de consultoría y elegir productos aplicables.

1. Seleccione un **Producto principal** en la lista desplegable.
2. Seleccione un **Tipo de servicio de consultoría** en la lista desplegable:

    - **Valoración**: una evaluación del entorno del cliente para determinar la aplicabilidad de una solución y proporcionar una estimación de costo y tiempo.
    - **Sesión informativa**: introducción a una solución o un servicio de consultoría para determinar el interés del cliente mediante plataformas, demostraciones y ejemplos de clientes.
    - **Implementación**: una instalación completa que da como resultado una solución que funciona completamente. Limítese a las soluciones que se pueden implementar en dos semanas o menos.
    - **Prueba de concepto**: una implementación de ámbito limitado para determinar si una solución cumple los requisitos del cliente.
    - **Taller**: una involucración interactiva que se lleva a cabo en las instalaciones del cliente. Puede implicar entrenamiento, sesiones informativas, evaluaciones o demostraciones que se crean en los datos o el entorno del cliente.

1. Si ha seleccionado un producto principal de **Azure**, seleccione hasta tres **Áreas de solución**. Esto hace que sea más fácil para los clientes de Azure Marketplace encontrar la oferta. Si no ha seleccionado Azure, omita este paso.
2. Si ha seleccionado un producto principal _distinto_ de Azure, seleccione hasta tres **Productos aplicables**. Esto hace que sea más fácil para los clientes de AppSource encontrar la oferta. Para más información, consulte [Instrucciones sobre listas de servicios de consultoría de Microsoft AppSource](https://go.microsoft.com/fwlink/?LinkId=828734&amp;clcid=0x409) (PDF).
3. Seleccione hasta seis **Sectores** en los que la oferta sea aplicable. Esto hace que sea más fácil para los clientes encontrar la oferta.
4. Agregue hasta tres **Competencias** que su empresa haya conseguido para mostrar en la lista de ofertas de servicios de consultoría. Se requiere al menos una competencia, excepto en el caso de MSP experto de Azure y MSP de Redes de Azure.

Seleccione **Guardar borrador** antes de continuar con la siguiente sección, Descripción de la oferta.

## <a name="offer-listing"></a>Descripción de la oferta

Aquí puede definir los detalles de la oferta que se muestran en Marketplace. Esto incluye el nombre de la oferta, la descripción, las imágenes, etc. Asegúrese de seguir las directivas que se detallan en la [página de directivas de Microsoft](https://docs.microsoft.com/legal/marketplace/certification-policies#800-consulting-services) mientras configura esta oferta.

> [!NOTE]
> No es necesario que los detalles de la oferta estén en inglés si la descripción de la oferta comienza con la frase &quot;Esta aplicación solo está disponible en [idioma distinto del inglés].&quot; También es adecuado proporcionar un vínculo para ofrecer el contenido en un idioma distinto al utilizado en la descripción de la oferta.

### <a name="name"></a>Nombre

El nombre que escriba aquí se muestra como el título de la oferta. Este campo se rellena previamente con el texto que escribió en el cuadro de texto **Alias de la oferta** al crear la oferta. Puede cambiar este nombre más adelante.

El nombre:

- Puede contener marcas comerciales (y puede incluir símbolos de marca comercial o copyright).
- No puede tener más de 50 caracteres.
- No puede incluir emojis.

### <a name="search-results-summary"></a>Resumen de los resultados de la búsqueda

Proporcione una breve descripción de la oferta. Puede tener una longitud de hasta 100 caracteres y se usa en los resultados de la búsqueda de Marketplace.

### <a name="description"></a>Descripción

Proporcione una descripción más larga de la oferta (hasta 3000 caracteres). Se muestra a los clientes en la información general de la lista de Marketplace.

Incluya uno o varios de los siguientes elementos en la descripción:

- Valor y beneficios principales que proporciona la oferta
- Asociaciones de categoría o de sector o ambas
- Oportunidades de compra desde la aplicación
- Cualquier divulgación necesaria

Estas son algunas sugerencias para escribir la descripción:

- Describa claramente la propuesta de valor de la oferta en las primeras frases de la descripción. Incluya los siguientes elementos:
  - Descripción de la oferta.
  - Tipo de usuario que se beneficia de la oferta.
  - Necesidades o problemas del cliente que aborda la oferta.
- Recuerde que estas primeras frases podrían mostrarse en los resultados de la búsqueda.
- No se base exclusivamente en las características y funcionalidades para vender su producto. En su lugar, céntrese en el valor que proporciona la oferta.
- Intente usar un vocabulario específico del sector o palabras relacionadas con las ventajas.

Para que la descripción sea más atractiva, use el editor de texto enriquecido para darle formato. El editor de texto enriquecido le permite agregar números, viñetas, negritas, cursivas y sangrías para que la descripción sea más legible.

:::image type="content" source="media/cs-rich-text-editor.png" alt-text="Muestra el editor de texto enriquecido para escribir la descripción de la oferta." border="false":::

### <a name="keywords"></a>Palabras clave

Escriba hasta tres palabras clave de búsqueda adecuadas para el producto principal y el servicio de consultoría. Esto facilitará la búsqueda de la oferta.

### <a name="duration"></a>Duration

Establezca la duración esperada de este compromiso con el cliente.

### <a name="contact-information"></a>Información de contacto

Debe proporcionar el nombre, correo electrónico y número de teléfono de un **Contacto principal** y un **Contacto secundario**. Esta información no se muestra a los clientes. Está disponible para Microsoft y se puede proporcionar a los asociados como Proveedor de soluciones en la nube (CSP).

### <a name="supporting-documents"></a>Documentos relacionados

Agregue hasta tres (pero al menos uno) documentos PDF para la oferta.

### <a name="marketplace-images"></a>Imágenes de Marketplace

Proporcione logotipos e imágenes para usarlos con la oferta. Todas las imágenes deben estar en formato .PNG. Las imágenes borrosas se rechazarán.

>[!Note]
>Si tiene un problema al cargar archivos, asegúrese de que la red local no bloquee el servicio https://upload.xboxlive.com que usa el Centro de partners.

#### <a name="store-logos"></a>Logotipos de Store

Proporcione archivos .png del logotipo de la oferta en cada uno de los siguientes tamaños de píxel:

- **Pequeño (48 x 48)**
- **Grande (216 x 216)**

Todos los logotipos son necesarios y se usan en lugares diferentes de la lista de Marketplace.

#### <a name="screenshots-optional"></a>Capturas de pantalla (opcional)

Agregue hasta cinco capturas de pantalla que muestren el funcionamiento de la oferta. Cada una debe tener un tamaño de 1280 x 720 píxeles y el formato .png.

#### <a name="videos-optional"></a>Vídeos (opcional)

Agregue hasta cuatro vídeos que muestren la oferta. Escriba el nombre del vídeo, su dirección web (URL) y una imagen en miniatura en formato .png del vídeo con un tamaño de 1280 x 720 píxeles.

Seleccione **Guardar borrador** antes de continuar con la siguiente sección, Precios y disponibilidad.

## <a name="pricing-and-availability"></a>Precios y disponibilidad

Aquí podrá definir elementos como los precios, el mercado y una clave privada.

1. **Mercado**: establezca el mercado en el que estará disponible la oferta. Solo puede seleccionar un mercado por oferta.
    1. En el caso de los mercados de Estados Unidos o Canadá, seleccione **Editar Estados** (o **provincias**) para especificar dónde estará disponible la oferta.
2. **Público preliminar**: configure la **Clave oculta** que se usa para establecer la audiencia privada de la oferta.
3. **Precios**: Especifique si la oferta es **Gratuita** o **De pago**.

    > [!NOTE]
    > Las ofertas de servicios de consultoría son solo para la lista. Cualquier transacción se realizará directamente, fuera de Marketplace comercial.

4. Para una oferta de pago, especifique el **Precio y moneda** y si el precio es **Fijo** o **Estimado**. Si es estimado, debe especificar en la descripción los factores que afectan al precio.
5. Seleccione **Guardar borrador**.

## <a name="review-and-publish"></a>Revisión y publicación

Una vez que haya completado todas las secciones necesarias de la oferta, puede enviar la oferta para su revisión y publicación.

1. Cuando esté listo para publicar la oferta del servicio de consultoría, haga clic en **Revisar y publicar**.
2. Revise los detalles de la página de envío final.
3. Si es necesario, escriba una nota al equipo de certificación si cree que alguno de los detalles de la oferta requiere explicación.
4. Cuando esté listo, seleccione **Enviar**.
5. En la página **Información general de la oferta** se muestra la fase de publicación en la que se encuentra la oferta.

Para más información sobre el tiempo que puede esperar que esté la oferta en cada fase de publicación, consulte [Comprobación del estado de publicación de la oferta de Marketplace comercial](https://docs.microsoft.com/azure/marketplace/partner-center-portal/publishing-status).

## <a name="update-your-existing-consulting-service-offers"></a>Actualización de las ofertas de servicios de consultoría existentes

- [Actualización de una oferta existente en Marketplace comercial](https://docs.microsoft.com/azure/marketplace/partner-center-portal/update-existing-offer)
