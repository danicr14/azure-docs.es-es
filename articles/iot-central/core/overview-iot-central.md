---
title: Introducción a Azure IoT Central | Microsoft Docs
description: Azure IoT Central es una plataforma de aplicaciones de IoT que simplifica la creación de soluciones de IoT y ayuda a reducir la carga y el costo de las operaciones de administración de IoT y el desarrollo. En este artículo se proporciona información general sobre las características de Azure IoT Central.
author: dominicbetts
ms.author: dobett
ms.date: 12/10/2019
ms.topic: overview
ms.service: iot-central
services: iot-central
ms.custom: mvc
ms.openlocfilehash: 05d73ae09d95879c37e86f5f3e73e35ed4607296
ms.sourcegitcommit: 856db17a4209927812bcbf30a66b14ee7c1ac777
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2020
ms.locfileid: "82560955"
---
# <a name="what-is-azure-iot-central"></a>¿Qué es Azure IoT Central?

IoT Central es una plataforma de aplicaciones de IoT que reduce la carga y el costo del desarrollo, la administración y el mantenimiento de soluciones de IoT de nivel empresarial. La elección de compilar con IoT Central ofrece la oportunidad de centrar el tiempo, el dinero y la energía en transformar su negocio con datos de IoT, en lugar de simplemente mantener y actualizar una infraestructura de IoT compleja y continuamente en constante evolución.

La interfaz de usuario web le permite supervisar las condiciones del dispositivo, crear reglas y administrar millones de dispositivos y sus datos a lo largo de su ciclo de vida. Además, le permite actuar sobre la información del dispositivo mediante la extensión de IoT Intelligence en aplicaciones de línea de negocio.

Para IoT Central, en este artículo se describe lo siguiente:

- Los roles típicos asociados a un proyecto.
- Cómo crear una aplicación.
- Cómo conectar los dispositivos a la aplicación.
- Cómo administrar una aplicación.
- Azure IoT Edge funcionalidades en IoT Central.
- Cómo conectar los dispositivos del entorno de ejecución de Azure IoT Edge a la aplicación.

## <a name="known-issues"></a>Problemas conocidos

- La exportación continua de datos no admite el formato Avro (incompatibilidad).
- GeoJSON no se admite actualmente.
- El icono del mapa no se admite actualmente.
- Los trabajos no admiten tipos complejos.
- No se admiten los tipos de esquema de matriz.
- Solo se admiten el SDK de dispositivos de C y los SDK de dispositivos y servicios de Node.js.
- IoT Central está disponible actualmente en ubicaciones de Estados Unidos, Europa, Asia Pacífico, Australia, Reino Unido y Japón.
- No puede usar la plantilla de aplicación **Aplicación personalizada (heredada)** en las ubicaciones de Reino Unido y Japón.
- Los modelos de funcionalidad del dispositivo deben tener todas las interfaces definidas insertadas en el mismo archivo.
- La compatibilidad con [IoT Plug and Play](../../iot-pnp/overview-iot-plug-and-play.md) se encuentra en versión preliminar y solo se admite en determinadas regiones.

## <a name="personas"></a>Personas

La documentación IoT Central hace referencia a cuatro personas que interactúan con una aplicación IoT Central:

- Un _generador de soluciones_ es responsable de definir los tipos de dispositivos que se conectan a la aplicación y de personalizar la aplicación para el operador.
- Un _operador_, que administra los dispositivos conectados a la aplicación.
- Un _administrador_ es responsable de las tareas administrativas, como la administración de [roles de usuario y permisos](howto-administer.md) dentro de la aplicación.
- Un _desarrollador de dispositivos_ crea el código que se ejecuta en un dispositivo o un módulo de IoT Edge conectado a la aplicación.

## <a name="create-your-iot-central-application"></a>Creación de la aplicación IoT Central

Como generador de soluciones, use IoT Central para crear una solución de IoT personalizada hospedada en la nube para su organización. Normalmente, una solución de personalizada IoT consta de:

- Una aplicación basada en la nube que recibe los datos de telemetría de los dispositivos y le permite administrar los dispositivos.
- Varios dispositivos que ejecutan código personalizado y que están conectados a la aplicación en la nube.

Puede implementar rápidamente una aplicación IoT Central nueva y, luego, personalizarla según sus requisitos específicos en el explorador. Puede empezar con una _plantilla de aplicación_ genérica o con una de las plantillas de aplicación específicas para los sectores [minorista](../retail/overview-iot-central-retail.md), [energético](../energy/overview-iot-central-energy.md), [gubernamental](../government/overview-iot-central-government.md) o [sanitario](../healthcare/overview-iot-central-healthcare.md).

