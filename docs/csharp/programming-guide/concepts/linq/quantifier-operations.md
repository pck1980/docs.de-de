---
title: "Quantifizierer-Vorgänge (C#) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 84ac2ac2-7a63-4581-bc4c-14e34be1493b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0e4265f08f1fbe540885e1c9de28c5054f2f33a7
ms.lasthandoff: 03/13/2017

---
# <a name="quantifier-operations-c"></a>Quantifizierer-Vorgänge (C#)
Quantifizierer-Vorgänge geben einen <xref:System.Boolean>-Wert zurück, der angibt, ob einige oder alle Elemente in einer Sequenz eine Bedingung erfüllen.  
  
 Die folgende Abbildung zeigt zwei verschiedene Quantifizierer-Vorgänge bei zwei verschiedenen Quellsequenzen. Der erste Vorgang fragt, ob eines oder mehrere der Elemente das Zeichen „A“ sind. Das Ergebnis ist `true`. Der zweite Vorgang fragt, ob alle Elemente das Zeichen „A“ sind. Das Ergebnis ist `true`.  
  
 ![LINQ-Quantifizierer-Vorgänge](../../../../csharp/programming-guide/concepts/linq/media/linq_quantifier.png "LINQ_Quantifier")  
  
 Die Methoden des Standardabfrageoperators, die Quantifizierer-Vorgänge ausführen, sind im folgenden Abschnitt aufgeführt.  
  
## <a name="methods"></a>Methoden  
  
|Methodenname|Beschreibung|C#-Abfrageausdruckssyntax|Weitere Informationen|  
|-----------------|-----------------|---------------------------------|----------------------|  
|Alle|Bestimmt, ob alle Elemente in einer Sequenz eine Bedingung erfüllen.|Nicht zutreffend.|<xref:System.Linq.Enumerable.All%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.All%2A?displayProperty=fullName>|  
|Beliebig|Bestimmt, ob Elemente einer Sequenz eine Bedingung erfüllen.|Nicht zutreffend.|<xref:System.Linq.Enumerable.Any%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Any%2A?displayProperty=fullName>|  
|Enthält|Bestimmt, ob eine Sequenz ein angegebenes Element enthält.|Nicht zutreffend.|<xref:System.Linq.Enumerable.Contains%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Contains%2A?displayProperty=fullName>|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Linq>   
 [Übersicht über Standardabfrageoperatoren (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [How to: Dynamically Specify Predicate Filters at Runtime (Vorgehensweise: Dynamisches Festlegen von Prädikatfiltern zur Laufzeit)](../../../../csharp/programming-guide/linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)   
 [How to: Query for Sentences that Contain a Specified Set of Words (LINQ) (C#) (Vorgehensweise: Abfragen von Sätzen, die bestimmte Wörter enthalten (LINQ) (C#))](../../../../csharp/programming-guide/concepts/linq/how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq.md)
