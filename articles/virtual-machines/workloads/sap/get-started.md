---
title: Introducción a SAP en máquinas virtuales de Azure | Microsoft Docs
description: Información sobre las soluciones SAP que se ejecutan en máquinas virtuales (VM) en Microsoft Azure
services: virtual-machines-linux
documentationcenter: ''
author: msjuergent
manager: bburns
editor: ''
tags: azure-resource-manager
keywords: ''
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/10/2020
ms.author: juergent
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: be403815838233350929c7d4ca0eed979d7dfa8c
ms.sourcegitcommit: 72c2da0def8aa7ebe0691612a89bb70cd0c5a436
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/10/2020
ms.locfileid: "79080332"
---
# <a name="use-azure-to-host-and-run-sap-workload-scenarios"></a>Uso de Azure para hospedar y ejecutar escenarios de carga de trabajo de SAP

Cuando utiliza Microsoft Azure, puede ejecutar de forma confiable los escenarios y las cargas de trabajo de SAP críticas en una plataforma compatible, ampliable y de uso demostrado en la empresa. Consigue la escalabilidad, la flexibilidad y el ahorro de costos de Azure. Con la ampliación de la asociación entre Microsoft y SAP, puede ejecutar las aplicaciones SAP en escenarios de desarrollo, pruebas y producción en Azure y serán totalmente compatibles. De SAP NetWeaver a SAP S/4HANA, de BI de SAP en Linux a Windows y de SAP HANA a SQL, lo cubrimos todo.

Además de hospedar escenarios de SAP NetWeaver con los diferentes DBMS en Azure, puede hospedar otros escenarios de cargas de trabajo de SAP, como BI de SAP en Azure. 

La unicidad de Azure para SAP HANA es una oferta que distingue a Azure. Para habilitar el hospedaje de escenarios de SAP con más demanda de recursos de memoria y CPU que implican a SAP HANA, Azure ofrece el uso de hardware de reconstrucción completa dedicado para el cliente. Use esta solución para ejecutar las implementaciones de SAP HANA que requieren hasta 24 TB (120 TB de escalabilidad horizontal) de memoria para S/4HANA u otra carga de trabajo de SAP HANA. 

El hospedaje de escenarios de carga de trabajo de SAP en Azure también puede crear requisitos de integración de identidades y de inicio de sesión único. Esta situación puede producirse al usar Azure Active Directory (Azure AD) para conectar diferentes componentes y ofertas de software como servicio (SaaS) o plataforma como servicio (PaaS) de SAP. En la sección "Integración de identidades de AAD SAP e inicio de sesión único" se describe y documenta una lista de estos escenarios de integración e inicio de sesión único con entidades de Azure AD y SAP.

## <a name="changes-to-the-sap-workload-section"></a>Cambios en la sección de cargas de trabajo de SAP
Al final de este artículo se enumeran los cambios en los documentos de la sección sobre cargas de trabajo de SAP en Azure. Las entradas del registro de cambios se mantienen durante unos 180 días.

## <a name="you-want-to-know"></a>Más información
Si tiene preguntas específicas, vamos a apuntar a documentos o flujos específicos en esta sección de la página de inicio. Más información sobre los siguientes aspectos:

- Las VM de Azure y las unidades de instancias grandes de HANA se admiten en las versiones de software de SAP y en las versiones de sistema operativo. Lea el documento [Qué software de SAP es compatible con la implementación de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-supported-product-on-azure) para obtener respuestas y el proceso para buscar la información.
- Qué escenarios de implementación de SAP se admiten en las VM de Azure y las instancias grandes de HANA. Puede encontrar información sobre los escenarios admitidos en los siguientes documentos:
    - [Carga de trabajo de SAP en escenarios admitidos en máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-planning-supported-configurations)
    - [Escenarios admitidos para instancias grandes de HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-supported-scenario)
