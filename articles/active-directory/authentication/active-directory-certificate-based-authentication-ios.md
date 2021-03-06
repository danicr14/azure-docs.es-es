---
title: 'Autenticación basada en certificados en iOS: Azure Active Directory'
description: Obtenga información acerca de los escenarios admitidos y los requisitos para configurar la autenticación basada en certificados en las soluciones con dispositivos iOS
services: active-directory
ms.service: active-directory
ms.subservice: authentication
ms.topic: conceptual
ms.date: 01/15/2018
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.reviewer: annaba
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8a042897ecbe35935c1832a53f523eb0597ebafc
ms.sourcegitcommit: 62c5557ff3b2247dafc8bb482256fef58ab41c17
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "80654239"
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Autenticación basada en certificados de Azure Active Directory en iOS

Los dispositivos iOS pueden usar la autenticación basada en certificados (CBA) para autenticarse en Azure Active Directory mediante el uso de un certificado de cliente en el dispositivo cuando se conecten a:

* aplicaciones móviles de Office como Microsoft Outlook y Microsoft Word,
* clientes de Exchange ActiveSync (EAS).

Al configurar esta función, no tendrá que escribir una combinación de nombre de usuario y contraseña en determinadas aplicaciones de correo electrónico y Microsoft Office de su dispositivo móvil.

En este tema se proporcionan los requisitos y los escenarios admitidos para configurar CBA en un dispositivo iOS (Android) para usuarios de inquilinos de planes de Office 365 Enterprise, Empresa, Educación, US Government, China y Alemania.

Esta característica se encuentra disponible como versión preliminar en los planes Office 365 US Government Defense y US Government Federal.

## <a name="microsoft-mobile-applications-support"></a>Compatibilidad con aplicaciones móviles de Microsoft

| Aplicaciones | Soporte técnico |
| --- | --- |
| Aplicación Azure Information Protection |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| Portal de empresa de Intune |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| Equipos de Microsoft |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| OneNote |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| OneDrive |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| Outlook |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| Power BI |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| Skype Empresarial |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| Word, Excel y PowerPoint |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |
| Yammer |![La marca de verificación indica que hay compatibilidad con esta aplicación][1] |

## <a name="requirements"></a>Requisitos

La versión del sistema operativo del dispositivo debe ser iOS 9 y posterior.

Se debe configurar un servidor de federación.

Se requiere Microsoft Authenticator para las aplicaciones de Office en iOS.

Para que Azure Active Directory revoque un certificado de cliente, el token de ADFS debe tener las siguientes notificaciones:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>` (el número de serie del certificado de cliente)
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>` (la cadena del emisor del certificado de cliente)

Azure Active Directory agrega estas notificaciones para el token de actualización, en caso de que estén disponibles en el token de ADFS (o en cualquier otro token SAML). Cuando hay que validar el token de actualización, esta información se utiliza para comprobar la revocación.

Se recomienda actualizar las páginas de error de ADFS de su organización con la información siguiente:

* El requisito de instalar Microsoft Authenticator en iOS
* Instrucciones sobre cómo obtener un certificado de usuario

Para más información, consulte el artículo sobre la [personalización de las páginas de inicio de sesión de AD FS](https://technet.microsoft.com/library/dn280950.aspx).

Algunas aplicaciones de Office (con la autenticación moderna habilitada) envían "*prompt=login*" a Azure AD en su solicitud. De manera predeterminada, Azure AD traduce "*prompt=login*" en la solicitud para ADFS a "*wauth=usernamepassworduri*" (pide a ADFS que realice la autenticación de U y P) y "*wfresh=0*" (pide a ADFS que ignore el estado de SSO y realice una autenticación nueva). Si desea habilitar la autenticación basada en certificados para estas aplicaciones, es preciso que modifique el comportamiento predeterminado de Azure AD. Basta con establecer "*PromptLoginBehavior*" en la configuración del dominio federado como "*Disabled*".
Para realizar esta tarea, puede usar el cmdlet [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0):

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`

## <a name="exchange-activesync-clients-support"></a>Compatibilidad con clientes de Exchange ActiveSync

En iOS 9 o posterior, se admite el cliente de correo de iOS nativo. Para todas las demás aplicaciones de Exchange ActiveSync, para determinar si se admite esta característica, póngase en contacto con el desarrollador de la aplicación.

## <a name="next-steps"></a>Pasos siguientes

Si quiere configurar la autenticación basada en certificados en su entorno, consulte las instrucciones de [Introducción a la autenticación basada en certificados en Android](../authentication/active-directory-certificate-based-authentication-get-started.md).

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
