---
title: "(Modulo) (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 243ddc4f-3c4e-41e1-a3ef-4ed39e36248b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# (Modulo) (Entity SQL)
Gibt den Rest der Division eines Ausdrucks durch einen anderen zurück.  
  
## Syntax  
  
```  
  
dividend  
%  
divisor  
  
```  
  
## Argumente  
 `dividend`  
 Der zu dividierende numerische Ausdruck.`dividend` ist jeder gültige Ausdruck eines der numerischen Datentypen.  
  
 `divisor`  
 Der numerische Ausdruck, durch den der Dividend geteilt werden soll.`divisor` ist jeder gültige Ausdruck eines der numerischen Datentypen.  
  
## Ergebnistypen  
 Edm.Int32  
  
## Beispiel  
 Die folgende Entity SQL\-Abfrage verwendet den arithmetischen Operator "%", um den Rest der Division eines Ausdrucks durch einen anderen zurückzugeben. Diese Abfrage beruht auf dem "AdventureWorks Sales"\-Modell. Führen Sie folgende Schritte aus, um diese Abfrage zu kompilieren und auszuführen:  
  
1.  Verwenden Sie das Verfahren unter [Vorgehensweise: Ausführen einer Abfrage, die StructuralType\-Ergebnisse zurückgibt](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Übergeben Sie die folgende Abfrage als Argument an die `ExecuteStructuralTypeQuery`\-Methode:  
  
 [!code-csharp[DP EntityServices Concepts 2#MODULO](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#modulo)]  
  
## Siehe auch  
 [Entity SQL\-Referenz](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)