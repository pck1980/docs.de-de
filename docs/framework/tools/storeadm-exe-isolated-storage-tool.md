---
title: "Storeadm.exe (Isolated Storage Tool) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Storeadm.exe"
  - "listing stores for current user"
  - "Isolated Storage tool"
  - "stores, current user"
  - "removing stores"
ms.assetid: b81202b8-d91d-4b23-9c53-4a112f74a44a
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# Storeadm.exe (Isolated Storage Tool)
Das Isolated Storage\-Tool listet alle vorhandenen Speicher des aktuellen Benutzers auf oder löscht diese.  
  
 Dieses Tool wird automatisch mit Visual Studio installiert.  Zum Ausführen des Tools verwenden Sie die Developer\-Eingabeaufforderung \(oder die Visual Studio\-Eingabeaufforderung in Windows 7\).  Weitere Informationen finden Sie unter [Eingabeaufforderungen](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Geben Sie an der Eingabeaufforderung Folgendes ein:  
  
## Syntax  
  
```  
  
storeadm [/list][/machine][/remove][/roaming][/quiet]  
```  
  
#### Parameter  
  
|Option|Beschreibung|  
|------------|------------------|  
|**\/h**\[**elp**\]|Zeigt Befehlssyntax und Optionen für das Tool an.|  
|**\/list**|Zeigt sämtliche vorhandenen Speicher des aktuellen Benutzers an.  Dies schließt die Speicher für alle von diesem Benutzer ausgeführten Anwendungen oder Assemblys ein.|  
|**\/machine**|Wählt den Computerspeicher aus.  Verwenden Sie diese Option zusammen mit der **\/list**\-Option oder der **\/remove**\-Option, um die auf den Computerspeicher anzuwendende Aktion anzugeben.<br /><br /> Neu in .NET Framework 2.0|  
|**\/quiet**|Gibt den stillen Modus an. Dies unterdrückt die Ausgabe von Informationen und zeigt nur Fehlermeldungen an.|  
|**\/remove**|Entfernt alle vorhandenen Speicher des aktuellen Benutzers dauerhaft.|  
|**\/roaming**|Wählt den Roamingspeicher aus.  Verwenden Sie diese Option zusammen mit der **\/list**\-Option oder der **\/remove**\-Option, um anzugeben, dass die Aktion auf den Roamingspeicher angewendet werden soll.|  
|**\/?**|Zeigt Befehlssyntax und Optionen für das Tool an.|  
  
## Hinweise  
 Wird "Storeadm.exe" ohne Angabe von Optionen von der Befehlszeile aus ausgeführt, werden Syntax und Optionen für das Tool angezeigt.  
  
 Die **\/list**\-Option und die **\/remove**\-Option werden in der Regel nicht gleichzeitig verwendet. Wenn jedoch zwei oder mehr Optionen angegeben sind, erfolgt deren Verarbeitung in der Reihenfolge ihres Eingabe in die Befehlszeile.  
  
 Anwendungen bieten die Wahl, in einen von zwei Speichern für einen Benutzer oder in den Computerspeicher zu speichern:  
  
-   Der lokale Speicher befindet sich an einem Speicherort, der \(unter Windows 2000 und höher\) kein Roaming zulässt, selbst wenn Benutzerdatenroaming für den Benutzer aktiviert ist.  
  
-   Der Roamingspeicher befindet sich an einem Speicherort, der Roaming ermöglicht, sofern über die Windows NT\-Verwaltung das Roaming von Benutzerdaten aktiviert ist.  
  
-   Der Computerspeicher wird von allen Benutzern eines Computers gemeinsam genutzt und unter einem allgemeinen Verzeichnis auf dem jeweiligen Computer angelegt.  
  
    > [!NOTE]
    >  Der Computerspeicher ist ein neues Feature in .NET Framework, Version 2.0.  
  
 Ob Roaming für den Benutzer tatsächlich aktiviert ist, wirkt sich nicht auf die Verwaltung von "Storeadm.exe" aus.  Wenn das Tool ohne Optionen ausgeführt wird, werden sämtliche Aktionen auf den lokalen Speicher angewendet.  Wird das Tool mit der **\/roaming**\-Option ausgeführt, werden alle Aktionen auf den Speicher angewendet, der Roaming zulässt.  Wenn das Tool mit der **\/machine**\-Option ausgeführt wird, werden sämtliche Aktionen auf den Computerspeicher angewendet.  
  
## Siehe auch  
 [Tools](../../../docs/framework/tools/index.md)   
 [Isolierte Speicherung](../../../docs/standard/io/isolated-storage.md)   
 [Eingabeaufforderungen](../../../docs/framework/tools/developer-command-prompt-for-vs.md)