Como generador de soluciones, se usan las herramientas web para crear una _plantilla de dispositivo_ para los dispositivos que se conectan a la aplicación. Una plantilla de dispositivo es el plano técnico que define las características y el comportamiento de un tipo de dispositivo, por ejemplo:

- La telemetría que envía.
- Las propiedades empresariales que un operador puede modificar.
- Las propiedades del dispositivo que se establecen mediante un dispositivo y que son de solo lectura en la aplicación.
- Propiedades, que un operador establece, que determinan el comportamiento del dispositivo.

Esta plantilla de dispositivo incluye:

- Un _modelo de funcionalidad del dispositivo_ que describe las funcionalidades que debe implementar un dispositivo, como los datos de telemetría que envía y las propiedades que notifica.
- Propiedades de la nube que no están almacenadas en el dispositivo.
- Personalizaciones, paneles y formularios que forman parte de la aplicación IoT Central.

### <a name="pricing"></a>Precios

Para crear aplicaciones de IoT Central se puede usar una evaluación gratuita de 7 días, o bien un plan de precios estándar.

- Las aplicaciones que se crean mediante el plan *gratuito* no tienen costo durante siete días y admiten un máximo de cinco dispositivos. En cualquier momento antes de que expiren puede convertirlas para que usen un plan de precios estándar.
- Las aplicaciones que se crean con un plan *estándar* se facturan por dispositivo y se pueden elegir el plan de precios **Estándar 1** o **Estándar 2** y los dos primeros dispositivos son gratis. Obtenga más información sobre los planes de precios gratuito y estándar en la [página de precios de Azure IoT Central](https://azure.microsoft.com/pricing/details/iot-central/).

### <a name="create-device-templates"></a>Creación de plantillas de dispositivo

[IoT Plug and Play (versión preliminar)](../../iot-pnp/overview-iot-plug-and-play.md) permite a IoT Central integrar dispositivos sin necesidad de escribir ningún código de dispositivo integrado. En el centro de IoT Plug and Play (versión preliminar) se encuentra un esquema del modelo de funcionalidad del dispositivo que describe las funcionalidades del dispositivo. En una aplicación de IoT Central, las plantillas de dispositivo usan estos modelos de funcionalidad del dispositivo de IoT Plug and Play (versión preliminar).

Como generador de soluciones, tiene varias opciones para crear plantillas de dispositivo:

- Importe un modelo de funcionalidad del dispositivo desde el [catálogo de dispositivos Azure Certified for IoT](https://aka.ms/iotdevcat) y, a continuación, agregue las propiedades, las personalizaciones y los paneles en la nube que necesite la aplicación de IoT Central.
- Diseñe la plantilla de dispositivo en IoT Central y, después, implemente el modelo de funcionalidad del dispositivo en el código del dispositivo.
- Cree un modelo de funcionalidad del dispositivo mediante Visual Studio Code y publique el modelo en un repositorio. Implemente el código del dispositivo desde el modelo y conecte el dispositivo a la aplicación de IoT Central. IoT Central encuentra el modelo de funcionalidad del dispositivo en el repositorio y crea automáticamente una plantilla de dispositivo simple.
- Cree un modelo de funcionalidad del dispositivo mediante Visual Studio Code. Implemente el código del dispositivo a partir del modelo. Importe manualmente el modelo de funcionalidad del dispositivo en la aplicación de IoT Central y, a continuación, agregue las propiedades, las personalizaciones y los paneles en la nube que necesite la aplicación de IoT Central.

Como generador de soluciones, puede usar IoT Central para generar código para que los dispositivos de prueba validen las plantillas de dispositivo.

### <a name="customize-the-ui"></a>Personalización de la interfaz de usuario

Como generador de soluciones, también puede personalizar la interfaz de usuario de la aplicación IoT Central para los operadores responsables del uso cotidiano de la aplicación. Entre las personalizaciones que puede crear un generador de soluciones se incluyen:

- Definir el diseño de las propiedades y la configuración en una plantilla de dispositivo.
- Configurar paneles personalizados para ayudar a los operadores a descubrir información y resolver los problemas con mayor rapidez.
- Configurar análisis personalizados para explorar los datos de series temporales de los dispositivos conectados.

## <a name="pricing"></a>Precios

Para crear aplicaciones de IoT Central se puede usar una evaluación gratuita de 7 días, o bien un plan de precios estándar.

- Las aplicaciones que se crean mediante el plan *gratuito* no tienen costo durante siete días y admiten un máximo de cinco dispositivos. En cualquier momento antes de que expiren puede convertirlas para que usen un plan de precios estándar.
- Las aplicaciones que se crean con un plan *estándar* se facturan por dispositivo y se puede elegir el plan de precios **Estándar 1** o **Estándar 2**, y los dos primeros dispositivos son gratis. Más información sobre los [precios de IoT Central](https://aka.ms/iotcentral-pricing).

## <a name="connect-your-devices"></a>Conectar dispositivos

Azure IoT Central usa Azure [IoT Device Provisioning Service (DPS)](../../iot-dps/about-iot-dps.md) para administrar el registro y la conexión de todos los dispositivos.

El uso de DPS permite:

- Que IoT Central admite la incorporación y la conexión de dispositivos a escala.
- Que usted pueda generar credenciales de dispositivo y configurar los dispositivos sin conexión sin tener que registrarlos primero en la interfaz de usuario de IoT Central.
- Que los dispositivos se conecten mediante firmas de acceso compartido.
- Que los dispositivos se conecten con los certificados X.509 estándar del sector.
- Que usted pueda usar identificadores de dispositivo propios para registrar estos en IoT Central. Esto simplifica la integración con sistemas del área de operaciones existentes.
- Una manera sencilla y coherente de conectar dispositivos a IoT Central.

Para más información, consulte [Conexión a Azure IoT Central](./concepts-get-connected.md).

### <a name="azure-iot-edge-devices"></a>Dispositivos de Azure IoT Edge

Además de los dispositivos creados con el [SDK de IoT de Azure](https://github.com/Azure/azure-iot-sdks), también puede conectar [dispositivos Azure IoT Edge](../../iot-edge/about-iot-edge.md) a una aplicación IoT Central. Azure IoT Edge permite ejecutar la inteligencia de nube y la lógica personalizada directamente en dispositivos IoT administrados por IoT Central. El tiempo de ejecución de IoT Edge permite:

- Instalación y actualización de las cargas de trabajo en el dispositivo.
- Mantenimiento de los estándares de seguridad de Azure IoT Edge en el dispositivo.
- Garantía de que los módulos de IoT Edge están siempre en ejecución.
- Notificación del mantenimiento del módulo a la nube para la supervisión remota.
- Administración de la comunicación entre los dispositivos hoja descendentes y un dispositivo IoT Edge, entre los módulos de un dispositivo IoT Edge y entre un dispositivo IoT Edge y la nube.

Para más información, consulte [dispositivos Azure IoT Edge e IoT Central](concepts-architecture.md#azure-iot-edge-devices).

## <a name="stay-connected"></a>Mantenimiento de la conexión

Las aplicaciones IoT Central están totalmente hospedadas por Microsoft, lo que reduce la sobrecarga de administración que suponen las aplicaciones.

Como operador, se usa la aplicación IoT Central para administrar los dispositivos de la solución de IoT Central. Los operadores realizan tareas como:

- Supervisar los dispositivos conectados a la aplicación.
- Solucionar problemas y errores de los dispositivos.
- Aprovisionar dispositivos nuevos.

Como generador de soluciones, puede definir reglas y acciones personalizadas que funcionan a través de la transmisión de datos desde dispositivos conectados. Un operador puede habilitar o deshabilitar estas reglas en el nivel de dispositivo para controlar y automatizar las tareas dentro de la aplicación.

Los administradores administran el acceso a la aplicación con [permisos y roles de usuario](howto-administer.md).

Con cualquier solución de IoT diseñada para funcionar a escala es importante tener un enfoque estructurado en relación con la administración de dispositivos. No basta con conectar los dispositivos a la nube, sino que es necesario mantener los dispositivos conectados y en buen estado. Un operador puede usar las siguientes funcionalidades de IoT Central para administrar los dispositivos a lo largo del ciclo de vida de la aplicación:

### <a name="dashboards"></a>Paneles 

Los [paneles](./howto-set-up-template.md#generate-default-views) integrados proporcionan una interfaz de usuario personalizable para supervisar tanto el estado como los datos de telemetría de los dispositivos. Comience con un panel pregenerado en una [plantilla de aplicación](howto-use-app-templates.md), o bien cree sus propios paneles adaptados a las necesidades de sus operadores. Puede compartir los paneles con todos los usuarios de la aplicación, o bien mantenerlos privados.

### <a name="rules-and-actions"></a>Reglas y acciones

Cree [reglas personalizadas](tutorial-create-telemetry-rules.md) basadas en el estado y la telemetría de los dispositivos, con el fin de identificar aquellos que necesitan atención. Configure acciones para notificar a las personas adecuadas y asegúrese de que se aplican medidas correctivas en el momento oportuno.

### <a name="jobs"></a>Trabajos

Los [trabajos](howto-run-a-job.md) permiten aplicar actualizaciones individuales o en masa a los dispositivos, para lo que se establecen propiedades o se realizan llamadas a comandos. 

### <a name="user-roles-and-permissions"></a>Roles y permisos de usuario

Los [roles y permisos](howto-manage-users-roles.md) permiten a los administradores adaptar la experiencia de cada usuario. Los administradores usan la interfaz de usuario web para crear roles y asignar permisos.

## <a name="transform-your-iot-data"></a>Transformación de los datos de IoT

Como plataforma de aplicaciones, IoT Central permite transformar los datos de IoT en información empresarial que produce resultados útiles. Las [reglas](./tutorial-create-telemetry-rules.md), la [exportación de datos](./howto-export-data.md) y la [API REST pública](https://docs.microsoft.com/learn/modules/manage-iot-central-apps-with-rest-api/) son ejemplos de integración de IoT Central con aplicaciones de línea de negocio:

![Transformación de datos de IoT mediante IoT Central](media/overview-iot-central/transform.png)

### <a name="monitor-device-health-and-operations-using-rules"></a>Supervisión del estado de los dispositivos y las operaciones mediante reglas

Mientras los dispositivos estén conectados y envíen datos, las reglas pueden identificar aquellos dispositivos que tienen problemas o enviar mensajes de error, con el fin de que se puedan solucionar con un tiempo de inactividad mínimo. Cree en la aplicación IoT Central reglas que supervisen los datos de telemetría de los dispositivos y que avisen a algún operador cuando una métrica supere un umbral o un dispositivo envíe un mensaje concreto. Las acciones del correo electrónico y los webhooks de sus reglas envían notificaciones tanto a las personas como a los sistemas de bajada correctos.

### <a name="run-custom-analytics-and-processing-on-your-exported-data"></a>Ejecución de análisis y procesamiento personalizados en los datos exportados

Puede generar información empresarial, como determinar las tendencias de eficiencia de la máquina o predecir el uso futuro de la energía en una fábrica, mediante la creación de canalizaciones de análisis personalizadas para procesar los datos de telemetría de los dispositivos y almacenar el resultado. Configure las exportaciones de datos en la aplicación de IoT Central para exportar datos de telemetría, cambios de propiedades de los dispositivos y cambios de las plantillas de dispositivos a otros servicios en los que puede analizar, almacenar y visualizar los datos con sus herramientas preferidas.

### <a name="build-custom-iot-solutions-and-integrations-with-the-rest-apis"></a>Creación de soluciones de IoT personalizadas e integraciones con las API REST

Cree soluciones de IoT como:

- Aplicaciones de Mobile Companion que pueden configurar y controlar dispositivos de forma remota.
- Integraciones personalizadas que permiten a las aplicaciones de línea de negocio existentes interactuar con los datos y dispositivos de IoT.
- Aplicaciones de administración de dispositivos para el modelado de dispositivos, la incorporación, la administración y el acceso a los datos.

## <a name="quotas"></a>Cuotas

Cada suscripción de Azure tiene cuotas predeterminadas que pueden afectar al ámbito de la solución de IoT. Actualmente, IoT Central limita el número de aplicaciones que se pueden implementar en una suscripción a 10. Si quiere aumentar este límite, póngase en contacto con el [soporte técnico de Microsoft](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una visión general de IoT Central, estos son los siguientes pasos sugeridos:

- Conocer las [tecnologías y servicios de Azure disponibles para crear soluciones de IoT](../../iot-fundamentals/iot-services-and-technologies.md).
- Familiarizarse con la [interfaz de usuario de Azure IoT Central](overview-iot-central-tour.md).
- [Crear una aplicación de Azure IoT Central](quick-deploy-iot-central.md) para empezar a trabajar.
- Más información sobre [IoT Plug and Play (versión preliminar)](../../iot-pnp/overview-iot-plug-and-play.md).
- Más información sobre cómo [conectar un dispositivo de Azure IoT Edge](./tutorial-add-edge-as-leaf-device.md).
- Más información sobre las [tecnologías y servicios de IoT de Azure](../../iot-fundamentals/iot-services-and-technologies.md).

Si es un desarrollador de dispositivos y desea profundizar en algún código, el paso siguiente que se sugiere se indica en [Creación y conexión de un aplicación cliente a una aplicación de Azure IoT Central](./tutorial-connect-device-nodejs.md).
