---
title: Proxy de aplicación de Azure AD y Qlik Sense | Microsoft Docs
description: Active el proxy de aplicación en Azure Portal e instale los conectores del proxy inverso.
services: active-directory
documentationcenter: ''
author: msmimart
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: article
ms.date: 09/06/2018
ms.author: mimart
ms.reviewer: japere
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2edf63da0fd09f829f936b54eb088c34dfe029a1
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2020
ms.locfileid: "79036994"
---
# <a name="application-proxy-and-qlik-sense"></a>Proxy de aplicación y Qlik Sense 
Azure Active Directory Application Proxy y Qlik Sense se han asociado para garantizar que pueda usar fácilmente el proxy de aplicación para proporcionar acceso remoto para la implementación de Qlik Sense.  

## <a name="prerequisites"></a>Prerrequisitos 
Para el resto de este escenario, se da por sentado que ha hecho lo siguiente:
 
- Configurar [Qlik Sense](https://community.qlik.com/docs/DOC-19822). 
- [Instalar un conector de proxy de aplicación](application-proxy-add-on-premises-application.md#install-and-register-a-connector) 
 
## <a name="publish-your-applications-in-azure"></a>Publicación de aplicaciones en Azure 
Para publicar QlikSense, debe publicar dos aplicaciones en Azure.  

### <a name="application-1"></a>Aplicación n.º 1: 
Siga estos pasos para publicar la aplicación. Para obtener un tutorial más detallado de los pasos 1 a 8, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](application-proxy-add-on-premises-application.md). 


1. Inicie sesión en Azure Portal como administrador global. 
2. Seleccione **Azure Active Directory** > **Aplicaciones empresariales**. 
3. Seleccione **Agregar** en la parte superior de la hoja. 
4. Seleccione **Aplicación local**. 
5. Rellene los campos requeridos con la información de la aplicación nueva. Utilice las siguientes instrucciones para realizar la configuración: 
   - **Dirección URL interna**: esta aplicación debe tener una dirección URL interna que es la propia dirección URL de QlikSense. Por ejemplo, **https&#58;//demo.qlikemm.com:4244** 
   - **Método de autenticación previa**: Azure Active Directory (se recomienda, pero no es obligatorio). 
1. Seleccione **Agregar** en la parte inferior de la hoja. Se agrega la aplicación y se abre el menú de inicio rápido. 
2. En dicho menú, seleccione **Asignar un usuario para las pruebas**  y agregue al menos un usuario a la aplicación. Asegúrese de que esta cuenta de prueba tiene acceso a la aplicación local. 
3. Seleccione **Asignar** para guardar la asignación del usuario de prueba. 
4. (Opcional) En la hoja de administración de la aplicación, seleccione Inicio de sesión único. Elija **Kerberos Constrained Delegation** (Delegación limitada de Kerberos) en el menú desplegable y rellene los campos obligatorios según la configuración de Qlik. Seleccione **Guardar**. 

### <a name="application-2"></a>Aplicación n.º 2: 
Siga los mismos pasos que para la aplicación n.º 1, con las siguientes excepciones: 

**Paso 5**: la dirección URL interna ahora debe ser la dirección URL de QlikSense con el puerto de autenticación que usa la aplicación. En las versiones de QlikSense anteriores a abril de 2018, el valor predeterminado es **4244** para HTTPS y **4248** para HTTP. En las versiones de QlikSense posteriores a abril de 2018, el valor predeterminado es **443** para HTTPS y **80** para HTTP.  Por ejemplo, **https&#58;//demo.qlik.com:4244**</br></br>
**Paso 10:** no configure SSO y deje el **Inicio de sesión único deshabilitado**
 
 
## <a name="testing"></a>Prueba 
La aplicación ya se puede probar. Acceda a la dirección URL externa que usó para publicar QlikSense en la aplicación n.º 1 e inicie sesión como usuario asignado a ambas aplicaciones.  

## <a name="additional-references"></a>Referencias adicionales
Para obtener más información acerca de la publicación de Qlik Sense con el proxy de aplicación, consulte los artículos de Qlik Community: 
- [Azure AD with Integrated Windows Authentication using a Kerberos Constrained Delegation with Qlik Sense](https://community.qlik.com/docs/DOC-20183) (Azure AD con autenticación integrada de Windows con una delegación limitada de kerberos con Qlik Sense)
- [Qlik Sense integration with Azure AD Application Proxy](https://community.qlik.com/t5/Technology-Partners-Ecosystem/Azure-AD-Application-Proxy/ta-p/1528396) (Integración de Qlik Sense con el proxy de aplicación de Azure AD)

## <a name="next-steps"></a>Pasos siguientes

- [Publicar aplicaciones con Proxy de aplicación](application-proxy-add-on-premises-application.md)
- [Trabajar con conectores de Application Proxy](application-proxy-connector-groups.md)

