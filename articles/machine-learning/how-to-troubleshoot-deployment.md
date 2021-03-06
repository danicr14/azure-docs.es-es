---
title: Guía de solución de problemas de implementación
titleSuffix: Azure Machine Learning
description: Obtenga información sobre cómo abordar, solucionar y resolver los errores comunes de implementación de Docker con Azure Kubernetes Service y Azure Container Instances mediante Azure Machine Learning.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
author: clauren42
ms.author: clauren
ms.reviewer: jmartens
ms.date: 03/05/2020
ms.custom: seodec18
ms.openlocfilehash: fab46f7d7ae74ad643ce3f122b27b0dc767f5a78
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2020
ms.locfileid: "78399688"
---
# <a name="troubleshooting-azure-machine-learning-azure-kubernetes-service-and-azure-container-instances-deployment"></a>Solución de problemas con la implementación de Azure Machine Learning, Azure Kubernetes Service y Azure Container Instances

Obtenga información sobre cómo abordar, solucionar y resolver los errores comunes de implementación de Docker con Azure Container Instances (ACI) y Azure Kubernetes Service (AKS) mediante Azure Machine Learning.

Al implementar un modelo en Azure Machine Learning, el sistema realiza una serie de tareas.

El enfoque recomendado y más actualizado para la implementación de modelo se realiza a través de la API [Model.deploy()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.model%28class%29?view=azure-ml-py#deploy-workspace--name--models--inference-config-none--deployment-config-none--deployment-target-none--overwrite-false-) mediante un objeto [Entorno](https://docs.microsoft.com/azure/machine-learning/service/how-to-use-environments) como parámetro de entrada. En este caso, nuestro servicio creará una imagen de Docker base automáticamente durante la fase de implementación y montará los modelos necesarios en una llamada. Las tareas de implementación básicas son:

1. Registrar el modelo en el registro de modelos del área de trabajo.

2. Defina la configuración de inferencia:
    1. Cree un objeto [Entorno](https://docs.microsoft.com/azure/machine-learning/service/how-to-use-environments) basado en las dependencias que especifique en el archivo yaml de entorno o use uno de nuestros entornos adquiridos.
    2. Cree una configuración de inferencia (objeto InferenceConfig) basada en el entorno y el script de puntuación.

3. Implemente el modelo en el servicio de instancia de contenedor de Azure (ACI) o Azure Kubernetes Service (AKS).

Más información sobre este proceso en la introducción a la [administración de modelos](concept-model-management-and-deployment.md).

## <a name="prerequisites"></a>Prerrequisitos

* Una **suscripción de Azure**. Si no tiene una ya, pruebe la [versión gratuita o de pago de Azure Machine Learning](https://aka.ms/AMLFree).
* El [SDK de Azure Machine Learning](https://docs.microsoft.com/python/api/overview/azure/ml/install?view=azure-ml-py).
* La[CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).
* La [extensión de la CLI para Azure Machine Learning](reference-azure-machine-learning-cli.md).
* Para depurar localmente, debe tener una instalación de Docker en funcionamiento en el sistema local.

    Para comprobar la instalación de Docker, use el comando `docker run hello-world` desde un símbolo del sistema o terminal. Para obtener información sobre la instalación de Docker o la solución de problemas de Docker, consulte la [Documentación de Docker](https://docs.docker.com/).

## <a name="before-you-begin"></a>Antes de empezar

Si tiene algún problema, lo primero es dividir la tarea de implementación (descrita anteriormente) en pasos individuales para aislar el problema.

Suponiendo que esté usando el método de implementación nuevo o recomendado a través de la API [Model.deploy()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.model%28class%29?view=azure-ml-py#deploy-workspace--name--models--inference-config-none--deployment-config-none--deployment-target-none--overwrite-false-) con un objeto [Entorno](https://docs.microsoft.com/azure/machine-learning/service/how-to-use-environments) como parámetro de entrada, su código puede dividirse en tres importantes pasos:

1. Registre el modelo. Este es un código de ejemplo:

    ```python
    from azureml.core.model import Model


    # register a model out of a run record
    model = best_run.register_model(model_name='my_best_model', model_path='outputs/my_model.pkl')

    # or, you can register a file or a folder of files as a model
    model = Model.register(model_path='my_model.pkl', model_name='my_best_model', workspace=ws)
    ```

2. Defina la configuración de inferencia para la implementación:

    ```python
    from azureml.core.model import InferenceConfig
    from azureml.core.environment import Environment


    # create inference configuration based on the requirements defined in the YAML
    myenv = Environment.from_conda_specification(name="myenv", file_path="myenv.yml")
    inference_config = InferenceConfig(entry_script="score.py", environment=myenv)
    ```

3. Implemente el modelo mediante la configuración de inferencia creada en el paso anterior:

    ```python
    from azureml.core.webservice import AciWebservice


    # deploy the model
    aci_config = AciWebservice.deploy_configuration(cpu_cores=1, memory_gb=1)
    aci_service = Model.deploy(workspace=ws,
                           name='my-service',
                           models=[model],
                           inference_config=inference_config,
                           deployment_config=aci_config)
    aci_service.wait_for_deployment(show_output=True)
    ```

Una vez que haya dividido el proceso de implementación en tareas individuales, se pueden observar algunos de los errores más comunes.

## <a name="debug-locally"></a>Depuración local

Si tiene problemas al implementar un modelo en ACI o AKS, intente implementarlo como un servicio web local. El uso de un servicio web local facilita la solución de problemas. Se descarga la imagen de Docker que contiene el modelo y se inicia en el sistema local.

> [!WARNING]
> No se admiten las implementaciones de servicios web locales en escenarios de producción.

Para implementar de forma local, modifique el código para usar `LocalWebservice.deploy_configuration()` con el fin de crear una configuración de implementación. Luego use `Model.deploy()` para implementar el servicio. En el ejemplo siguiente se implementa un modelo (incluido en la variable de modelo) como un servicio web local:

```python
from azureml.core.environment import Environment
from azureml.core.model import InferenceConfig, Model
from azureml.core.webservice import LocalWebservice


# Create inference configuration based on the environment definition and the entry script
myenv = Environment.from_conda_specification(name="env", file_path="myenv.yml")
inference_config = InferenceConfig(entry_script="score.py", environment=myenv)
# Create a local deployment, using port 8890 for the web service endpoint
deployment_config = LocalWebservice.deploy_configuration(port=8890)
# Deploy the service
service = Model.deploy(
    ws, "mymodel", [model], inference_config, deployment_config)
# Wait for the deployment to complete
service.wait_for_deployment(True)
# Display the port that the web service is available on
print(service.port)
```

Tenga en cuenta que si va a definir su propio YAML de especificación de Conda, debe enumerar azureml-defaults con la versión >= 1.0.45 como dependencia de PIP. Este paquete contiene la funcionalidad necesaria para hospedar el modelo como un servicio web.

En este punto, se puede trabajar con el servicio de forma habitual. Por ejemplo, en el código siguiente se muestra cómo enviar datos al servicio:

```python
import json

test_sample = json.dumps({'data': [
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
]})

test_sample = bytes(test_sample, encoding='utf8')

prediction = service.run(input_data=test_sample)
print(prediction)
```

Para obtener más información sobre cómo personalizar el entorno de Python, consulte el tema sobre la [creación y administración de entornos de entrenamiento e implementación](how-to-use-environments.md). 

### <a name="update-the-service"></a>Actualizar el servicio

Durante las pruebas locales, es posible que deba actualizar el archivo `score.py` para agregar un registro o intentar resolver los problemas que haya descubierto. Para recargar los cambios realizados en el archivo `score.py`, use `reload()`. Por ejemplo, el código siguiente recarga el script para el servicio y luego envía datos. Los datos se puntúan con el archivo `score.py` actualizado:

> [!IMPORTANT]
> El método `reload` solo está disponible para las implementaciones locales. Para obtener información sobre cómo actualizar una implementación en otro destino de proceso, consulte la sección de actualización de [Implementación de modelos](how-to-deploy-and-where.md#update).

```python
service.reload()
print(service.run(input_data=test_sample))
```

> [!NOTE]
> El script se recarga desde la ubicación que especifica el objeto `InferenceConfig` que usa el servicio.

Para cambiar el modelo, las dependencias de Conda o la configuración de implementación, use [update()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice%28class%29?view=azure-ml-py#update--args-). En el siguiente ejemplo se actualiza el modelo que usa el servicio:

```python
service.update([different_model], inference_config, deployment_config)
```

### <a name="delete-the-service"></a>Eliminación del servicio

Para eliminar el servicio, use [delete()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice%28class%29?view=azure-ml-py#delete--).

### <a name="inspect-the-docker-log"></a><a id="dockerlog"></a> Inspección del registro de Docker

Puede imprimir los mensajes detallados de registro del motor de Docker desde el objeto de servicio. Puede ver el registro para ACI, AKS y las implementaciones locales. En el ejemplo siguiente se muestra cómo imprimir los registros.

```python
# if you already have the service object handy
print(service.get_logs())

# if you only know the name of the service (note there might be multiple services with the same name but different version number)
print(ws.webservices['mysvc'].get_logs())
```

## <a name="service-launch-fails"></a>Error en el inicio del servicio

Después de que la imagen se haya compilado correctamente, el sistema intenta iniciar un contenedor con el uso de la configuración de implementación. Como parte del proceso de puesta en marcha del contenedor, el sistema invoca la función `init()` en el script de puntuación. Si hay excepciones no detectadas en la función `init()`, es posible que vea el error **CrashLoopBackOff** en el mensaje de error.

Use la información que aparece en la sección [Inspeccionar el registro de Docker](#dockerlog) para comprobar los registros.

## <a name="function-fails-get_model_path"></a>Error en la función: get_model_path()

A menudo, en la función `init()` en el script de puntuación, se llama a la función [Model.get_model_path()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.model.model?view=azure-ml-py#get-model-path-model-name--version-none---workspace-none-) para buscar un archivo de modelo o una carpeta de archivos de modelo en el contenedor. Si no se encuentra el archivo de modelo o la carpeta, se produce un error en la función. La manera más fácil de depurar este error es ejecutar el siguiente código de Python en el shell del contenedor:

```python
from azureml.core.model import Model
import logging
logging.basicConfig(level=logging.DEBUG)
print(Model.get_model_path(model_name='my-best-model'))
```

En este ejemplo se imprime la ruta de acceso local (relativa a `/var/azureml-app`) en el contenedor donde el script de puntuación espera encontrar el archivo de modelo o la carpeta. A continuación, puede comprobar si el archivo o la carpeta están realmente donde se espera que estén.

Establecer el nivel de registro en DEBUG puede provocar el registro de información adicional, que puede resultar útil para identificar el error.

## <a name="function-fails-runinput_data"></a>Error en la función: run(input_data)

Si el servicio se implementa correctamente, pero se bloquea al publicar datos en el punto de conexión de puntuación, puede agregar una instrucción de captura de errores en la función `run(input_data)` para que devuelva un mensaje de error detallado en su lugar. Por ejemplo:

```python
def run(input_data):
    try:
        data = json.loads(input_data)['data']
        data = np.array(data)
        result = model.predict(data)
        return json.dumps({"result": result.tolist()})
    except Exception as e:
        result = str(e)
        # return error message back to the client
        return json.dumps({"error": result})
```

**Nota**: La devolución de mensajes de error de la llamada `run(input_data)` se debe realizar solo con fines de depuración. Por motivos de seguridad, no debe devolver los mensajes de error de este modo en un entorno de producción.

## <a name="http-status-code-502"></a>Código de estado HTTP 502

Un código de estado 502 indica que el servicio ha producido una excepción o se ha bloqueado en el método `run()` del archivo score.py. Utilice la información de este artículo para depurar el archivo.

## <a name="http-status-code-503"></a>Código de estado HTTP 503

Las implementaciones de Azure Kubernetes Service admiten el escalado automático, que permite que las réplicas se agreguen para admitir una carga adicional. Sin embargo, el escalador automático está diseñado para controlar cambios **graduales** en la carga. Si recibe grandes picos en las solicitudes por segundo, los clientes pueden recibir un código de estado HTTP 503.

Hay dos cosas que ayudan a impedir los códigos de estado 503:

* Cambiar el nivel de uso en el que el escalado automático crea nuevas réplicas.
    
    De forma predeterminada, se establece el uso de destino de escalado automático en el 70 %, lo que significa que el servicio puede controlar los picos en las solicitudes por segundo (RPS) de hasta un 30 %. Puede ajustar el objetivo de uso mediante el establecimiento de `autoscale_target_utilization` en un valor inferior.

    > [!IMPORTANT]
    > Este cambio no hace que las réplicas se creen *más rápidamente*. En lugar de eso, se crean con un umbral de uso más bajo. En lugar de esperar a que el servicio se use en un 70 %, si se cambia el valor a un 30 %, las réplicas se crearán cuando se produzca este 30 % de uso.
    
    Si el servicio web ya usa el número máximo de réplicas actuales y siguen apareciendo los códigos de estado 503, aumente el valor de `autoscale_max_replicas` con el fin de aumentar el número máximo de réplicas.

* Cambie el número mínimo de réplicas. El aumento en el número mínimo de réplicas proporciona un grupo más grande para controlar los picos entrantes.

    Para aumentar el número mínimo de réplicas, establezca `autoscale_min_replicas` en un valor superior. Puede calcular las réplicas necesarias mediante el código siguiente, reemplazando los valores por valores específicos del proyecto:

    ```python
    from math import ceil
    # target requests per second
    targetRps = 20
    # time to process the request (in seconds)
    reqTime = 10
    # Maximum requests per container
    maxReqPerContainer = 1
    # target_utilization. 70% in this example
    targetUtilization = .7

    concurrentRequests = targetRps * reqTime / targetUtilization

    # Number of container replicas
    replicas = ceil(concurrentRequests / maxReqPerContainer)
    ```

    > [!NOTE]
    > Si recibe picos de solicitudes más grandes que el número mínimo nuevo de réplicas que se puede controlar, es posible que reciba códigos de estado 503 otra vez. Por ejemplo, a medida que el tráfico al servicio aumente, es posible que deba aumentar el número mínimo de réplicas.

Para obtener más información sobre cómo configurar `autoscale_target_utilization`, `autoscale_max_replicas`, y `autoscale_min_replicas`, vea la referencia de módulo [AksWebservice](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice.akswebservice?view=azure-ml-py).

## <a name="http-status-code-504"></a>Código de estado HTTP 504

Un código de estado 504 indica que la solicitud ha agotado el tiempo de espera. El tiempo de espera predeterminado es 1 minuto.

Puede aumentar el tiempo de espera o intentar acelerar el servicio modificando el archivo score.py para quitar llamadas innecesarias. Si estas acciones no solucionan el problema, use la información de este artículo para depurar el archivo score.py. El código puede estar en un estado bloqueado o en un bucle infinito.

## <a name="advanced-debugging"></a>Depuración avanzada

En algunos casos, es posible que tenga que depurar interactivamente el código de Python incluido en la implementación de modelo. Por ejemplo, si el script de entrada presenta errores y no se puede determinar el motivo mediante un registro adicional. Mediante el uso de Visual Studio Code y las Herramientas de Python para Visual Studio (PTVSD), se puede adjuntar al código que se ejecuta dentro del contenedor de Docker.

> [!IMPORTANT]
> Este método de depuración no funciona cuando se usa `Model.deploy()` y `LocalWebservice.deploy_configuration` para implementar un modelo de manera local. En su lugar, debe crear una imagen con el método [Model.package()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.model.model?view=azure-ml-py#package-workspace--models--inference-config-none--generate-dockerfile-false-).

Las implementaciones de servicios web locales requieren una instalación de Docker en funcionamiento en el sistema local. Para obtener más información sobre el uso de Docker, consulte la [Documentación de Docker](https://docs.docker.com/).

### <a name="configure-development-environment"></a>Configuración del entorno de desarrollo

1. Para instalar las Herramientas de Python para Visual Studio (PTVSD) en el entorno de desarrollo de VS Code local, use el comando siguiente:

    ```
    python -m pip install --upgrade ptvsd
    ```

    Para más información sobre cómo usar PTVSD con VS Code, consulte [Depuración remota](https://code.visualstudio.com/docs/python/debugging#_remote-debugging).

1. Para configurar VS Code para comunicarse con la imagen de Docker, cree una configuración de depuración nueva:

    1. En VS Code, seleccione el menú __Depurar__ y, luego, seleccione __Abrir configuraciones__. Se abre un archivo denominado __launch.json__.

    1. En el archivo __launch.json__, busque la línea que contiene `"configurations": [` e inserte el texto siguiente después de ella:

        ```json
        {
            "name": "Azure Machine Learning: Docker Debug",
            "type": "python",
            "request": "attach",
            "port": 5678,
            "host": "localhost",
            "pathMappings": [
                {
                    "localRoot": "${workspaceFolder}",
                    "remoteRoot": "/var/azureml-app"
                }
            ]
        }
        ```

        > [!IMPORTANT]
        > Si ya hay otras entradas en la sección de configuraciones, agregue una coma (,) después del código que insertó.

        Esta sección se adjunta al contenedor de Docker mediante el puerto 5678.

    1. Guarde el archivo __launch.json__.

### <a name="create-an-image-that-includes-ptvsd"></a>Creación de una imagen que incluye PTVSD

1. Modifique el entorno de conda para la implementación de manera que incluya PTVSD. En el ejemplo siguiente se muestra cómo se agrega con el parámetro `pip_packages`:

    ```python
    from azureml.core.conda_dependencies import CondaDependencies 


    # Usually a good idea to choose specific version numbers
    # so training is made on same packages as scoring
    myenv = CondaDependencies.create(conda_packages=['numpy==1.15.4',            
                                'scikit-learn==0.19.1', 'pandas==0.23.4'],
                                 pip_packages = ['azureml-defaults==1.0.45', 'ptvsd'])

    with open("myenv.yml","w") as f:
        f.write(myenv.serialize_to_string())
    ```

1. Para iniciar PTVSD y esperar una conexión cuando se inicia el servicio, agregue lo siguiente en la parte superior del archivo `score.py`:

    ```python
    import ptvsd
    # Allows other computers to attach to ptvsd on this IP address and port.
    ptvsd.enable_attach(address=('0.0.0.0', 5678), redirect_output = True)
    # Wait 30 seconds for a debugger to attach. If none attaches, the script continues as normal.
    ptvsd.wait_for_attach(timeout = 30)
    print("Debugger attached...")
    ```

1. Cree una imagen basada en la definición de entorno y extráigala en el Registro local. Durante la depuración, es posible que quiera hacer cambios en los archivos de la imagen sin tener que volver a crearla. Para instalar un editor de texto (vim) en la imagen de Docker, use las propiedades `Environment.docker.base_image` y `Environment.docker.base_dockerfile`:

    > [!NOTE]
    > En este ejemplo se da por supuesto que `ws` apunta al área de trabajo de Azure Machine Learning y que `model` es el modelo que se está implementando. El archivo `myenv.yml` contiene las dependencias de conda creadas en el paso 1.

    ```python
    from azureml.core.conda_dependencies import CondaDependencies
    from azureml.core.model import InferenceConfig
    from azureml.core.environment import Environment


    myenv = Environment.from_conda_specification(name="env", file_path="myenv.yml")
    myenv.docker.base_image = None
    myenv.docker.base_dockerfile = "FROM mcr.microsoft.com/azureml/base:intelmpi2018.3-ubuntu16.04\nRUN apt-get update && apt-get install vim -y"
    inference_config = InferenceConfig(entry_script="score.py", environment=myenv)
    package = Model.package(ws, [model], inference_config)
    package.wait_for_creation(show_output=True)  # Or show_output=False to hide the Docker build logs.
    package.pull()
    ```

    Una vez que se haya creado y descargado la imagen, la ruta de acceso de la misma (incluye el repositorio, el nombre y la etiqueta, que en este caso también es su resumen) se mostrará en un mensaje similar al siguiente:

    ```text
    Status: Downloaded newer image for myregistry.azurecr.io/package@sha256:<image-digest>
    ```

1. Para facilitar el trabajo con la imagen, use el comando siguiente para agregar una etiqueta. Reemplace `myimagepath` por el valor de la ubicación del paso anterior.

    ```bash
    docker tag myimagepath debug:1
    ```

    Para el resto de los pasos, puede hacer referencia a la imagen local como `debug:1` en lugar del valor de la ruta de acceso completa a la imagen.

### <a name="debug-the-service"></a>Depuración del servicio

> [!TIP]
> Si establece un tiempo de expiración para la conexión de PTVSD en el archivo `score.py`, debe conectar VS Code a la sesión de depuración antes de que se cumpla el tiempo de expiración. Inicie VS Code, abra la copia local de `score.py`, establezca un punto de interrupción y prepárelo antes de seguir los pasos de esta sección.
>
> Para más información sobre la depuración y el establecimiento de puntos de interrupción, consulte [Depuración](https://code.visualstudio.com/Docs/editor/debugging).

1. Para iniciar un contenedor de Docker con la imagen, use el comando siguiente:

    ```bash
    docker run --rm --name debug -p 8000:5001 -p 5678:5678 debug:1
    ```

1. Para adjuntar VS Code a PTVSD dentro del contenedor, abra VS Code y use la tecla F5 o seleccione __Depurar__. Cuando se le solicite, seleccione la configuración __Azure Machine Learning: Docker Debug__ (Azure Machine Learning Service: depuración de Docker). También puede seleccionar el icono de depuración en la barra lateral, la entrada __Azure Machine Learning: Docker Debug__ (Azure Machine Learning Service: depuración de Docker) en el menú desplegable Depurar y, luego, use la flecha verde para adjuntar el depurador.

    ![El icono de depuración, el botón de inicio de la depuración y el selector de configuración](./media/how-to-troubleshoot-deployment/start-debugging.png)

En este punto, VS Code se conecta a PTVSD dentro del contenedor de Docker y se detiene en el punto de interrupción que se estableció anteriormente. Ahora puede recorrer el código a medida que se ejecuta, ver variables, etc.

Para más información sobre cómo usar VS Code para implementar Python, consulte [Depurar el código de Python](https://docs.microsoft.com/visualstudio/python/debugging-python-in-visual-studio?view=vs-2019).

<a id="editfiles"></a>
### <a name="modify-the-container-files"></a>Modificación de los archivos de contenedor

Para hacer cambios en los archivos de la imagen, puede adjuntar el contenedor en ejecución y ejecutar un shell de Bash. Desde ahí, puede usar vim para editar los archivos:

1. Para conectarse al contenedor en ejecución e iniciar un shell de Bash en el contenedor, use este comando:

    ```bash
    docker exec -it debug /bin/bash
    ```

1. Para encontrar los archivos que usa el servicio, utilice el siguiente comando del shell de bash en el contenedor si el directorio predeterminado es diferente de `/var/azureml-app`:

    ```bash
    cd /var/azureml-app
    ```

    Desde aquí, puede usar vim para editar el archivo `score.py`. Para más información sobre el uso de vim, consulte el artículo sobre cómo [usar el editor Vim](https://www.tldp.org/LDP/intro-linux/html/sect_06_02.html).

1. Por lo general, los cambios realizados en un contenedor no se conservan. Para guardar los cambios que haga, use el comando siguiente antes de salir del shell que se inició en el paso anterior (es decir, en otro shell):

    ```bash
    docker commit debug debug:2
    ```

    Este comando crea una imagen denominada `debug:2` que contiene las ediciones.

    > [!TIP]
    > Deberá detener el contenedor actual y empezar a usar la versión nueva antes de que los cambios surtan efecto.

1. Asegúrese de mantener los cambios que haga en los archivos del contenedor sincronizados con los archivos locales que usa VS Code. De lo contrario, la experiencia del depurador no funcionará según lo esperado.

### <a name="stop-the-container"></a>Detención del contenedor

Para detener el contenedor, use el comando siguiente:

```bash
docker stop debug
```

## <a name="next-steps"></a>Pasos siguientes

Más información acerca de la implementación:

* [Cómo implementar y dónde](how-to-deploy-and-where.md)
* [Tutorial: Entrenamiento e implementación de modelos](tutorial-train-models-with-aml.md)
