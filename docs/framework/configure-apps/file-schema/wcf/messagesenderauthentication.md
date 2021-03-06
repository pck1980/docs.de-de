---
title: "&lt;messageSenderAuthentication&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ea62fc06-55fb-42e0-aa2b-8867bdf4b415
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;messageSenderAuthentication&gt;
Gibt Authentifizierungseinstellungen für ein Peerzertifikat an, das von einem Nachrichtenabsender verwendet wird.  
  
## Syntax  
  
```  
  
<messageSenderAuthentication  
   customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
   certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
   revocationMode="NoCheck/Online/Offline"  
   trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|`certificateValidationMode`|Optionale Enumeration.  Gibt einen von fünf die Überprüfung von Anmeldeinformationen verwendeten Modi an.  Dieses Attribut ist vom Typ <xref:System.ServiceModel.Security.X509CertificateValidationMode>.  Wenn dies auf `Custom` festgelegt wurde, muss auch ein `customCertificateValidator` bereitgestellt werden.|  
|`customCertificateValidatorType`|Optionale Zeichenfolge.  Bestimmt einen Typ und eine Assembly, die zum Prüfen eines benutzerdefinierten Typs verwendet werden.  Das Attribut muss festgelegt werden, wenn für `certificateValidationMode` der Wert `Custom` festgelegt wurde.  Dieses Attribut ist vom Typ <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] stellt ein standardmäßiges Peerzertifikats\-Validierungssteuerelement bereit, das das Peerzertifikat gegen den Speicher vertrauenswürdiger Personen überprüft.  Außerdem wird überprüft, ob sich das Zertifikat zu einem gültigen Stamm verkettet.  Sie können ein benutzerdefiniertes Validierungssteuerelement implementieren, um ein anderes Verhalten anzugeben und dieses Attribut zum Verweisen auf das benutzerdefinierte Validierungssteuerelement verwenden.|  
|`revocationMode`|Optionale Enumeration.  Legt den Zertifikatssperrmodus fest.  Dieses Attribut ist vom Typ <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>.  Das System stellt anhand der Liste mit den gesperrten Zertifikaten sicher, dass das Clientzertifikat nicht gesperrt wurde.  Diese Überprüfung kann entweder online oder offline mit einer zwischengespeicherten Liste gesperrter Zertifikate erfolgen.  Die Sperrüberprüfung kann deaktiviert werden, indem für dieses Attribut der Wert NoCheck festgelegt wird.|  
|`trustedStoreLocation`|Optionale Enumeration.  Gibt den Ort des vertrauenswürdigen Speichers an, an dem das Peerzertifikat vom [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]\-Sicherheitssystem überprüft wird.  Dieses Attribut ist vom Typ <xref:System.Security.Cryptography.X509Certificates.StoreLocation>.|  
  
### Untergeordnete Elemente  
 Keine  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-servicecredentials.md)|Gibt die aktuellen Anmeldeinformationen für einen Peerknoten an.|  
  
## Hinweise  
 Dieses Element muss konfiguriert werden, wenn die Nachrichtenauthentifizierung ausgewählt wird.  Für Ausgabekanäle wird jede Nachricht mit dem von [\<certificate\>](../../../../../docs/framework/configure-apps/file-schema/wcf/certificate-element.md) bereitgestellten Zertifikat signiert.  Alle Nachrichten werden vor dem Zustellen zur Anwendung mithilfe des durch das `customCertificateValidatorType`\-Attribut dieses Elements angegebenen Validierungssteuerelements mit den Nachrichtenanmeldeinformationen verglichen.  Das Validierungssteuerelement kann die Anmeldeinformationen akzeptieren oder ablehnen.  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>   
 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>   
 <xref:System.ServiceModel.Security.PeerCredential.MessageSenderAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.MessageSenderAuthentication%2A>   
 [Verwenden von Zertifikaten](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Peer\-to\-Peer\-Netzwerke](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/de-de/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/de-de/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [Sichern von Peerkanalanwendungen](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)