---
title: "Vorgehensweise: Dynamisches Erstellen einer Datenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb7f23c4-4572-4c38-9898-a287807d070c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Vorgehensweise: Dynamisches Erstellen einer Datenbank
In LINQ to SQL wird einer relationalen Datenbank ein Objektmodell zugeordnet.  Das Mapping wird durch attributbasiertes Mapping oder eine externe Mappingdatei zur Beschreibung der Struktur der relationalen Datenbank ermöglicht.  In beiden Szenarien sind genügend Informationen über die relationale Datenbank vorhanden, dass mithilfe der <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=fullName>\-Methode eine neue Instanz der Datenbank erstellt werden kann.  
  
 Die <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=fullName>\-Methode erstellt nur in dem Umfang ein Replikat der Datenbank, in dem Informationen im Objektmodell codiert sind.  Mappingdateien und \-attribute aus dem Objektmodell können möglicherweise nicht alle Informationen zur Struktur einer vorhandenen Datenbank codieren.  Mappinginformationen stellen nicht den Inhalt von benutzerdefinierten Funktionen, gespeicherten Prozeduren, Triggern und CHECK\-Einschränkungen dar.  Dieses Verhalten ist für eine Vielzahl von Datenbanken ausreichend.  
  
 Die <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=fullName>\-Methode kann in einer Vielzahl von Szenarien verwendet werden, insbesondere dann, wenn ein bekannter Datenanbieter wie Microsoft SQL Server 2008 verfügbar ist.  Zu den typischen Szenarien zählen:  
  
-   Sie erstellen eine Anwendung, die sich automatisch auf einem Kundensystem installiert.  
  
-   Sie erstellen eine Clientanwendung, die eine lokale Datenbank benötigt, um den Offlinezustand zu speichern.  
  
 Sie können die <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=fullName>\-Methode auch in Verbindung mit SQL Server nutzen, indem Sie \(je nach Verbindungszeichenfolge\) eine MDF\-Datei oder einen Katalognamen verwenden.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] definiert mithilfe der Verbindungszeichenfolge die zu erstellende Datenbank und den zu verwendenden Server.  
  
> [!NOTE]
>  Falls möglich, sollte die integrierte Sicherheit von Windows für die Verbindung mit der Datenbank verwendet werden, sodass in der Verbindungszeichenfolge keine Kennwörter erforderlich sind.  
  
## Beispiel  
 Der folgende Code bietet ein Beispiel für die Erstellung einer neuen Datenbank mit dem Namen "MyDVDs.mdf".  
  
 [!code-csharp[DLinqSubmittingChanges#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#5)]
 [!code-vb[DLinqSubmittingChanges#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#5)]  
  
## Beispiel  
 Das Objektmodell kann verwendet werden, um wie folgt eine Datenbank zu erstellen:  
  
 [!code-csharp[DLinqSubmittingChanges#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#6)]
 [!code-vb[DLinqSubmittingChanges#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#6)]  
  
## Beispiel  
 Beim Erstellen einer Anwendung, die auf einem Kundensystem automatisch installiert wird, sollte überprüft werden, ob die Datenbank bereits existiert. In diesem Fall sollte sie vor der Erstellung einer neuen Datenbank gelöscht werden.  Die <xref:System.Data.Linq.DataContext>\-Klasse stellt die <xref:System.Data.Linq.DataContext.DatabaseExists%2A>\-Methode und die <xref:System.Data.Linq.DataContext.DeleteDatabase%2A>\-Methode bereit, um diesen Prozess zu vereinfachen.  
  
 Im folgenden Beispiel wird eine Möglichkeit dargestellt, wie diese Methoden verwendet werden können, um diesen Ansatz zu implementieren:  
  
 [!code-csharp[DLinqSubmittingChanges#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#7)]
 [!code-vb[DLinqSubmittingChanges#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#7)]  
  
## Siehe auch  
 [Attributbasierte Zuordnung](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md)   
 [Externe Zuordnung](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md)   
 [SQL CLR\-Typzuordnung](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)   
 [Hintergrundinformationen](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [Vornehmen und Übergeben von Datenänderungen](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)