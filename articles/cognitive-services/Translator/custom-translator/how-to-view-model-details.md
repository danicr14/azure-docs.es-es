---
title: 'Ver los detalles del modelo: Custom Translator'
titleSuffix: Azure Cognitive Services
description: La pestaña de modelos en todos los proyectos muestra los detalles de cada modelo, como el nombre, estado, puntuación BLEU y el recuento de oraciones de aprendizaje, ajuste y pruebas.
author: swmachan
manager: nitinme
ms.service: cognitive-services
ms.subservice: translator-text
ms.date: 02/21/2019
ms.author: swmachan
ms.topic: conceptual
ms.openlocfilehash: 64f446c3b331c1aa6ddaae9081b7f61943f74ab2
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2020
ms.locfileid: "68595566"
---
# <a name="view-model-details"></a>Ver detalles de los modelos

La pestaña de modelos en el proyecto muestra todos los modelos del proyecto. Todos los modelos entrenados para ese proyecto se muestran en esta pestaña.

Estos detalles se muestran para todos los modelos del proyecto.

1.  Nombre del modelo: muestra el nombre de un modelo determinado.

2.  Estado: muestra el estado de un modelo determinado. El nuevo entrenamiento tendrá el estado Enviado hasta que se acepte. El estado cambiará a Procesamiento de datos mientras el servicio evalúa el contenido de los documentos. Una vez completada la evaluación de los documentos, el estado cambiará a En ejecución y podrá consultar el número de oraciones que forman parte del entrenamiento, incluidos los conjuntos de ajuste y de pruebas que se crearon automáticamente. A continuación se muestra una lista de estados del modelo que describe dichos estados.

    -  Enviado: especifica que el back-end está procesando los documentos para ese modelo.

    -  TrainingQueued (Entrenamiento en cola): especifica que el entrenamiento se pondrá en la cola del sistema de traducción automática para ese modelo.

    -  En ejecución: especifica que el entrenamiento se está ejecutando en el sistema de traducción automática para ese modelo.

    -  Correcto: especifica que el entrenamiento se realizó correctamente en el sistema de traducción automática y que hay un modelo disponible. En este estado, se muestra una puntuación BLEU para ese modelo.

    -  Implementado: especifica que el modelo entrenado correctamente se envió al sistema de traducción automática para su implementación.

    -  Anulando implementación: especifica que se está anulando la implementación del modelo implementado.

    -  Implementación anulada: especifica que el proceso de anulación de la implementación de un modelo se ha completado correctamente.

    -  Training Failed (Error de entrenamiento): especifica que hubo un error en el entrenamiento. Si se produce un error de entrenamiento, vuelva a ejecutar el trabajo de entrenamiento. Si el error continúa, póngase en contacto con nosotros. No elimine el modelo con errores.

    - DataProcessingFailed (Error de procesamiento de datos): especifica que hubo un error en el procesamiento de datos para uno o varios documentos que pertenecen al modelo.

    - DeploymentFailed (Error de implementación): especifica que la implementación de modelos ha devuelto un error.

    - MigratedDraft (Borrador migrado): especifica que el modelo está en estado de borrador después de la migración del centro de conectividad a Custom Translator.

4.  Puntuación BLEU: muestra la puntuación BLEU (suplente de evaluación bilingüe) del modelo, que indica la calidad de su sistema de traducción. Esta puntuación le indica qué tanto se acercan las traducciones del sistema de traducción creado con este entrenamiento a las oraciones de referencia incluidas en el conjunto de datos de prueba. La puntuación BLEU aparece si se ha completado correctamente el entrenamiento. Si el entrenamiento no se completa o devuelve errores, no verá ninguna puntuación BLEU.

5.  Recuento de oraciones de aprendizaje: muestra el número total de oraciones que se usaron como conjunto de aprendizaje.

6.  Recuento de oraciones de ajuste: muestra el número total de oraciones que se usaron como conjunto de ajuste.

7.  Recuento de oraciones de pruebas: muestra el número total de oraciones que se usaron como conjunto de pruebas.

8.  Recuento de oraciones monolingües: muestra el número total de oraciones que se usaron como conjunto monolingüe.

9.  Botón de acción para implementar: para cada modelo entrenado correctamente, muestra un botón "Implementar" si aún no se implementa. Si el modelo se ha implementado, se muestra un botón "Anular la implementación".

10. Eliminar: puede usar este botón si desea eliminar el modelo. La eliminación de un modelo no elimina ninguno de los documentos que se utilizaron para crearlo.

    ![Ver detalles de los modelos](media/how-to/how-to-view-model-details.png)

>[!Note]
>Para comparar los entrenamientos consecutivos para los mismos sistemas, es importante mantener constantes los conjuntos de ajuste y de pruebas.

## <a name="view-model-training-details"></a>Ver detalles del entrenamiento de los modelos

Una vez completado el entrenamiento, puede revisar sus detalles desde la página de detalles. Seleccione un proyecto, busque y seleccione la pestaña de modelos y elija un modelo.

La página del modelo tiene dos pestañas: Detalles de entrenamiento y Prueba.

1.  **Detalles de entrenamiento:** en esta pestaña se muestra la lista de documentos que se usaron en el entrenamiento:

    -  Nombre de documentos: en este campo se muestra el nombre del documento

    -  Tipo de documento: en este campo se muestra si este documento es paralelo o monolingüe.

    -  Recuento de oraciones en el idioma de origen: en este campo se muestra el número de oraciones que forman parte del idioma de origen.

    -  Recuento de oraciones en el idioma de destino: en este campo se muestra el número de oraciones que forman parte del idioma de destino.

    -  Oraciones alineadas: en este campo se muestra el número de oraciones que Custom Translator ha alineado durante el proceso de alineación.

    -  Oraciones utilizadas: en este campo se muestra el número de oraciones que Custom Translator ha utilizado durante el entrenamiento.

    ![Detalles del entrenamiento de los modelos](media/how-to/how-to-model-training-details.png)

2.  **Prueba:** en esta pestaña se muestran los detalles de prueba para un entrenamiento realizado correctamente.

## <a name="next-steps"></a>Pasos siguientes

- Revise los [resultados de pruebas](how-to-view-system-test-results.md) y analice los resultados del entrenamiento.
