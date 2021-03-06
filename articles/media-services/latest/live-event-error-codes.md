---
title: Códigos de error de eventos en directo de Azure Media Services | Microsoft Docs
description: En este artículo se enumeran los códigos de error de eventos en directo.
author: Juliako
manager: femila
editor: ''
services: media-services
documentationcenter: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2020
ms.author: juliako
ms.openlocfilehash: f9067562f67190b8bc04392f33078d4d3262f986
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2020
ms.locfileid: "77654586"
---
# <a name="media-services-live-event-error-codes"></a>Códigos de error de eventos en directo de Media Services

En las tablas de esta sección se enumeran los códigos de error de [eventos en directo](live-events-outputs-concept.md).

## <a name="liveeventconnectionrejected"></a>LiveEventConnectionRejected

Al suscribirse a los eventos de [Event Grid](https://docs.microsoft.com/azure/event-grid/) para un evento en directo, es posible que vea uno de los siguientes errores del evento [LiveEventConnectionRejected](media-services-event-schemas.md#liveeventconnectionrejected).

| Código de resultado | Descripción |
| ----------- | ----------- |
| MPE_RTMP_APPID_AUTH_FAILURE | Dirección URL de introducción incorrecta. |
| MPE_INGEST_ENCODER_CONNECTION_DENIED | El codificador de IP no está presente en la lista de direcciones IP permitidas configurada. |
| MPE_INGEST_RTMP_SETDATAFRAME_NOT_RECEIVED | El codificador RTMP no envió el comando setDataFrame. |
| MPE_INGEST_CODEC_NOT_SUPPORTED | No se admite el códec especificado. |
| MPE_INGEST_DESCRIPTION_INFO_NOT_RECEIVED |No se recibió la información de descripción de los elementos multimedia antes de que se entregaran los datos multimedia reales.|
| MPE_INGEST_MEDIA_QUALITIES_EXCEEDED |El recuento de calidades para el tipo de audio o vídeo superó el límite máximo permitido.|
| MPE_INGEST_BITRATE_AGGREGATED_EXCEEDED |La velocidad de bits entrante total en un servicio de canal o evento en directo superó el límite máximo permitido.|
| MPE_RTMP_FLV_TAG_TIMESTAMP_INVALID | La marca de tiempo de vídeo o audio FLVTag no es válida en el codificador de RTMP. |
| MPE_INGEST_FRAMERATE_EXCEEDED | Las transmisiones recibidas del codificador entrante con velocidades de fotogramas superaron el máximo permitido de 30 fps para codificar canales o eventos en directo.|
| MPE_INGEST_VIDEO_RESOLUTION_NOT_SUPPORTED | Las transmisiones recibidas del codificador entrante superaron las siguientes resoluciones permitidas: 1920 x 1088 para la codificación de canales o eventos en directo y 4096 x 2160 para canales o eventos en directo de paso a través.|

## <a name="liveeventencoderdisconnected"></a>LiveEventEncoderDisconnected

Es posible que vea uno de los siguientes errores del evento [LiveEventEncoderDisconnected](media-services-event-schemas.md#liveeventencoderdisconnected).

|Código de resultado|Descripción|
|---|---|
|MPE_RTMP_SESSION_IDLE_TIMEOUT|La sesión de RTMP agotó el tiempo de espera después de estar inactiva durante el límite de tiempo permitido.|
|MPE_RTMP_FLV_TAG_TIMESTAMP_INVALID|La marca de tiempo de vídeo o audio FLVTag no es válida en el codificador de RTMP.|
|MPE_CAPACITY_LIMIT_REACHED|El codificador envía datos demasiado rápido.|
|Códigos de error desconocidos|Estos códigos de error pueden variar desde un error de memoria hasta entradas duplicadas en el mapa de hash.|


## <a name="see-also"></a>Consulte también

[Códigos de error de puntos de conexión de streaming (origen)](streaming-endpoint-error-codes.md)

## <a name="next-steps"></a>Pasos siguientes

[Tutorial: Streaming en vivo con Media Services](stream-live-tutorial-with-api.md)
