---
title: "&lt;security&gt; von &lt;ws2007HttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fdda0ff7-b462-4e26-af52-e87ddab71945
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# &lt;security&gt; von &lt;ws2007HttpBinding&gt;
Stellt die mit dem [\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)\-Element verwendeten Sicherheitseinstellungen dar.  
  
## Syntax  
  
```  
  
<system.serviceModel>  
    <bindings>  
        <ws2007HttpBinding>  
            <binding name = "string">  
              <security mode="None/Message/Transport/TransportWithMessageCredential">  
                  <transport>  
                  </transport>  
                  <message>  
                  </message>  
              </security  
        </ws2007HttpBinding>  
    </bindings>  
</system.ServiceModel>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|`mode`|-   Dies ist optional.  Gibt den angewendeten Sicherheitstyp an.  Die Standardeinstellung ist `Message`.<br /><br /> Dieses Attribut ist vom Typ <xref:System.ServiceModel.SecurityMode>.|  
  
## Mode\-Attribut  
  
|Wert|Beschreibung|  
|----------|------------------|  
|`None`|Die Sicherheitsfunktionen sind deaktiviert.|  
|`Transport`|Die Sicherheit wird über HTTPS bereitgestellt.  Der Dienst muss mit Secure Sockets Layer \(SSL\)\-Zertifikaten konfiguriert werden.  Die Nachricht wird vollständig über HTTPS gesichert, und der Dienst wird vom Client über das SSL\-Zertifikat des Diensts authentifiziert.  Die Clientauthentifizierung wird über das `ClientCredentials`\-Attribut des [\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md)\-Elements gesteuert.|  
|`Message`|Sicherheit wird über die SOAP\-Nachrichtensicherheit bereitgestellt.  Standardmäßig wird der SOAP\-Nachrichtentext verschlüsselt und signiert.  In diesem Modus kann eine Reihe von Funktionen festgelegt werden, z.&\#160;B., ob die Dienstanmeldeinformationen out\-of\-band auf dem Client verfügbar sind, welche Algorithmenfolge verwendet werden soll und welcher Schutzgrad durch die <xref:System.ServiceModel.Security.SecurityMessageProperty> auf den Nachrichtentext angewendet werden soll.  Die Clientauthentifizierung wird einmal pro Sitzung durchgeführt, und die Ergebnisse der Authentifizierung werden für die Dauer der Sitzung zwischengespeichert.|  
|`TransportWithMessageCredential`|In diesem Modus bietet HTTPS Integrität, Vertraulichkeit und Serverauthentifizierung, und die SOAP\-Nachrichtensicherheit stellt die Clientauthentifizierung sicher.  Die Clientauthentifizierung wird standardmäßig einmal pro Sitzung durchgeführt, und die Ergebnisse der Authentifizierung werden für die Dauer der Sitzung zwischengespeichert.|  
  
### Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md)|Definiert die Sicherheitseinstellungen für den Transport.  Dieses Element entspricht dem <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>\-Typ.  Diese Einstellungen werden nur übernommen, wenn der Modus auf Transport festgelegt ist.|  
|[\<message\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-ws2007httpbinding.md)|Definiert die Sicherheitseinstellungen für die Nachricht.  Dieses Element entspricht dem <xref:System.ServiceModel.Configuration.MessageSecurityOverHttpElement>\-Typ.  Diese Einstellungen werden nicht übernommen, wenn der Modus auf Transport festgelegt ist.|  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)|Eine sichere Bindung für HTTP\-Transportanwendungen.|  
  
## Hinweise  
 Diese Element ist für die Zusammenarbeit mit Diensten vorgesehen, die WS\-\*\-Spezifikationen implementieren.  Die Transportsicherheit für diese Bindung ist SSL \(Secure Sockets Layer\) über HTTP oder HTTPS.  
  
## Siehe auch  
 <xref:System.ServiceModel.WSHttpSecurity>   
 <xref:System.ServiceModel.WSHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>   
 <xref:System.ServiceModel.BasicHttpSecurity>   
 [Sichern von Diensten und Clients](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Bindungen](../../../../../docs/framework/wcf/bindings.md)   
 [Konfigurieren der vom System bereitgestellten Bindungen](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/de-de/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<Bindung\>](../../../../../docs/framework/misc/binding.md)