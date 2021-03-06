---
title: Solución de problemas
description: Información de solución de problemas de Azure Remote Rendering
author: florianborn71
ms.author: flborn
ms.date: 02/25/2020
ms.topic: troubleshooting
ms.openlocfilehash: b86af2ff8fad3793fc47cec9399fd499c1cabba7
ms.sourcegitcommit: acb82fc770128234f2e9222939826e3ade3a2a28
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81681855"
---
# <a name="troubleshoot"></a>Solución de problemas

En esta página se enumeran los problemas comunes que interfieren con Azure Remote Rendering y las maneras de resolverlos.

## <a name="client-cant-connect-to-server"></a>El cliente no se puede conectar al servidor

Asegúrese de que los firewalls (en el dispositivo, dentro de los enrutadores, etc.) no bloqueen los puertos siguientes:

* **50051 (TCP)** : necesario para la conexión inicial (protocolo de enlace HTTP)
* **8266 (TCP + UDP)** : necesario para la transferencia de datos
* **5000 (TCP)** , **5433 (TCP)** , **8443 (TCP)** : necesario para [ArrInspector](tools/arr-inspector.md)

## <a name="error-disconnected-videoformatnotavailable"></a>Error "Desconectado: VideoFormatNotAvailable"

Compruebe que la GPU admita la descodificación de vídeo de hardware. Consulte [Equipo de desarrollo](../overview/system-requirements.md#development-pc).

Si está trabajando en un equipo portátil con dos GPU, es posible que la GPU que se ejecuta de forma predeterminada no proporcione la funcionalidad de descodificación de vídeo de hardware. Si es así, intente forzar la aplicación para que use la otra GPU. Esto suele ser posible en la configuración del controlador de GPU.

## <a name="h265-codec-not-available"></a>Códec H265 no disponible

Hay dos razones por las que el servidor puede rechazar la conexión debido a un error de **códec no disponible**.

**El códec H265 no está instalado:**

En primer lugar, asegúrese de instalar **Extensiones de vídeo HEVC** como se menciona en la sección [Software](../overview/system-requirements.md#software) de los requisitos del sistema.

Si sigue experimentando problemas, asegúrese de que la tarjeta gráfica admite H265 y de que tiene instalado el controlador de gráficos más reciente. Consulte la sección [Equipo de desarrollo](../overview/system-requirements.md#development-pc) de los requisitos del sistema para obtener información específica del proveedor.

**El códec está instalado, pero no se puede usar:**

La razón de este problema es una configuración de seguridad incorrecta en los archivos DLL. Este problema no se manifiesta al intentar ver vídeos codificados con H265. La reinstalación del códec tampoco soluciona el problema. En su lugar, realice los pasos siguientes:

1. Abra una instancia de **PowerShell con derechos de administrador** y ejecute el comando:

    ```PowerShell
    Get-AppxPackage -Name Microsoft.HEVCVideoExtension
    ```
  
    Ese comando debería generar el objeto `InstallLocation` del códec, similar al siguiente:
  
    ```cmd
    InstallLocation   : C:\Program Files\WindowsApps\Microsoft.HEVCVideoExtension_1.0.23254.0_x64__5wasdgertewe
    ```

1. Abra esa carpeta en el Explorador de Windows.
1. Debería contener las subcarpetas **x86** y **x64**. Haga clic con el botón derecho en una de las carpetas y elija **Propiedades**.
    1. Seleccione la pestaña **Seguridad** y, después, haga clic en el botón **Opciones avanzadas**.
    1. Haga clic en **Cambiar** en **Propietario**.
    1. Escriba **Administradores** en el campo de texto.
    1. Haga clic en **Comprobar nombres** y luego en **Aceptar**.
1. Repita los pasos anteriores para la otra carpeta.
1. Repita también los pasos anteriores en cada archivo DLL de ambas carpetas. Debe haber cuatro archivos DLL en total.

Para comprobar que la configuración ahora es correcta, realice el procedimiento siguiente con cada archivo DLL:

1. Seleccione **Propiedades > Seguridad > Editar**.
1. Recorra la lista de todos los **Grupos/Usuarios** y asegúrese de que cada uno tenga el derecho **Lectura y ejecución** establecido (deben tener la marca de verificación en la columna **Permitir**)

## <a name="low-video-quality"></a>Calidad de vídeo baja

La calidad de vídeo puede verse afectada por la calidad de la red o la falta del códec de vídeo H265.

* Consulte los pasos para [identificar problemas de red](#unstable-holograms).
* Consulte los [requisitos del sistema](../overview/system-requirements.md#development-pc) para instalar el controlador de gráficos más reciente.

## <a name="video-recorded-with-mrc-does-not-reflect-the-quality-of-the-live-experience"></a>El vídeo grabado con MRC no refleja la calidad de la experiencia en directo

Se puede grabar un vídeo en Hololens a través de [Captura de realidad mixta (MRC)](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-capture-for-developers). Sin embargo, el vídeo resultante tiene una calidad peor que la experiencia en directo por dos motivos:
* La velocidad de fotogramas de vídeo se limita a 30 Hz en lugar de 60 Hz.
* Las imágenes de vídeo no se someten al paso de procesamiento de [reproyección de la fase final](../overview/features/late-stage-reprojection.md), por lo que el vídeo parece más entrecortado.

Ambas limitaciones son inherentes de la técnica de grabación.

## <a name="black-screen-after-successful-model-loading"></a>Pantalla negra tras cargar el modelo correctamente

Si está conectado al entorno de ejecución de representación y ha cargado un modelo correctamente, pero después solo ve una pantalla negra después, puede deberse a distintas causas.

Se recomienda realizar las comprobaciones siguientes antes de realizar un análisis más exhaustivo:

* ¿El códec H265 está instalado? Aunque debería haber una reserva para el códec H264, hemos detectado casos en los que esta reserva no funcionó correctamente. Consulte los [requisitos del sistema](../overview/system-requirements.md#development-pc) para instalar el controlador de gráficos más reciente.
* Al usar un proyecto de Unity, cierre Unity, elimine las carpetas temporales *library* y *obj* del directorio del proyecto, y cargue o cree el proyecto de nuevo. En algunos casos, los datos almacenados en caché provocaron el fracaso del ejemplo sin ningún motivo aparente.

Si estos dos pasos no ayudan, debe averiguar si el cliente recibe fotogramas de vídeo. La consulta se puede realizar mediante programación, como se explica en el capítulo [Consultas de rendimiento del lado del servidor](../overview/features/performance-queries.md). El objeto `FrameStatistics struct` tiene un miembro que indica el número de fotogramas de vídeo que se han recibido. Si este número es mayor que 0 y aumenta con el tiempo, el cliente recibe fotogramas de vídeo reales del servidor. Por lo tanto, debe tratarse de un problema en el lado cliente.

### <a name="common-client-side-issues"></a>Problemas comunes del lado cliente

**El modelo no está dentro del tronco de la vista:**

En muchos casos, el modelo se muestra correctamente pero se encuentra fuera del tronco de la cámara. Un motivo habitual es que el modelo se ha exportado con una dinamización muy descentrada y el plano de recorte lejano de la cámara lo ha recortado. Ayuda a consultar el cuadro de límite del modelo mediante programación y a visualizar el cuadro con Unity como un cuadro de línea o imprimir sus valores en el registro de depuración.

Además, el proceso de conversión genera un [archivo JSON de salida](../how-tos/conversion/get-information.md) junto con el modelo convertido. Para depurar los problemas de posicionamiento de modelos, vale la pena examinar la entrada `boundingBox` de la sección [outputStatistics](../how-tos/conversion/get-information.md#the-outputstatistics-section):

```JSON
{
    ...
    "outputStatistics": {
        ...
        "boundingBox": {
            "min": [
                -43.52,
                -61.775,
                -79.6416
            ],
            "max": [
                43.52,
                61.775,
                79.6416
            ]
        }
    }
}
```

El cuadro de límite se describe como una posición `min` y `max` en el espacio 3D, en metros. Por lo tanto, una coordenada de 1000,0 significa que está a 1 kilómetro del origen.

Puede haber dos problemas con este cuadro de límite que den lugar a una geometría invisible:
* **El cuadro puede estar muy alejado del centro**, de modo que el objeto se recorte por completo debido al recorte del plano lejano. En este caso, los valores `boundingBox` tendrían el siguiente aspecto: `min = [-2000, -5,-5], max = [-1990, 5,5]`, con un gran desplazamiento en el eje x como ejemplo aquí. Para resolver este tipo de problema, habilite la opción `recenterToOrigin` en [Configuración de la conversión de modelos](../how-tos/conversion/configure-model-conversion.md).
* **El cuadro puede centrarse, pero los órdenes de magnitud ser demasiado grandes**. Esto significa que, aunque la cámara se inicie en el centro del modelo, su geometría se recorta en todas las direcciones. En este caso, los valores de `boundingBox` típicos tendrían el siguiente aspecto: `min = [-1000,-1000,-1000], max = [1000,1000,1000]`. El motivo de este tipo de problema suele ser una discrepancia en la escala de unidades. Para compensarla, especifique un [valor de escalado durante la conversión](../how-tos/conversion/configure-model-conversion.md#geometry-parameters) o marque el modelo de origen con las unidades correctas. El escalado también se puede aplicar al nodo raíz al cargar el modelo en tiempo de ejecución.

**La canalización de representación de Unity no incluye los enlaces de representación:**

Azure Remote Rendering se enlaza a la canalización de representación de Unity para realizar la composición de fotogramas con el vídeo y para volver a proyectarla. Para comprobar que los enlaces existen, abra el menú *Ventana > Análisis > Frame Debugger*. Habilite esta opción y asegúrese de que existen dos entradas de `HolographicRemotingCallbackPass` en la canalización:

![Unity Frame Debugger](./media/troubleshoot-unity-pipeline.png)

## <a name="unity-code-using-the-remote-rendering-api-doesnt-compile"></a>El código de Unity que usa la API de Remote Rendering no se compila

Cambie el *tipo de compilación* de la solución Unity a **Depuración**. Al probar ARR en el editor de Unity, el objeto `UNITY_EDITOR` de definición solo está disponible en las compilaciones de tipo "Depuración". Tenga en cuenta que esto no está relacionado con el tipo de compilación usado para las [aplicaciones implementadas](../quickstarts/deploy-to-hololens.md), donde debe preferirá las compilaciones de tipo "Versión".

## <a name="unstable-holograms"></a>Hologramas inestables

En caso de que parezca que los objetos representados se mueven con movimientos de cabeza, es posible que experimente problemas de *reproyección de fases con demora* (LSR). Consulte la sección sobre la [reproyección de fases con demora](../overview/features/late-stage-reprojection.md) para obtener instrucciones sobre cómo enfocar esta situación.

Otra causa de los hologramas inestables (hologramas con tambaleo, deformación, vibración o saltos) puede ser una conectividad de red deficiente, en particular, un ancho de banda de red insuficiente o una latencia demasiado alta. Un buen indicador de la calidad de la conexión de red es el valor de [estadísticas de rendimiento](../overview/features/performance-queries.md)`ARRServiceStats.VideoFramesReused`. Los fotogramas reutilizados indican situaciones en las que un fotograma de vídeo antiguo necesitaba reutilizarse en el lado cliente porque no había ningún nuevo fotograma de vídeo disponible (por ejemplo, debido a la pérdida de paquetes o a variaciones en la latencia de red). Si `ARRServiceStats.VideoFramesReused` suele ser mayor que cero, significa que hay un problema de red.

Otro valor que se debe examinar es `ARRServiceStats.LatencyPoseToReceiveAvg`. Debe estar siempre por debajo de 100 ms. Si ve valores más altos, significa que está conectado a un centro de datos que está demasiado lejos.

Para obtener una lista de posibles mitigaciones, consulte las [instrucciones sobre la conectividad de red](../reference/network-requirements.md#guidelines-for-network-connectivity).

## <a name="next-steps"></a>Pasos siguientes

* [Requisitos del sistema](../overview/system-requirements.md)
* [Requisitos de red](../reference/network-requirements.md)
