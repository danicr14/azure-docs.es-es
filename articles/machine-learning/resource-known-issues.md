---
title: Problemas conocidos y soluciones
titleSuffix: Azure Machine Learning
description: Obtenga una lista de los problemas conocidos y soluciones para Azure Machine Learning.
services: machine-learning
author: j-martens
ms.author: jmartens
ms.reviewer: mldocs
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
ms.date: 03/31/2020
ms.openlocfilehash: 2db7a25f3f463e9210544354395c9d33a75f633c
ms.sourcegitcommit: bc738d2986f9d9601921baf9dded778853489b16
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2020
ms.locfileid: "80619369"
---
# <a name="known-issues-and-troubleshooting-azure-machine-learning"></a>Problemas conocidos y soluciones de Azure Machine Learning

Este artículo le ayuda a buscar y corregir los errores que se producen al usar Azure Machine Learning.

## <a name="diagnostic-logs"></a>Registros de diagnóstico

A veces puede resultar útil proporcionar información de diagnóstico al solicitar ayuda. Para ver algunos registros: 
1. Visite [Azure Machine Learning Studio](https://ml.azure.com). 
1. En el lado izquierdo, seleccione **Experimento**. 
1. Seleccione un experimento.
1. Seleccione una ejecución.
1. En la parte superior, seleccione **Resultados y registros**.

> [!NOTE]
> Azure Machine Learning registra información de varios orígenes durante el entrenamiento, como AutoML o el contenedor de Docker que ejecuta el trabajo de entrenamiento. Muchos de estos registros no están documentados. Si encuentra problemas y se pone en contacto con el Soporte técnico de Microsoft, es posible que puedan usar estos registros durante la resolución de problemas.


## <a name="resource-quotas"></a>Cuotas de recursos

Obtenga información sobre la [cuotas de recursos](how-to-manage-quotas.md) que puede encontrar al trabajar con Azure Machine Learning.

## <a name="installation-and-import"></a>Instalación e importación

* **Mensaje de error: no se puede desinstalar 'PyYAML'**

    SDK de Azure Machine Learning para Python: PyYAML es un proyecto instalado de `distutils`. Por lo tanto, no se puede determinar con precisión qué archivos le pertenecen en caso de una desinstalación parcial. Para continuar con la instalación del SDK sin tener en cuenta este error, use:
    
    ```Python
    pip install --upgrade azureml-sdk[notebooks,automl] --ignore-installed PyYAML
    ```

* **Error de Databricks al instalar los paquetes**

    No es posible instalar el SDK de Azure Machine Learning en Azure Databricks cuando se instalan más paquetes. Algunos paquetes, como `psutil`, pueden provocar conflictos. Para evitar errores de instalación, inmovilice la versión de la biblioteca para instalar los paquetes. Este problema está relacionado con Databricks y no con el SDK de Azure Machine Learning. También puede experimentar este problema con otras bibliotecas. Ejemplo:
    
    ```python
    psutil cryptography==1.5 pyopenssl==16.0.0 ipython==2.2.0
    ```

    Como alternativa, puede usar scripts de init si sigue experimentando problemas de instalación con las bibliotecas de Python. Este enfoque no se admite oficialmente. Para más información, consulte [Cluster-scoped init scripts](https://docs.azuredatabricks.net/user-guide/clusters/init-scripts.html#cluster-scoped-init-scripts) (Script de init del ámbito de clúster).

* **Error de importación de Databricks: no se puede importar el nombre "Timedelta" de "pandas._libs.tslibs"** : Si ve este error al usar el aprendizaje automático automatizado, ejecute las dos líneas siguientes en el cuaderno:
    ```
    %sh rm -rf /databricks/python/lib/python3.7/site-packages/pandas-0.23.4.dist-info /databricks/python/lib/python3.7/site-packages/pandas
    %sh /databricks/python/bin/pip install pandas==0.23.4
    ```

* **Error de importación de Databricks: No hay ningún módulo denominado "pandas.core.indexes"** : Si ve este error al usar el aprendizaje automático automatizado:

    1. Ejecute este comando para instalar dos paquetes en el clúster de Azure Databricks:
    
       ```bash
       scikit-learn==0.19.1
       pandas==0.22.0
       ```
    
    1. Desasocie y, luego, vuelva a conectar el clúster al cuaderno.
    
    Si estos pasos no resuelven el problema, pruebe a reiniciar el clúster.

* **FailToSendFeather de Databricks**: Si ve un error `FailToSendFeather` al leer datos en un clúster de Azure Databricks, consulte las soluciones siguientes:
    
    * Actualice el paquete `azureml-sdk[automl]` a la versión más reciente.
    * Agregue `azureml-dataprep` versión 1.1.8 o superior.
    * Agregue `pyarrow` versión 0.11 o superior.

## <a name="create-and-manage-workspaces"></a>Crear y administrar áreas de trabajo

> [!WARNING]
> No se admite mover el área de trabajo de Azure Machine Learning a otra suscripción ni mover la suscripción propietaria a un nuevo inquilino. Si lo hace, pueden producirse errores.

* **Portal de Azure**: si va directamente al área de trabajo desde un vínculo de recurso compartido desde el SDK o el portal, no podrá ver la página de **Información general** normal con la información de suscripción de la extensión. Tampoco será capaz de cambiar a otra área de trabajo. Si necesita ver otra área de trabajo, vaya directamente a [Azure Machine Learning Studio](https://ml.azure.com) y busque el nombre del área de trabajo.

## <a name="set-up-your-environment"></a>Configurar el entorno

* **Problemas al crear AmlCompute**: Es posible que algunos usuarios que crearon su área de trabajo de Azure Machine Learning en Azure Portal antes de la versión de disponibilidad general no puedan crear la instancia de AmlCompute en esa área de trabajo. Puede generar una solicitud de soporte técnico en el servicio o crear una nueva área de trabajo mediante el portal o el SDK para desbloquearse a sí mismo inmediatamente.

## <a name="work-with-data"></a>Trabajar con datos

### <a name="overloaded-azurefile-storage"></a>Almacenamiento AzureFile sobrecargado

Si recibe un error `Unable to upload project files to working directory in AzureFile because the storage is overloaded`, aplique las siguientes soluciones alternativas.

Si usa un recurso compartido de archivos para otras cargas de trabajo, como la transferencia de datos, se recomienda usar blobs para que el recurso compartido de archivos se pueda usar para el envío de ejecuciones. También puede dividir la carga de trabajo entre dos áreas de trabajo diferentes.

### <a name="passing-data-as-input"></a>Paso de datos como entrada

*  **TypeError: FileNotFound: no se encontró el archivo o directorio**: Este error se produce si la ruta de acceso al archivo que se proporcionó no es donde se encuentra el archivo. Debe asegurarse de que la forma en que hace referencia al archivo es coherente con la ubicación en la que montó el conjunto de archivos en el destino de proceso. Para garantizar un estado determinista, se recomienda usar la ruta de acceso abstracta al montar un conjunto de datos en un destino de proceso. Por ejemplo, en el código siguiente se monta el conjunto de datos en la raíz del sistema de archivos del destino de proceso, `/tmp`. 
    
    ```python
    # Note the leading / in '/tmp/dataset'
    script_params = {
        '--data-folder': dset.as_named_input('dogscats_train').as_mount('/tmp/dataset'),
    } 
    ```

    Si no incluye la barra diagonal inicial ("/"), tendrá que prefijar el directorio de trabajo (por ejemplo, `/mnt/batch/.../tmp/dataset`) en el destino de proceso para indicar dónde quiere que se monte el conjunto de datos.

### <a name="data-labeling-projects"></a>Proyecto de etiquetado de datos

|Problema  |Solución  |
|---------|---------|
|Solo se pueden usar los conjuntos de datos creados en almacenes de datos de blobs     |  Esta es una limitación conocida de la versión actual.       |
|Después de la creación, el proyecto muestra el mensaje "Initializing" (Inicializando) durante mucho tiempo     | Actualice manualmente la página. La inicialización debería continuar aproximadamente en 20 puntos de datos por segundo. La falta de actualización automática es un problema conocido.         |
|Al revisar imágenes, no se muestran las imágenes recién etiquetadas     |   Para cargar todas las imágenes etiquetadas, elija el botón **Primera**. El botón **Primera** le llevará al principio de la lista, pero carga todos los datos etiquetados.      |
|Al presionar la tecla ESC mientras se etiqueta para la detección de objetos, se crea una etiqueta de tamaño cero en la esquina superior izquierda. El envío de etiquetas en este estado produce un error.     |   Haga clic en la cruz junto a la etiqueta para eliminarla.  |

## <a name="azure-machine-learning-designer"></a>Diseñador de Azure Machine Learning

Problemas conocidos:

* **Tiempo prolongado de preparación de un proceso**: puede tardar unos minutos o incluso más tiempo en conectarse por primera vez a un destino de proceso o en crear uno. 

## <a name="train-models"></a>Entrenamiento de modelos

* **ModuleErrors (ningún módulo con nombre)** :  Si está ejecutando ModuleErrors mientras envía experimentos en Azure ML, significa que el script de entrenamiento espera que se instale un paquete pero no se agrega. Una vez que proporcione el nombre del paquete, Azure ML instalará el paquete en el entorno que se usa para la ejecución de su entrenamiento. 

    Si usa [Estimadores](concept-azure-machine-learning-architecture.md#estimators) para enviar experimentos, puede especificar un nombre de paquete mediante el parámetro `pip_packages` o `conda_packages` en el estimador basado en el origen desde el que desea instalar el paquete. También puede especificar un archivo yml con todas sus dependencias mediante `conda_dependencies_file` o enumerar todos sus requisitos de pip en un archivo txt con el parámetro `pip_requirements_file`. Si tiene su propio objeto de entorno de Azure ML para invalidar la imagen predeterminada que usa el estimador, puede especificar ese entorno a través del parámetro `environment` del constructor del estimador.

    Azure ML también proporciona estimadores específicos del marco para Tensorflow, PyTorch, Chainer y SKLearn. El uso de estos estimadores asegurará que las principales dependencias del marco se instalen en su nombre en el entorno utilizado para el entrenamiento. Tiene la opción de especificar dependencias adicionales como se describe anteriormente. 
 
    Azure ML mantuvo las imágenes acopladas y su contenido se puede ver en [Contenedores AzureML](https://github.com/Azure/AzureML-Containers).
    Las dependencias específicas del marco se enumeran en la documentación del marco respectivo: [Chainer](https://docs.microsoft.com/python/api/azureml-train-core/azureml.train.dnn.chainer?view=azure-ml-py#remarks), [PyTorch](https://docs.microsoft.com/python/api/azureml-train-core/azureml.train.dnn.pytorch?view=azure-ml-py#remarks), [TensorFlow](https://docs.microsoft.com/python/api/azureml-train-core/azureml.train.dnn.tensorflow?view=azure-ml-py#remarks), [SKLearn](https://docs.microsoft.com/python/api/azureml-train-core/azureml.train.sklearn.sklearn?view=azure-ml-py#remarks).

    > [!Note]
    > Si cree que un paquete en particular es lo suficientemente común como para agregarlo en imágenes y entornos mantenidos por Azure ML, cree una incidencia de GitHub en [Contenedores de AzureML](https://github.com/Azure/AzureML-Containers). 
 
* **NameError (Nombre no definido), AttributeError (El objeto no tiene ningún atributo)** : Esta excepción debería provenir de sus scripts de entrenamiento. Puede consultar los archivos de registro de Azure Portal para obtener más información sobre el nombre específico no definido o el error de atributo. Desde el SDK, puede usar `run.get_details()` para ver el mensaje de error. Esto también mostrará una lista de todos los archivos de registro generados para su ejecución. Asegúrese de revisar su script de entrenamiento y corrija el error antes de volver a enviar la ejecución. 

* **Horovod se apagó**: En la mayoría de los casos, si se muestra "AbortedError: Horovod has been shut down" (AbortedError: Horovod se cerró), esta excepción significa que hubo una excepción subyacente en uno de los procesos, y esto causó el apagado de Horovod. Cada clasificación en el trabajo MPI obtiene su propio archivo de registro dedicado en Azure ML. Estos registros son nombrados `70_driver_logs`. En caso de entrenamiento distribuido, los nombres de registro tienen el sufijo `_rank` para facilitar la diferenciación de los registros. Para encontrar el error exacto que provocó el apagado de Horovod, revise todos los archivos de registro y busque `Traceback` al final de los archivos driver_log. Uno de estos archivos le dará la excepción subyacente real. 

* **Eliminación de ejecuciones o experimentos**:  Los experimentos se pueden archivar con el método [Experiment.archive](https://docs.microsoft.com/python/api/azureml-core/azureml.core.experiment(class)?view=azure-ml-py#archive--) o desde la vista de la pestaña Experimento en el cliente de Azure Machine Learning Studio a través del botón "Archive experiment" (Archivar experimento). Esta acción oculta el experimento de listas de consultas y vistas, pero no lo elimina.

    Actualmente no se admite la eliminación permanente de experimentos ni ejecuciones individuales. Para obtener más información sobre cómo eliminar recursos del área de trabajo, consulte [Exportación o eliminación de los datos del área de trabajo de Machine Learning Service](how-to-export-delete-data.md).

* **El documento de métricas es demasiado grande**: Azure Machine Learning tiene límites internos en cuanto al tamaño de los objetos de métricas que se pueden registrar a la vez desde una ejecución de entrenamiento. Si aparece el error "El documento de métricas es demasiado grande" al registrar una métrica con valores de lista, intente dividir la lista en fragmentos más pequeños, por ejemplo:

    ```python
    run.log_list("my metric name", my_metric[:N])
    run.log_list("my metric name", my_metric[N:])
    ```

    De forma interna, Azure ML concatena los bloques con el mismo nombre de métrica en una lista contigua.

## <a name="automated-machine-learning"></a>Automated Machine Learning

* **Tensor Flow**: el aprendizaje automático automatizado no admite actualmente la versión 1.13 de Tensor Flow. Instalar esta versión hará que las dependencias del paquete dejen de funcionar. Estamos trabajando para corregir este problema en una versión futura.

* **Gráficos de experimento**: Los gráficos de clasificación binaria (precisión-retirada, ROC, curva de ganancia, etc.) que se muestran en las iteraciones de experimentos de ML automatizados no se representan correctamente en la interfaz de usuario desde el 12/04. Los trazados de los gráficos actualmente muestran resultados inversos, donde los modelos con mejor rendimiento se muestran con resultados inferiores. Se está investigando una resolución.

* **Cancelación de Databricks de una ejecución de aprendizaje automático automatizado**: Al usar las funcionalidades de aprendizaje automático automatizado en Azure Databricks, para cancelar una ejecución e iniciar una nueva ejecución de un experimento, reinicie el clúster de Azure Databricks.

* **> 10 iteraciones de Databricks para aprendizaje automático automatizado**: En la configuración del aprendizaje automático automatizado, si tiene más de 10 iteraciones, establezca `show_output` en `False` cuando envíe la ejecución.

* **Widget de Databricks para el SDK de Azure Machine Learning y aprendizaje automático automatizado**: El widget del SDK de Azure Machine Learning no se admite en un cuaderno de Databricks porque los cuadernos no pueden analizar los widgets HTML. Para ver el widget en el portal, use este código de Python en la celda del cuaderno de Azure Databricks:

    ```
    displayHTML("<a href={} target='_blank'>Azure Portal: {}</a>".format(local_run.get_portal_url(), local_run.id))
    ```

## <a name="deploy--serve-models"></a>Implementación y servicio de modelos

Realice estas acciones para los siguientes errores:

|Error  | Solución  |
|---------|---------|
|Error de creación de imágenes al implementar el servicio web     |  Agregar "pynacl==1.2.1" como una dependencia pip al archivo de Conda para la configuración de la imagen.       |
|`['DaskOnBatch:context_managers.DaskOnBatch', 'setup.py']' died with <Signals.SIGKILL: 9>`     |   Cambie la SKU de las máquinas virtuales usadas en la implementación por otra que tenga más memoria. |
|Error de FPGA     |  No podrá implementar modelos en FPGA hasta que haya solicitado y se haya aprobado para la cuota FPGA. Para solicitar acceso, rellene el formulario de solicitud de cuota: https://aka.ms/aml-real-time-ai       |

### <a name="updating-azure-machine-learning-components-in-aks-cluster"></a>Actualización de componentes de Azure Machine Learning en el clúster de AKS

Las actualizaciones a componentes de Azure Machine Learning instalados en un clúster de Azure Kubernetes Service se deben aplicar manualmente. 

Para aplicar estas actualizaciones, puede desconectar el clúster del área de trabajo de Azure Machine Learning y, luego, volver a conectarlo al área de trabajo. Si TLS está habilitado en el clúster, tendrá que proporcionar el certificado TLS/SSL y la clave privada al volver a asociar el clúster. 

```python
compute_target = ComputeTarget(workspace=ws, name=clusterWorkspaceName)
compute_target.detach()
compute_target.wait_for_completion(show_output=True)

attach_config = AksCompute.attach_configuration(resource_group=resourceGroup, cluster_name=kubernetesClusterName)

## If SSL is enabled.
attach_config.enable_ssl(
    ssl_cert_pem_file="cert.pem",
    ssl_key_pem_file="key.pem",
    ssl_cname=sslCname)

attach_config.validate_configuration()

compute_target = ComputeTarget.attach(workspace=ws, name=args.clusterWorkspaceName, attach_configuration=attach_config)
compute_target.wait_for_completion(show_output=True)
```

Si ya no tiene el certificado TLS/SSL y la clave privada, o si usa un certificado generado por Azure Machine Learning, puede recuperar los archivos antes de desasociar el clúster si se conecta al clúster mediante `kubectl` y recupera el secreto `azuremlfessl`.

```bash
kubectl get secret/azuremlfessl -o yaml
```

>[!Note]
>Kubernetes almacena los secretos en formato codificado en base-64. Deberá decodificar en base-64 los componentes `cert.pem` y `key.pem` de los secretos antes de proporcionarlos a `attach_config.enable_ssl`. 

### <a name="webservices-in-azure-kubernetes-service-failures"></a>Servicios web en errores de Azure Kubernetes Service

Muchos errores de servicio web de Azure Kubernetes Service se pueden depurar mediante la conexión al clúster con `kubectl`. Puede obtener el archivo `kubeconfig.json` para un clúster de Azure Kubernetes Service mediante la ejecución de:

```azurecli-interactive
az aks get-credentials -g <rg> -n <aks cluster name>
```

## <a name="authentication-errors"></a>Errores de autenticación

Si realiza una operación de administración en un destino de proceso desde un trabajo remoto, recibirá uno de los siguientes errores:

```json
{"code":"Unauthorized","statusCode":401,"message":"Unauthorized","details":[{"code":"InvalidOrExpiredToken","message":"The request token was either invalid or expired. Please try again with a valid token."}]}
```

```json
{"error":{"code":"AuthenticationFailed","message":"Authentication failed."}}
```

Por ejemplo, si intenta crear o asociar un destino de proceso desde una canalización de aprendizaje automático que se envía para ejecución remota, recibirá un error.
