---
title: "104 - ActivityScheduledRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae202178-8fb1-4646-a3aa-18beeda8ff93
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 104 - ActivityScheduledRecord
## Eigenschaften  
  
|||  
|-|-|  
|Id|104|  
|Schlüsselwörter|EndToEndMonitoring, Troubleshooting, HealthMonitoring, WFTracking|  
|Grad|Informationen|  
|Kanal|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Beschreibung  
 Dieses Ereignis wird vom ETW\-Überwachungsteilnehmer ausgegeben, wenn eine Aktivität in einer Workflowinstanz ActivityScheduledRecord ausgibt  
  
## Meldung  
 TrackRecord \= ActivityScheduledRecord, InstanceID \= %1,  RecordNumber \= %2, EventTime \= %3, Name \= %4, ActivityId \= %5, ActivityInstanceId \= %6, ActivityTypeName \= %7, ChildActivityName \= %8, ChildActivityId \= %9, ChildActivityInstanceId \= %10, ChildActivityTypeName \=%11, Annotations\=%12, ProfileName \= %13  
  
## Details  
  
|Datenelementname|Datenelementtyp|Beschreibung|  
|----------------------|---------------------|------------------|  
|InstanceId|xs:GUID|Die Instanz\-ID für den Workflow.|  
|RecordNumber|xs:long|Die Sequenznummer des ausgegebenen Datensatzes.|  
|EventTime|xs:dateTime|Die Zeit in UTC, als das Ereignis ausgegeben wurde|  
|Name|xs:string|Der Name der Aktivität, die die untergeordnete Aktivität geplant hat|  
|ActivityId|xs:string|Die ID der Aktivität, die die untergeordnete Aktivität geplant hat|  
|ActivityInstanceId|xs:string|Die Instanz\-ID der Aktivität, die die untergeordnete Aktivität geplant hat|  
|ActivityTypeName|xs:string|Der Typ der Aktivität, die den Abbruchvorgang angefordert hat|  
|ChildActivityName|xs:string|Der Name der geplanten Aktivität|  
|ChildActivityId|xs:string|Die ID der geplanten Aktivität|  
|ChildActivityInstanceId|xs:string|Die Instanz\-ID der geplanten Aktivität|  
|ChildActivityTypeName|xs:string|Der Typ der geplanten Aktivität|  
|Annotations|xs:string|Die Anmerkungen, die diesem Ereignis hinzugefügt wurden.Die Werte werden in einem XML\-Element im Format \<items\>\< item  name \= "annotationName" type\="System.String"\>annotationValue\<\/item\>\<\/items\> gespeichert.Wenn keine Anmerkungen angegeben werden, enthält die Zeichenfolge \<items\/\>.Die ETW\-Ereignisgröße wird von der ETW\-Puffergröße oder der maximalen Nutzlast für ein ETW\-Ereignis beschränkt.Wenn die Größe des Ereignisses die ETW\-Beschränkung überschreitet, wird das Ereignis abgeschnitten, indem die Anmerkungen ausgelassen und der Anmerkungswert durch \<items\>...\<\/items\> ersetzt wird.|  
|ProfileName|xs:string|Der Name oder das Überwachungsprofil, das zur Ausgabe dieses Ereignisses geführt hat.|  
|HostReference|xs:string|Für im Internet gehostete Dienste identifiziert dieses Feld den Dienst in der Webhierarchie eindeutig.Das Format ist als "Virtueller Anwendungspfad des Websitenamens &#124; Virtueller Dienstpfad &#124; Servicename" definiert. Beispiel: "Standardwebsite\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService".|  
|AppDomain|xs:string|Die von AppDomain.CurrentDomain.FriendlyName zurückgegebene Zeichenfolge.|