- Para conocer qué servicios de Azure, tipos de máquinas virtuales de Azure e instancias de almacenamiento de Azure hay disponibles en las diferentes regiones de Azure, vea el sitio [Productos disponibles por región](https://azure.microsoft.com/global-infrastructure/services/) 

 
## <a name="sap-hana-on-azure-large-instances"></a>SAP HANA en Azure (instancias grandes)

Una serie de documentos le guían a través de SAP HANA en Azure (instancias grandes) o, para abreviar, las instancias grandes de HANA. Para obtener información sobre las instancias grandes de HANA, empiece con el documento [Introducción y arquitectura de SAP HANA en Azure (instancias grandes)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) y consulte la documentación relacionada en la sección de instancias grandes de HANA.



## <a name="sap-hana-on-azure-virtual-machines"></a>SAP HANA en máquinas virtuales de Azure
Esta sección de la documentación trata diferentes aspectos de SAP HANA. Antes debe estar familiarizado con los principales servicios de Azure que proporcionan servicios básicos de IaaS de Azure. Por lo tanto, necesita conocer el proceso, almacenamiento y redes de Azure. Muchos de estos temas se tratan en la [guía de planeamiento de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide) relacionada con SAP NetWeaver. 

Para obtener información sobre HANA en Azure, consulte los siguientes artículos y sus artículos secundarios:

- [Configuraciones y operaciones de infraestructura de SAP HANA en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations)
- [Alta disponibilidad de SAP HANA para máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-availability-overview)
- [Alta disponibilidad de SAP HANA en máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability)
- [Guía de copia de seguridad de SAP HANA en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)


 

## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a>SAP NetWeaver implementado en máquinas virtuales de Azure
En esta sección se incluye documentación sobre la planeación e implementación para SAP NetWeaver y Business One en Azure. La documentación se centra en los conceptos básicos y el uso de las bases de datos no perteneciente a HANA con una carga de trabajo de SAP en Azure. Los documentos y los artículos sobre alta disponibilidad también son la base para la alta disponibilidad de HANA en Azure como, por ejemplo:

- [Guía de plan de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide). 
- [SAP Business One en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/business-one-azure)
- [Protección de la implementación de una aplicación SAP NetWeaver de niveles múltiples mediante Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-sap)
- [Conector de SAP LaMa para Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/lama-installation)

Para obtener información sobre las bases de datos no pertenecientes a HANA bajo una carga de trabajo de SAP en Azure, consulte:

- [Consideraciones para la implementación de DBMS de Azure Virtual Machines para la carga de trabajo de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms_guide_general)
- [Implementación de DBMS de Azure Virtual Machines de SQL Server para la carga de trabajo de SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms_guide_sqlserver)
- [Implementación de DBMS de Azure Virtual Machines de Oracle para una carga de trabajo de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms_guide_oracle)
- [Implementación de DBMS de Azure Virtual Machines de IBM DB2 para una carga de trabajo de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms_guide_ibm)
- [Implementación de DBMS de Azure Virtual Machines de SAP ASE para una carga de trabajo de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms_guide_sapase)
- [Implementación de SAP MaxDB, liveCache y del servidor de contenido en máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms_guide_maxdb)

Para obtener información sobre las bases de datos de SAP HANA en Azure, consulte la sección "SAP HANA en máquinas virtuales de Azure".

Para obtener información sobre la alta disponibilidad de una carga de trabajo de SAP en Azure, consulte:

- [Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-high-availability-guide-start)

Este documento apunta a muchos otros documentos de arquitectura y escenario. En documentos posteriores del escenario, se proporcionan vínculos a documentos técnicos detallados que explican la implementación y configuración de los distintos métodos de alta disponibilidad. Los distintos documentos que muestran cómo establecer y configurar la alta disponibilidad para cargas de trabajo de SAP NetWeaver comprenden a los sistemas operativos Linux y Windows.


Para obtener información sobre la integración entre Azure Active Directory (AAD), los servicios de SAP y el inicio de sesión único, consulte:

- [Tutorial: Integración de Azure Active Directory con SAP Cloud for Customer](https://docs.microsoft.com/azure/active-directory/saas-apps/sap-customer-cloud-tutorial?toc=%2fazure%2fvirtual-machines%2fworkloads%2fsap%2ftoc.json)
- [Tutorial: Integración de Azure Active Directory con SAP Cloud Platform Identity Authentication](https://docs.microsoft.com/azure/active-directory/saas-apps/sap-hana-cloud-platform-identity-authentication-tutorial?toc=%2fazure%2fvirtual-machines%2fworkloads%2fsap%2ftoc.json)
- [Tutorial: Integración de Azure Active Directory con SAP Cloud Platform](https://docs.microsoft.com/azure/active-directory/saas-apps/sap-hana-cloud-platform-tutorial?toc=%2fazure%2fvirtual-machines%2fworkloads%2fsap%2ftoc.json)
- [Tutorial: Integración de Azure Active Directory con SAP NetWeaver](https://docs.microsoft.com/azure/active-directory/saas-apps/sap-netweaver-tutorial?toc=%2fazure%2fvirtual-machines%2fworkloads%2fsap%2ftoc.json)
- [Tutorial: Integración de Azure Active Directory con SAP Business ByDesign](https://docs.microsoft.com/azure/active-directory/saas-apps/sapbusinessbydesign-tutorial?toc=%2fazure%2fvirtual-machines%2fworkloads%2fsap%2ftoc.json)
- [Tutorial: Integración de Azure Active Directory con SAP HANA](https://docs.microsoft.com/azure/active-directory/saas-apps/saphana-tutorial?toc=%2fazure%2fvirtual-machines%2fworkloads%2fsap%2ftoc.json)
- [Your S/4HANA environment: Fiori Launchpad SAML single sign-on with Azure AD](https://blogs.sap.com/2017/02/20/your-s4hana-environment-part-7-fiori-launchpad-saml-single-sing-on-with-azure-ad/) (Entorno S/4HANA: inicio de sesión único basado en SAML para Fiori Launchpad con Azure AD)

Para obtener información sobre la integración de servicios de Azure en los componentes de SAP, consulte:

- [Uso de SAP HANA en Power BI Desktop](https://docs.microsoft.com/power-bi/desktop-sap-hana)
- [DirectQuery y SAP HANA](https://docs.microsoft.com/power-bi/desktop-directquery-sap-hana)
- [Uso del conector SAP BW en Power BI Desktop](https://docs.microsoft.com/power-bi/desktop-sap-bw-connector) 
- [Azure Data Factory ofrece integración de datos de SAP HANA y Business Warehouse](https://azure.microsoft.com/blog/azure-data-factory-offer-sap-hana-and-business-warehouse-data-integration)


## <a name="change-log"></a>Registro de cambios
- 10/03/2020: cambio en [Configuraciones de almacenamiento de máquinas virtuales de Azure en SAP HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations-storage) para aclarar los límites de rendimiento existentes reales de ANF
- 09/03/2020: cambio en [Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure en SUSE Linux Enterprise Server para SAP Applications](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse), [Alta disponibilidad de SAP NetWeaver en VM de Azure en SUSE Linux Enterprise Server con Azure NetApp Files para las aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-netapp-files), [Alta disponibilidad para NFS en máquinas virtuales de Azure en SUSE Linux Enterprise Server](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-nfs), [Configuración de Pacemaker en SUSE Linux Enterprise Server en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-pacemaker), [Alta disponibilidad de IBM Db2 LUW en máquinas virtuales de Azure en SUSE Linux Enterprise Server con Pacemaker](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms-guide-ha-ibm), [Alta disponibilidad de SAP HANA en máquinas virtuales de Azure en SUSE Linux Enterprise Server](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability) y [Alta disponibilidad para SAP NetWeaver en VM de Azure en Red Hat Enterprise Linux para SAP Applications: guía de varios SID](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-multi-sid) para actualizar los recursos de clúster con el agente de recursos azure-lb 
- 05/03/2020: cambios de estructura y de contenido para regiones y máquinas virtuales de Azure en [Implementación y planeamiento de Azure Virtual Machines para SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide)
- 03/03/2020: cambio en la [alta disponibilidad para SAP NW en VM de Azure en SLES con ANF para aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-netapp-files) para cambiar a un diseño de volumen de ANF más eficaz.
- 01/03/2020: modificación de la [guía de copia de seguridad de SAP HANA en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide) para incluir el servicio Azure Backup. Reducción y compresión del contenido de [Azure Backup de SAP HANA en el nivel de archivo](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level), y eliminación de un tercer documento relacionado con la copia de seguridad a través de la instantánea del disco. El contenido se controla en la Guía de copia de seguridad de SAP HANA en Azure Virtual Machines 
- 27/02/2020: cambio en la [alta disponibilidad para SAP NetWeaver en VM de Azure en SLES para aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse), la [alta disponibilidad para SAP NW en VM de Azure en SLES con ANF para aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-netapp-files) y la [guía de alta disponibilidad para SAP NetWeaver en VM de Azure en SLES con varios SID](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-multi-sid) para ajustar el parámetro del clúster "en caso de error".
- 26/02/2020: cambio en las [configuraciones de almacenamiento de Azure Virtual Machines de SAP HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations-storage) para aclarar la elección del sistema de archivos para HANA en Azure.
- 26/02/2020: cambio en la [arquitectura y los escenarios de alta disponibilidad para SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-high-availability-architecture-scenarios) a fin de incluir el vínculo a la guía de alta disponibilidad de SAP NetWeaver en VM de Azure en RHEL con varios SID.
- 26/02/2020: cambio en la [alta disponibilidad para SAP NW en VM de Azure en SLES para aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse), la [alta disponibilidad para SAP NW en VM de Azure en SLES con ANF para aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-netapp-files), la [alta disponibilidad de las VM de Azure para SAP NetWeaver en RHEL](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel) y la [alta disponibilidad de las VM de Azure para SAP NetWeaver en RHEL con Azure NetApp Files](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-netapp-files) para quitar la declaración de incompatibilidad del clúster de ASCS/ERS con varios SID.
- 26/02/2020: publicación de la [guía de alta disponibilidad para SAP NetWeaver en VM de Azure en RHEL con varios SID](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-multi-sid) para agregar un vínculo a la guía de clústeres de SUSE con varios SID.
- 25/02/2020: Cambio en [Escenarios y arquitectura de alta disponibilidad para SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-high-availability-architecture-scenarios) para agregar vínculos a los artículos de alta disponibilidad.
- 25/02/2020: Cambio en [Alta disponibilidad de IBM Db2 LUW en VM de Azure en SUSE Linux Enterprise Server con Pacemaker](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms-guide-ha-ibm) para apuntar a un documento que describe el acceso al punto de conexión público con Azure Load Balancer estándar.
- 21/02/2020: Revisión completa del artículo [Implementación de DBMS de Azure Virtual Machines de SAP ASE para la carga de trabajo de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms_guide_sapase).
- 21/02/2020: Cambio en [Configuraciones de almacenamiento de máquinas virtuales de Azure en SAP HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations-storage) para representar una nueva recomendación sobre el tamaño de franja para /hana/data y agregar la configuración de un programador de E/S.
- 21/02/2020: Cambios en documentos de instancia grande de HANA para representar las SKU recién certificadas de S224 y S224m.
- 21/02/2020: Cambio en [Alta disponibilidad de VM de Azure para SAP NetWeaver en RHEL](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel) y [Alta disponibilidad de VM de Azure para SAP NetWeaver en RHEL con Azure NetApp Files](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-netapp-files) para ajustar las restricciones del clúster a la arquitectura de replicación del servidor de puesta en cola 2 (ENSA2)
- 20/02/2020: Cambio en [Alta disponibilidad para SAP NetWeaver en VM de Azure en SLES: guía de varios SID](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-multi-sid) para agregar un vínculo a la guía de clústeres de varios SID de SUSE.
- 13/02/2020: Cambios en [Implementación y planeamiento de Azure Virtual Machines para SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide) para implementar vínculos a nuevos documentos.
- 13/02/2020: Incorporación de nueva documentación en [Carga de trabajo de SAP en escenarios admitidos en máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-planning-supported-configurations)
- 13/02/2020: Incorporación de nueva documentación en [¿Qué software de SAP es compatible con las implementaciones de Azure?](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-supported-product-on-azure)
- 13/02/2020: Cambio en [Alta disponibilidad de IBM Db2 LUW en VM de Azure en Red Hat Enterprise Linux Server](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-ibm-db2-luw) para apuntar a un documento que describe el acceso al punto de conexión público con Azure Load Balancer estándar.
- 13/02/2020: Incorporación de nuevos tipos de VM en [Configuraciones y certificaciones de SAP que se ejecutan en Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-certifications).
- 13/02/2020: Incorporación de nuevas notas de compatibilidad de SAP en [Lista de comprobación de planeamiento e implementación de cargas de trabajo de SAP en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-deployment-checklist).
- 13/02/2020: Cambio en la [alta disponibilidad de las máquinas virtuales de Azure para SAP NetWeaver en RHEL](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel) y [alta disponibilidad de las máquinas virtuales de Azure para SAP NetWeaver en RHEL con Azure NetApp Files](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-netapp-files) para alinear los tiempos de espera de los recursos de clúster con las recomendaciones de tiempo de espera de Red Hat
- 11/02/2020: Versión de la [migración de SAP HANA en instancias grandes de Azure a máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-large-instance-virtual-machine-migration)
- 07/02/2020: Cambio en [Conectividad del punto de conexión público para las máquinas virtuales que usan Azure Standard ILB en escenarios de alta disponibilidad de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-standard-load-balancer-outbound-connections) para actualizar la captura de pantalla de ejemplo de NSG
- 03/02/2020: Cambio en [Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure en SUSE Linux Enterprise Server para SAP Applications](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse) y [Alta disponibilidad de SAP NetWeaver en VM de Azure en SUSE Linux Enterprise Server con Azure NetApp Files para las aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-netapp-files) para quitar la advertencia sobre el uso de guiones en los nombres de host de los nodos de clúster en SUSE Linux Enterprise Server.
- 28/01/2020: Cambio en la [alta disponibilidad de SAP HANA en máquinas virtuales de Azure en RHEL](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability-rhel) para alinear los tiempos de espera de los recursos de clúster de SAP HANA con las recomendaciones de tiempo de espera de Red Hat.
- 17/01/2020: Cambio en los [grupos de selección de ubicación de proximidad de Azure para conseguir una latencia de red óptima con aplicaciones SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-proximity-placement-scenarios) para cambiar la sección del movimiento de las máquinas virtuales existentes a un grupo de selección de ubicación de proximidad.
- 17/01/2020: Cambio en las [configuraciones de carga de trabajo de SAP con Azure Availability Zones](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-ha-availability-zones) para que apunten al procedimiento que automatiza las mediciones de latencia entre zonas de disponibilidad
- 16/01/2020: Cambio en la [instalación y configuración de SAP HANA (instancias grandes) en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-installation) para adaptar las versiones del sistema operativo al directorio de hardware de IaaS de HANA
- 16/01/2020: Cambios en la [guía de varios SID de alta disponibilidad de las máquinas virtuales de Azure para SAP NetWeaver en SLES](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-multi-sid) para agregar instrucciones para sistemas SAP con la arquitectura de puesta en cola del servidor 2 (ENSA2)
- 10/01/2020: Cambios en la [escalabilidad horizontal de SAP HANA con nodo en espera en máquinas virtuales de Azure con Azure NetApp Files en SLES](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-scale-out-standby-netapp-files-suse) y en la [escalabilidad horizontal de SAP HANA con nodo en espera en máquinas virtuales de Azure con Azure NetApp Files en RHEL](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-scale-out-standby-netapp-files-rhel) para agregar instrucciones sobre cómo hacer que los cambios de `nfs4_disable_idmapping` sean permanentes.
- 10/01/2020: Cambios en [Alta disponibilidad de SAP NetWeaver en VM de Azure en SUSE Linux Enterprise Server con Azure NetApp Files para las aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-netapp-files) y en [Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver en Red Hat Enterprise Linux con Azure NetApp Files para aplicaciones SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-netapp-files) para agregar instrucciones sobre cómo montar volúmenes NFSv4 de Azure NetApp Files.
- 23/12/2019: Publicación de la [guía de varios SID de alta disponibilidad de las máquinas virtuales de Azure para SAP NetWeaver en SLES](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-multi-sid)
- 18/12/2019: Publicación de la [escalabilidad horizontal de SAP HANA con nodo en espera en máquinas virtuales de Azure con Azure NetApp Files en RHEL](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-scale-out-standby-netapp-files-rhel)
- 21/11/2019: Los cambios en [SAP HANA se escalan horizontalmente con el nodo en espera en máquinas virtuales de Azure con Azure NetApp Files en SUSE Linux Enterprise Server](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-scale-out-standby-netapp-files-suse) para simplificar la configuración de la asignación de identificador de NFS y cambiar la interfaz de red principal recomendada para simplificar el enrutamiento.
- 15/11/2019: Cambios menores en [Alta disponibilidad de SAP NetWeaver en SUSE Linux Enterprise Server con Azure NetApp Files para aplicaciones de SAP](high-availability-guide-suse-netapp-files.md) y [Alta disponibilidad para SAP NetWeaver en Red Hat Enterprise Linux con Azure NetApp Files para aplicaciones SAP](high-availability-guide-rhel-netapp-files.md) para aclarar las restricciones de tamaño del grupo de capacidad y quitar la declaración de que solo se admite la versión de NFSv3.
- 12/11/2019: Publicación de [Alta disponibilidad de SAP NetWeaver en Windows con Azure NetApp Files (SMB)](high-availability-guide-windows-netapp-files-smb.md)
- 08/11/2019: Cambios en [Alta disponibilidad de SAP HANA en máquinas virtuales de Azure en SUSE Linux Enterprise Server](sap-hana-high-availability.md), [Configuración de la replicación del sistema SAP HANA en máquinas virtuales de Azure](sap-hana-high-availability-rhel.md), [Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure en SUSE Linux Enterprise Server para SAP Applications](high-availability-guide-suse.md), [Alta disponibilidad de SAP NetWeaver en VM de Azure en SUSE Linux Enterprise Server con Azure NetApp Files para las aplicaciones de SAP](high-availability-guide-suse-netapp-files.md), [Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver en Red Hat Enterprise Linux](high-availability-guide-rhel.md), [Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver en Red Hat Enterprise Linux con Azure NetApp Files para aplicaciones SAP](high-availability-guide-rhel-netapp-files.md), [Alta disponibilidad para NFS en máquinas virtuales de Azure en SUSE Linux Enterprise Server](high-availability-guide-suse-nfs.md), [GlusterFS en máquinas virtuales de Azure de Red Hat Enterprise Linux para SAP NetWeaver](high-availability-guide-rhel-glusterfs.md) para recomendar el equilibrador de carga estándar de Azure  
- 08/11/2019: Cambios en [Lista de comprobación de planeamiento e implementación de cargas de trabajo de SAP en Azure](sap-deployment-checklist.md) para aclarar la recomendación de cifrado  
- 04/11/2019: Cambios en [Configuración de Pacemaker en SUSE Linux Enterprise Server en Azure](high-availability-guide-suse-pacemaker.md) para crear el clúster directamente con la configuración de unidifusión.  
- 29/10/2019: Publicación de [Conectividad del punto de conexión público para las máquinas virtuales que usan Azure Standard Load Balancer en escenarios de alta disponibilidad de SAP](high-availability-guide-standard-load-balancer-outbound-connections.md).
- 25/10/2019: Cambios en [Configuraciones de almacenamiento de máquina virtual de Azure en SAP HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations-storage) y en [Escalabilidad horizontal de SAP HANA con nodo en espera en máquinas virtuales de Azure con Azure NetApp Files en SUSE Linux Enterprise Server](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-scale-out-standby-netapp-files-suse) para clarificar el protocolo NFS para SAP HANA o para volúmenes compartidos.
- 22/10/2019: Cambio en [Alta disponibilidad de SAP NetWeaver en VM de Azure en SUSE Linux Enterprise Server con Azure NetApp Files para las aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse), [Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure en SUSE Linux Enterprise Server para aplicaciones de SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-netapp-files), [Alta disponibilidad para NFS en máquinas virtuales de Azure en SUSE Linux Enterprise Server](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-nfs), [Configuración de Pacemaker en SUSE Linux Enterprise Server en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-pacemaker), [Alta disponibilidad de IBM Db2 LUW en máquinas virtuales de Azure en SUSE Linux Enterprise Server con Pacemaker](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms-guide-ha-ibm)y [Alta disponibilidad de SAP HANA en máquinas virtuales de Azure en SUSE Linux Enterprise Server](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability) para la protección de la detección del equilibrador de carga de Azure.
- Cambios en la sección ANF y la sección de encabezado en [Configuraciones de almacenamiento de máquinas virtuales de Azure en SAP HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations-storage)
- 21/10/2019: Publicación de [SAP HANA scale-out with standby node on Azure VMs with Azure NetApp Files on SLES](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-scale-out-standby-netapp-files-suse) (Escalabilidad horizontal de SAP HANA con nodo en espera en máquinas virtuales de Azure con Azure NetApp Files en SLES)
- 16/10/2019: Corrección de vínculos rotos en [Copia de seguridad y restauración](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-backup-restore)
- 16/10/2019: Cambio en el sistema operativo mínimo recomendado de SLES 12 SP3 a SLES 12 SP4 en [Alta disponibilidad de IBM Db2 LUW en máquinas virtuales de Azure en SUSE Linux Enterprise Server con Pacemaker](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/dbms-guide-ha-ibm)
- 11/10/2019: Cambios en las configuraciones de almacenamiento de disco Ultra e introducción de ANF en [Configuraciones de almacenamiento de máquinas virtuales de Azure en SAP HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations-storage)
- 01/10/2019: Cambio en los gráficos de [Grupos de selección de ubicación de proximidad de Azure para una latencia de red óptima con aplicaciones SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-proximity-placement-scenarios) para conseguir mayor claridad.
- 01/10/2019: Cambio en [Configuraciones y operaciones de infraestructura de SAP HANA en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations) para corregir instrucciones relacionadas con el recurso compartido NFS de alta disponibilidad para /hana/shared. 
- 28/09/2019: Cambio en [Configuración de Pacemaker en Red Hat Enterprise Linux en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker) para acarar que no se admite SBD como mecanismo de barrera en los clústeres RHEL.  
- 17/09/2019: Cambio en la guía de planeación e implementación de NetWeaver para unificar los términos en torno a la extensión de máquina virtual para SAP  
- 22/08/2019: Cambios en [Configuración de Pacemaker en SUSE Linux Enterprise Server en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-pacemaker) para actualizar las direcciones URL para la creación de roles personalizados.  
- 16/08/2019: Cambios en [Configuración de Pacemaker en Red Hat Enterprise Linux en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker) para recordar a los clientes que si se actualizan a la nueva versión del agente de barrera de Azure, actualicen las acciones en el rol personalizado.  
- 15/08/2019: Cambios en [Configuraciones de almacenamiento de máquinas virtuales de Azure en SAP HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-vm-operations-storage) para reflejar la disponibilidad general de discos Ultra (anteriormente SSD Ultra)
- 01/08/2019: Cambios en la [Configuración de Pacemaker en SUSE Linux Enterprise Server en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide-suse-pacemaker) para integrar los cambios específicamente para SLES 15 


