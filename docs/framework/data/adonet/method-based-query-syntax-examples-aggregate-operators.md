---
title: "Beispiele f&#252;r die methodenbasierte Abfragesyntax: Aggregierungsoperatoren (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5ed5f01d-acb2-4dd4-be60-f04c2d570fa8
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Beispiele f&#252;r die methodenbasierte Abfragesyntax: Aggregierungsoperatoren (LINQ to DataSet)
In den Beispielen in diesem Thema wird gezeigt, wie Sie mithilfe der Operatoren <xref:System.Linq.Enumerable.Aggregate%2A>, <xref:System.Linq.Enumerable.Average%2A>, <xref:System.Linq.Enumerable.Count%2A>, <xref:System.Linq.Enumerable.LongCount%2A>, <xref:System.Linq.Enumerable.Max%2A>, <xref:System.Linq.Enumerable.Min%2A> und <xref:System.Linq.Enumerable.Sum%2A> und der methodenbasierten Abfragesyntax ein <xref:System.Data.DataSet> abfragen und Daten aggregieren können.  
  
 Informationen zur `FillDataSet`\-Methode, die in diesen Beispielen verwendet wird, finden Sie unter [Laden von Daten in ein 'DataSet'](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md).  
  
 In den Beispielen in diesem Thema wird auf die Tabellen \<legacyBold\>Contact\<\/legacyBold\>, \<legacyBold\>Address\<\/legacyBold\>, \<legacyBold\>Product\<\/legacyBold\>, \<legacyBold\>SalesOrderHeader\<\/legacyBold\> und \<legacyBold\>SalesOrderDetail\<\/legacyBold\> in der \<legacyBold\>AdventureWorks\<\/legacyBold\>\-Beispieldatenbank zurückgegriffen.  
  
 Die Beispiele in diesem Thema beziehen sich auf die folgenden `using`\/`Imports`\-Anweisungen:  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen eines LINQ to DataSet\-Projekts in Visual Studio](../../../../docs/framework/data/adonet/how-to-create-a-linq-to-dataset-project-in-vs.md).  
  
## Aggregat  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Aggregate%2A>\-Methode verwendet, um die ersten 5 Kontakte aus der `Contact`\-Tabelle abzurufen und eine Liste der Nachnamen zu erstellen, in der die einzelnen Einträge durch Kommas voneinander getrennt sind.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Aggregate_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#aggregate_mq)]
 [!code-vb[DP LINQ to DataSet Examples#Aggregate_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#aggregate_mq)]  
  
## Average  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Average%2A>\-Methode verwendet, um den durchschnittlichen Listenpreis der Produkte zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Average_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#average_mq)]
 [!code-vb[DP LINQ to DataSet Examples#Average_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#average_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Average%2A>\-Methode verwendet, um den durchschnittlichen Listenpreis der Produkte für die einzelnen Stile zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Average2_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#average2_mq)]
 [!code-vb[DP LINQ to DataSet Examples#Average2_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#average2_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Average%2A>\-Methode verwendet, um den durchschnittlichen fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#AverageProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#averageprojection_mq)]
 [!code-vb[DP LINQ to DataSet Examples#AverageProjection_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#averageprojection_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Average%2A>\-Methode verwendet, um für jede Kontakt\-ID den durchschnittlichen fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#AverageGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#averagegrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#AverageGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#averagegrouped_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Average%2A>\-Methode verwendet, um die Aufträge mit dem durchschnittlichen `TotalDue`\-Wert für jeden Kontakt abzurufen.  
  
 [!code-csharp[DP LINQ to DataSet Examples#AverageElements_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#averageelements_mq)]
 [!code-vb[DP LINQ to DataSet Examples#AverageElements_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#averageelements_mq)]  
  
## Anzahl  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Count%2A>\-Methode verwendet, um die Anzahl der Produkte in der `Product`\-Tabelle zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Count](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#count)]
 [!code-vb[DP LINQ to DataSet Examples#Count](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#count)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Count%2A>\-Methode verwendet, um eine Liste der Kontakt\-IDs und der jeweiligen Anzahl von Aufträgen zu erstellen.  
  
 [!code-csharp[DP LINQ to DataSet Examples#CountNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#countnested)]
 [!code-vb[DP LINQ to DataSet Examples#CountNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#countnested)]  
  
### Beispiel  
 In diesem Beispiel werden die Produkte nach ihrer Farbe gruppiert. Anschließend wird die <xref:System.Linq.Enumerable.Count%2A>\-Methode verwendet, um die Anzahl der Produkte in jeder Farbgruppe abzurufen.  
  
 [!code-csharp[DP LINQ to DataSet Examples#CountGrouped](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#countgrouped)]
 [!code-vb[DP LINQ to DataSet Examples#CountGrouped](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#countgrouped)]  
  
## LongCount  
  
### Beispiel  
 In diesem Beispiel wird die Anzahl der Kontakte als lange ganze Zahl abgerufen.  
  
 [!code-csharp[DP LINQ to DataSet Examples#LongCountSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#longcountsimple)]
 [!code-vb[DP LINQ to DataSet Examples#LongCountSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#longcountsimple)]  
  
## Max  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Max%2A>\-Methode verwendet, um den größten fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#MaxProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#maxprojection_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MaxProjection_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#maxprojection_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Max%2A>\-Methode verwendet, um für jede Kontakt\-ID den größten fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#MaxGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#maxgrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MaxGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#maxgrouped_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Max%2A>\-Methode verwendet, um für jede Kontakt\-ID die Aufträge mit dem größten `TotalDue`\-Wert abzurufen.  
  
 [!code-csharp[DP LINQ to DataSet Examples#MaxElements_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#maxelements_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MaxElements_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#maxelements_mq)]  
  
## Min  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Min%2A>\-Methode verwendet, um den kleinsten fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#MinProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#minprojection_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MinProjection_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#minprojection_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Min%2A>\-Methode verwendet, um für jede Kontakt\-ID den kleinsten fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#MinGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#mingrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MinGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#mingrouped_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Min%2A>\-Methode verwendet, um für jeden Kontakt die Aufträge mit dem kleinsten fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#MinElements_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#minelements_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MinElements_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#minelements_mq)]  
  
## Summe  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Sum%2A>\-Methode verwendet, um die Gesamtzahl der Bestellmengen in der `SalesOrderDetail`\-Tabelle abzurufen.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SumProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#sumprojection_mq)]  
  
### Beispiel  
 In diesem Beispiel wird die <xref:System.Linq.Enumerable.Sum%2A>\-Methode verwendet, um für jede Kontakt\-ID den fälligen Gesamtbetrag zu ermitteln.  
  
 [!code-csharp[DP LINQ to DataSet Examples#SumGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#sumgrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SumGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#sumgrouped_mq)]  
  
## Siehe auch  
 [Laden von Daten in ein 'DataSet'](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md)   
 [LINQ to DataSet\-Beispiele](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)   
 [Standard Query Operators Overview](../../../../ocs/visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)