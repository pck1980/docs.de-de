---
title: "Handbuch f&#252;r die Interoperabilit&#228;t von Webdienstprotokollen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2981678-ebdb-433d-899b-467f7df95fb2
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# Handbuch f&#252;r die Interoperabilit&#228;t von Webdienstprotokollen
Von [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] wird eine Vielzahl von Webdienstprotokollen implementiert.  Viele dieser Protokolle verfügen über eine Reihe von Optionen und Erweiterungspunkten, deren Konfiguration im Ermessen der Implementierung liegt.  In diesem Thema finden Sie eine Liste mit Webdienstprotokollen, die von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementiert werden.  In den weiteren Themen dieses Abschnitts finden Sie ausführlichere Informationen zur Implementierung der einzelnen unterstützten Protokolle.  
  
## Von WCF implementierte Webdienstprotokolle  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] bietet mithilfe der Vertragsfunktion Unterstützung für Webdienst\-Infrastrukturprotokolle \(Web Services, WS\) über Channel und Webdienstanwendungen.  Die Interoperabilität von Anwendungsprotokollen wird mithilfe von XML Schema Description Language 1.0 \(XSD\) und Web Services Description Language \(WSDL\) 1.1 erzielt.  
  
 Die Interoperabilität von Infrastrukturprotokollen wird mittels der WS\-\*\-Spezifikationen bereitgestellt.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Kanäle bieten Unterstützung für eine Reihe von WS\-\*\-Infrastrukturprotokollen.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Kanäle werden mithilfe von Bindungselementen konfiguriert.  Die folgenden Tabellen enthalten eine vollständige Liste der WS\-\*\-Infrastrukturprotokolle, die von den verschiedenen [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Bindungselementen implementiert werden:  
  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> unterstützt die in der folgenden Tabelle aufgeführten Spezifikationen:  
  
|Spezifikation\/Dokument|Link|  
|-----------------------------|----------|  
|HTTP 1.1|[RFC 2616](http://go.microsoft.com/fwlink/?LinkId=90372)|  
|SOAP 1.1 HTTP\-Bindung|[Simple Object Access\-Protokoll \(SOAP\) 1.1](http://go.microsoft.com/fwlink/?LinkId=90520), Abschnitt 7|  
|SOAP 1,2 HTTP\-Bindung|[SOAP Version 1.2, Teil 2: Zusätze \(zweite Ausgabe\)](http://go.microsoft.com/fwlink/?LinkId=95329), Abschnitt 7|  
  
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> und <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> unterstützen die in der folgenden Tabelle aufgeführten Spezifikationen:  
  
|Spezifikation\/Dokument|Link|  
|-----------------------------|----------|  
|XML|[Extensible Markup Language \(XML\) 1.0 \(vierte Ausgabe\)](http://go.microsoft.com/fwlink/?LinkId=15139)|  
|SOAP 1,1|[Simple Object Access\-Protokoll \(SOAP\) 1.1](http://go.microsoft.com/fwlink/?LinkId=96687)|  
|SOAP 1.2 Core|[SOAP\-Version 1.2, Teil 1: Messagingframework \(zweite Ausgabe\)](http://go.microsoft.com/fwlink/?LinkId=94664)|  
|WS\-Adressierung 2004\/08|[Web Services Addressing \(WS\-Addressing\)](http://go.microsoft.com/fwlink/?LinkId=81239)|  
|W3C Web Services Addressing 1.0 \- Core|[Webdienste\-Adressierung 1.0 – Core](http://go.microsoft.com/fwlink/?LinkId=96688)|  
|W3C Web Services Addressing 1.0 \- SOAP\-Bindung|[Web Services Addressing 1.0 – SOAP\-Bindung](http://go.microsoft.com/fwlink/?LinkId=96689)|  
|W3C Web Services Addressing 1.0 \- WSDL\-Bindung\*|[Web Services Addressing 1.0 – WSDL\-Bindung](http://go.microsoft.com/fwlink/?LinkId=96690)|  
|W3C Web Services Addressing 1.0 – Metadaten|[Web Services Addressing 1.0 – Metadata](http://www.w3.org/TR/ws-addr-metadata/)|  
|WSDL SOAP1.1\-Bindung|[Web Services Description Language \(WSDL\) 1.1](http://go.microsoft.com/fwlink/?LinkId=96160)|  
|WSDL SOAP1.2\-Bindung|[WSDL 1.1\-Bindungserweiterung für SOAP 1.2](http://go.microsoft.com/fwlink/?LinkId=96691)|  
  
 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> unterstützt die in der folgenden Tabelle aufgeführten Spezifikationen:  
  
|Spezifikation\/Dokument|Link|  
|-----------------------------|----------|  
|XOP|[XML\-binary Optimized Packaging](http://go.microsoft.com/fwlink/?LinkId=96714)|  
|MTOM \+ SOAP1.2\-Bindung|[SOAP\-Nachrichten\-Übertragungsoptimierungsmechanismus](http://go.microsoft.com/fwlink/?LinkId=96713)|  
|MTOM SOAP 1.1\-Bindung|[SOAP 1.1\-Bindung für MTOM 1.0](http://go.microsoft.com/fwlink/?LinkId=96712)|  
|MTOM WS\-Richtlinienassertionen|Veröffentlichung steht noch aus|  
  
 <xref:System.ServiceModel.Channels.SecurityBindingElement> unterstützt die in der folgenden Tabelle aufgeführten Spezifikationen:  
  
|Spezifikation\/Dokument|Link|  
|-----------------------------|----------|  
|WSS: SOAP\-Nachrichtensicherheit 1,0|[Webdienstesicherheit: SOAP\-Nachrichtensicherheit 1.0](http://go.microsoft.com/fwlink/?LinkId=94684)|  
|WSS: Username Token Profile 1.0|[Webdienstesicherheit: Username\-Tokenprofil 1.0](http://go.microsoft.com/fwlink/?LinkId=95334)<br /><br /> Kennwort erforderlich\/@Type\=PasswordText \(Standard\)|  
|WSS: X.509 Token Profile 1.0|[Webdienstesicherheit: X.509\-Zertifikatstokenprofil](http://go.microsoft.com/fwlink/?LinkId=95335)|  
|WSS: SAML 1.1 Token Profile 1,0|[Webdienstesicherheit: SAML\-Tokenprofil](http://go.microsoft.com/fwlink/?LinkId=96693)|  
|WSS: SOAP\-Nachrichtensicherheit 1.1|[Webdienstesicherheit: SOAP\-Nachrichtensicherheit 1.1](http://go.microsoft.com/fwlink/?LinkId=91240)|  
|WSS: Username Token Profile 1.1|[Webdienstesicherheit: Username\-Tokenprofil 1.1](http://go.microsoft.com/fwlink/?LinkId=95331)<br /><br /> Implementieren Sie keine kennwortbasierte Schlüsselableitung;<br /><br /> Kennwort erforderlich\/@Type\=PasswordText \(Standard\)|  
|WSS: X509 Token Profile 1.1|[Webdienstesicherheit: X.509\-Zertifikatstokenprofil 1.1](http://go.microsoft.com/fwlink/?LinkId=95332)|  
|WSS: Kerberos Token Profile 1.1|[Webdienstesicherheit: Kerberos\-Tokenprofil 1.1](http://go.microsoft.com/fwlink/?LinkId=95333)|  
|WSS: SAML 1.1 Token Profile 1.1|[Webdienstesicherheit: SAML\-Tokenprofil 1.1](http://go.microsoft.com/fwlink/?LinkId=96694)|  
|WS\-Secure Conversation|[Webdienste: sichere Konversationssprache](http://go.microsoft.com/fwlink/?LinkId=95317)|  
|WS\-Trust 1.4 \(möglicherweise in englischer Sprache\)|[Webdienste: Trust\-Sprache](http://go.microsoft.com/fwlink/?LinkId=169514)|  
|WS\-SecurityPolicy 2005\/07|[Webdienste: sichere Konversationssprache](http://go.microsoft.com/fwlink/?LinkId=95317)<br /><br /> Wurde gemäß den an das OASIS WS\-SX Technical Committee übermittelten Fehlerberichten geändert.<br /><br /> [ws\-sx\-Nachricht](http://go.microsoft.com/fwlink/?LinkId=96700)|  
|WS\-ReliableMessaging 1.1|[Zuverlässiges Messaging\-Protokoll, Version 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)|  
  
 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> unterstützt die in der folgenden Tabelle aufgeführten Spezifikationen:  
  
|Spezifikation\/Dokument|Link|  
|-----------------------------|----------|  
|WS\-Coordination|[Webdienste: Koordinierung](http://go.microsoft.com/fwlink/?LinkId=95324)|  
|WS\-AtomicTransaction|[Webdienste: Atomic Transaction](http://go.microsoft.com/fwlink/?LinkId=95323)|  
  
 Die Klassen <xref:System.ServiceModel.Description.MetadataExporter>, <xref:System.ServiceModel.Description.MetadataImporter>, <xref:System.ServiceModel.Description.WSDLExporter>, <xref:System.ServiceModel.Description.WSDLImporter> und <xref:System.ServiceModel.Description.MetadataResolver> bieten Unterstützung für die folgenden Metadatenspezifikationen:  
  
-   [XML Schema Part 1: Structures Second Edition](http://go.microsoft.com/fwlink/?LinkId=3536)  
  
-   [XML Schema Part 2: Datatypes Second Edition](http://go.microsoft.com/fwlink/?LinkId=40138)  
  
-   [WSDL 1.1](http://go.microsoft.com/fwlink/?LinkId=96160)  
  
-   [WS\-Policy 1.2](http://go.microsoft.com/fwlink/?LinkId=96705)  
  
-   [WS\-Policy 1.5](http://go.microsoft.com/fwlink/?LinkId=96706)  
  
-   [WS\-PolicyAttachment 1.2](http://go.microsoft.com/fwlink/?LinkId=96707)  
  
-   [WS\-MetadataExchange 1.1](http://go.microsoft.com/fwlink/?LinkId=94868)  
  
-   [WS\-Transfer zum Abrufen von Metadaten](http://go.microsoft.com/fwlink/?LinkId=96708)  
  
 Darüber hinaus werden die folgenden Interoperabilitätsprofile in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementiert:  
  
-   [Basic Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=69313)  
  
-   [Simple SOAP Binding 1.0](http://go.microsoft.com/fwlink/?LinkId=96710)  
  
-   [Basic Security Profile 1.0 \(Arbeitsentwurf\)](http://go.microsoft.com/fwlink/?LinkId=96711)  
  
## Siehe auch  
 [Durc vom System bereitgestellte Interoperabilitätsbindungen unterstützte Webdienstprotokolle](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)   
 [Messagingprotokolle](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)   
 [Datenvertrags\-Schemareferenz](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)   
 [WSDL und Richtlinie](../../../../docs/framework/wcf/feature-details/wsdl-and-policy.md)   
 [Sicherheitsprotokolle](../../../../docs/framework/wcf/feature-details/security-protocols.md)   
 [Zuverlässiges Messaging\-Protokoll, Version 1.0](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-0.md)   
 [Zuverlässiges Messaging\-Protokoll, Version 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)   
 [Transaktionsprotokolle](../../../../docs/framework/wcf/feature-details/transaction-protocols.md)   
 [Kontextaustauschprotokoll](../../../../docs/framework/wcf/feature-details/context-exchange-protocol.md)