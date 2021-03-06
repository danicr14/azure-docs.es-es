---
title: Panel Uso de los análisis de marketplace comercial del Centro de partners
description: Obtenga información sobre cómo acceder a todas las métricas de uso y facturación medida de las ofertas de máquina virtual.
author: dsindona
ms.author: dsindona
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
ms.date: 12/11/2019
ms.openlocfilehash: 33762540d14ea51e8325abe9a466007cd7cca748
ms.sourcegitcommit: 8dc84e8b04390f39a3c11e9b0eaf3264861fcafc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2020
ms.locfileid: "81262186"
---
# <a name="usage-dashboard-in-commercial-marketplace-analytics"></a>Panel Uso de los análisis de marketplace comercial

En este artículo se proporciona información sobre el panel de uso del Centro de partners. En este panel se muestran todas las métricas de uso y facturación medida de las ofertas de máquina virtual en dos pestañas independientes: Uso de máquinas virtuales y Uso de facturación medido.

Para acceder al panel de uso, abra el panel **[Analizar](https://partner.microsoft.com/dashboard/commercial-marketplace/analytics/summary)** en Marketplace comercial.

>[!NOTE]
> Para obtener definiciones detalladas de la terminología de análisis, consulte [Preguntas más frecuentes y terminología del análisis de marketplace comercial](./faq-terminology.md).

## <a name="usage-dashboard"></a>Panel de uso

En el panel de uso se representan las métricas de uso y uso de facturación medido de todas las ofertas de máquina virtual (VM). Se encuentran en dos pestañas independientes: Uso de máquinas virtuales y Uso de facturación medido.

En la pestaña Uso de máquinas virtuales se incluyen representaciones gráficas de los elementos siguientes:

- [Resumen de uso](#usage-summary)
- [Uso por geografía](#usage-by-geography)
- [Uso por ofertas](#usage-by-offers)
- [Tendencia de uso por ofertas y SKU](#usage-trend-by-offers-and-skus)
- [Uso por tipo de oferta](#usage-by-offer-type)
- [Uso por tamaño de VM](#usage-by-vm-size)
- [Uso por canal de ventas](#usage-by-sales-channel)
- [Datos de uso detallados](#detailed-usage-data)

> [!NOTE]
> Los informes de análisis se muestran de otra manera en Cloud Partner Portal (CPP) y en el Centro de partners. En CPP, **Conclusiones sobre los vendedores** tiene una pestaña de pedidos y uso en la que se muestran datos para las ofertas basadas en el uso y no basadas en el uso. En el Centro de partners, las métricas de uso se muestran en una página independiente.

### <a name="usage-summary"></a>Resumen de uso

En la tabla de resumen de uso se muestran las horas de uso del cliente para todas las ofertas que haya comprado.

- Las horas de uso normalizadas se definen para contabilizar el número de núcleos de VM ([número de núcleos de VM] x [horas de uso sin procesar]). Las máquinas virtuales designadas como "SHAREDCORE" usan 1/6 (o 0,1666) como multiplicador de [número de núcleos de máquina virtual].
- Las horas de uso sin procesar se definen como la cantidad de tiempo que las máquinas virtuales se han ejecutado en términos de horas.
- El valor de porcentaje representa el cambio de crecimiento del uso para el intervalo de fechas seleccionado ([uso del último mes – uso del primer mes])/ uso del primer mes).
- Los triángulos de color verde que apuntan hacia arriba indican un cambio de crecimiento.
- Los triángulos de color rojo que apuntan hacia abajo indican un cambio de crecimiento negativo con respecto al mes anterior.
- Los gráficos de microbarras representan valores mensuales. Para mostrar el valor de cada mes, desplace el puntero sobre las columnas del gráfico.

### <a name="usage-by-geography"></a>Uso por geografía

En el mapa térmico de **uso normalizado por geografía** se muestran las horas de uso asignadas en función del país del cliente. La variación de color del país representa la concentración de uso normalizado. Para volver a la vista original, presione el botón **Inicio** en el mapa.

### <a name="usage-by-offers"></a>Uso por ofertas

- En el gráfico circular de **uso normalizado por ofertas** se muestra un desglose de las horas de uso normalizado por ofertas según el intervalo de fechas seleccionado. En el gráfico se muestran las 5 ofertas principales y el resto se agrupan en la categoría "Todo el resto".
- En el gráfico de barras se muestra una tendencia de crecimiento mensual para el intervalo de fechas seleccionado. Las columnas de mes representan las horas de uso de las ofertas, con las horas de mayor uso para el mes correspondiente. En el gráfico de líneas se muestra la tendencia del porcentaje de crecimiento trazada en el eje Y secundario.
- Use el control deslizante de la parte superior del gráfico para desplazarse hacia la derecha y la izquierda a lo largo del eje X o centrarse en puntos de datos específicos.

### <a name="usage-trend-by-offers-and-skus"></a>Tendencia de uso por ofertas y SKU

En este gráfico se muestra la tendencia del uso normalizado de las SKU seleccionadas de una oferta. En la tabla de clasificación de la oferta se muestran las 50 ofertas principales con el uso más alto y se ordenan por horas de uso. En la tabla de clasificación de SKU se muestran las 50 SKU principales con el uso más alto de la oferta seleccionada.

### <a name="usage-by-offer-type"></a>Uso por tipo de oferta

- En el gráfico circular de **uso por tipo de oferta** se organiza el uso en función del tipo de oferta.
- En el gráfico se muestran las ofertas principales y el resto se agrupan como "Todo el resto".
- En el gráfico de **tendencias** se muestran las tendencias de crecimiento mes a mes. En la columna de mes se representa el uso por parte de los tipos de oferta principales de ese mes.

### <a name="usage-by-vm-size"></a>Uso por tamaño de VM

En este gráfico se representa la tendencia de uso de los tamaños de máquina virtual seleccionados (máximo 5) de todas las ofertas y SKU. El gráfico de columnas se apila con las horas de uso de los tamaños de máquina virtual seleccionados.

En la tabla de clasificación se muestran los 50 tamaños de máquina virtual principales con el uso más alto y ordenados por horas de uso.

### <a name="usage-by-sales-channel"></a>Uso por canal de ventas

- En el gráfico circular de uso por canal de ventas se organiza el uso en función del canal de ventas.
- En el gráfico se muestra el canal de ventas principal con el uso más alto y el resto se agrupa como "Todo el resto".
- En la columna de mes se representa el uso por canal de ventas principal de ese mes.
- Las características de este gráfico son las mismas que las del gráfico "Uso por ofertas".

### <a name="detailed-usage-data"></a>Datos de uso detallados

En la **tabla de detalles de uso** se muestra una lista numerada de los 1000 registros de uso principales ordenados por uso.

- Cada columna de la cuadrícula se puede ordenar.
- Los datos se pueden extraer a un archivo CSV si el recuento de los registros es inferior a 1000.
- Si el recuento de registros es superior a 1000, los datos exportados se colocarán de forma asincrónica en una página de descargas que estará disponible durante los próximos 30 días.
- Se pueden aplicar filtros a los **datos de uso detallados** para mostrar solo los datos que le interesen. Los datos se pueden filtrar por país, canal de ventas, tipo de licencia de Marketplace, tipo de uso, tipo y nombre de la oferta, evaluaciones gratuitas, identificador de la suscripción a Marketplace, identificador de cliente y nombre de la empresa.

> [!NOTE]
> Seleccione **Tipo de uso** en el filtro de página para ver los gráficos de la página en "Vista normalizada" o "Vista sin formato". Para estos gráficos, "Vista normalizada" es la vista predeterminada.

Los **Filtros de página de uso** se aplican en el nivel de página. Puede seleccionar varios filtros para representar el gráfico para los criterios que quiera ver, así como los datos que quiera que se muestren en la cuadrícula o exportación de "datos de uso detallados". Los filtros se aplican a los datos extraídos para el rango de datos que ha seleccionado en la esquina superior derecha de la página de pedidos.

- **Tipos de oferta** y **Nombres de oferta** solo se muestran para las ofertas que ha comprado durante el intervalo de fechas seleccionado. Los nombres de oferta de la lista se muestran para los tipos de oferta seleccionados en la lista.
- La selección predeterminada es "Todo" para cada una de las opciones de filtros, menos para **Tipo de uso**. La selección predeterminada para **Tipo de uso** es el uso normalizado. Para mostrar el uso sin procesar en los gráficos, seleccione "Uso sin procesar".
- Los filtros aplicados muestran las selecciones de recuento de las selecciones de filtro que se hayan realizado. Los filtros aplicados no se mostrarán para las selecciones predeterminadas.

> [!NOTE]
> En la sección Diccionario de datos del artículo [Preguntas más frecuentes y terminología](link needed) se ofrecen una definición detallada de cada uno de los campos de la cuadrícula "datos de pedido detallados", los filtros de página y todas las selecciones posibles.

En la pestaña **Uso de facturación medido** se muestra información de uso de los tipos de oferta, donde el uso se mide por dimensión de medidor. Actualmente, se presenta el uso por encima del límite del tipo de oferta de SaaS. En la pestaña se muestran representaciones gráficas de las tendencias de uso por encima del límite del uso de facturación medido de SaaS:

- **Tendencia superior al límite por dimensión de medidor**: muestra la tendencia superior al límite mensual para la dimensión de medidor seleccionada de una oferta. El eje X representa el mes y el eje Y representa la cantidad de uso. La unidad de medida del medidor personalizado también se muestra en el eje Y.
- **Tendencia superior al límite por SKU**: representa la tendencia de la cantidad de uso de la dimensión de medidor seleccionada por SKU. Las SKU que se muestran representan las cinco SKU principales con la mayor cantidad de uso de la oferta seleccionada.
- **Tendencia superior al límite por primeros 50 clientes**: Las 50 ofertas principales con las horas de uso más alto se muestran en una ***tabla de clasificación*** y se clasifican por el uso más alto del medidor personalizado. Seleccione un cliente en la tabla de clasificación para ver la tendencia de uso de una dimensión de medidor seleccionada.
- **Tendencia superior al límite por clientes principales**: presenta los percentiles de cliente principales que contribuyen al porcentaje del uso general. El percentil de cliente principal se muestra en el eje X y está determinado por la cantidad de uso del cliente. En el eje Y se muestra la cantidad de uso. Puede mostrar detalles manteniendo el puntero sobre los puntos del gráfico de líneas.

> [!NOTE]
> Los detalles de uso y todos los gráficos de esta página se muestran para cualquier dimensión de medidor seleccionada para el filtro de página.

## <a name="next-steps"></a>Pasos siguientes

- Para más información sobre los informes de análisis disponibles en el marketplace comercial del Centro de partners, consulte [Análisis del marketplace comercial en el Centro de partners](./analytics.md).
- Para ver los gráficos, las tendencias y los valores de datos agregados que resumen la actividad de la oferta en el marketplace, consulte [Panel Resumen de los análisis de marketplace comercial](./summary-dashboard.md).
- Para información sobre los pedidos en un formato gráfico que se pueda descargar, consulte [Panel Pedidos de los análisis de marketplace comercial](./orders-dashboard.md).
- Para obtener información detallada acerca de los clientes, incluidas las tendencias de crecimiento, consulte [Panel Cliente de los análisis de marketplace comercial](./customer-dashboard.md).
- Para ver una lista de las solicitudes de descarga de los últimos 30 días, consulte [Panel Descargas de los análisis de marketplace comercial](./downloads-dashboard.md).
- Para tener una vista consolidada de comentarios de los clientes sobre las ofertas de Azure Marketplace y AppSource, consulte [Panel Calificaciones y opiniones de los análisis de marketplace comercial](./ratings-reviews.md).
- Para ver las preguntas más frecuentes sobre los análisis de marketplace comercial y un diccionario completo de términos de datos, consulte [Preguntas más frecuentes y terminología del análisis de marketplace comercial](./faq-terminology.md).
