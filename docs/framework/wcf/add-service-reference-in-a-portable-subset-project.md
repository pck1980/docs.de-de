---
title: "Hinzuf&#252;gen eines Dienstverweises in einem Projekt f&#252;r die portable Teilmenge | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 61ccfe0f-a34b-40ca-8f5e-725fa1b8095e
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Hinzuf&#252;gen eines Dienstverweises in einem Projekt f&#252;r die portable Teilmenge
Projekte für portable Teilmengen ermöglichen es Programmierern von .NET\-Assemblys, eine einzelne Quellstruktur zu verwalten und das System mit Unterstützung mehrerer .NET\-Plattformen \(Desktop, Silverlight, Windows Phone und XBOX\) aufzubauen.Projekte für portable Teilmengen verweisen nur auf portable .NET\-Bibliotheken, die einer .NET Framework\-Assembly entsprechen, die von einer beliebigen .NET\-Kernplattform verwendet werden kann.  
  
## Details zu "Dienstverweis hinzufügen"  
 Wenn Sie einem Projekt für portable Teilmengen einen Dienstverweis hinzufügen, werden die folgenden Einschränkungen erzwungen:  
  
1.  Für <xref:System.Xml.Serialization.XmlSerializer> sind nur literale Codierungen zulässig.SOAP\-Codierungen generieren während des Imports einen Fehler.  
  
2.  Bei Diensten, die <xref:System.Runtime.Serialization.DataContractSerializer>\-Szenarien verwenden, wird ein Datenvertrag\-Ersatzzeichen bereitgestellt, um sicherzustellen, dass wiederverwendete Typen nur aus der portablen Teilmenge stammen.  
  
3.  Endpunkte, die auf Bindungen basieren, die in portablen Bibliotheken nicht unterstützt werden \(alle Bindungen außer <xref:System.ServiceModel.BasicHttpBinding>, <xref:System.ServiceModel.WsHttpBinding> ohne Transaktionsfluss, zuverlässige Sitzungen oder MTOM\-Codierung und die entsprechenden benutzerdefinierten Bindungen\), werden ignoriert.  
  
4.  Nachrichtenheader werden vor dem Import aus allen Nachrichtenbeschreibungen in sämtlichen Vorgängen gelöscht.  
  
5.  Die nicht portablen Attribute <xref:System.ComponentModel.DesignerCategoryAttribute>, <xref:System.Serializable> und <xref:System.ServiceModel.TransactionFlow> werden aus generiertem Clientproxycode entfernt.  
  
6.  Die nicht portablen Eigenschaften **ProtectionLevel**, **SessionMode**, **IsInitiating** und **IsTerminating** werden aus <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.OperationContract> und <xref:System.ServiceModel.FaultContract> entfernt.  
  
7.  Alle Dienstvorgänge werden auf dem Clientproxy als asynchrone Vorgänge generiert.  
  
8.  Generierte Clientkonstruktoren, die nicht portable Typen verwenden, werden entfernt.  
  
9. Eine <xref:System.Net.CookieContainer>\-Instanz wird für den generierten Client verfügbar gemacht.  
  
10. Am Anfang der Datei wird ein Kommentar eingefügt, der die Assembly und die Version des Code\-Generators identifiziert: `// This code was auto-generated by Microsoft.VisualStudio.Portable.AddServiceReference, version 1.0.0.0`  
  
11. Die <xref:System.Runtime.Serialization.ISerializable>\-Schnittstelle wird nicht unterstützt.  
  
12. Net.Tcp\- und PollingDuplex\-Bindungen werden nicht unterstützt.  
  
13. <xref:System.Runtime.Serialization.DataContractSerializer> wird immer bei Fehlern verwendet.  
  
14. <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> wird in Projekten für portable Teilmengen nicht unterstützt.  
  
## Siehe auch  
 [Zugreifen auf Dienste mithilfe eines WCF\-Clients](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)   
 [Portable Klassenbibliothek](http://msdn.microsoft.com/library/gg597391\(v=vs.110\))