---
title: "Serialisierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a15ae411-8dc2-4ca3-84d2-01c9d5f1972a
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Serialisierung
In diesem Abschnitt werden die Serialisierungsfähigkeiten von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] beschrieben.  Die folgenden Abschnitte enthalten Informationen zum Hinzufügen von Serialisierung während der Codeerstellung zur Entwicklungszeit sowie zum Serialisierungsverhalten von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Klassen zur Laufzeit.  
  
 Sie können zur Entwurfszeit durch eine der folgenden Methoden Serialisierungscode hinzufügen:  
  
-   Ändern Sie in [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] die **Serialisierungsmodus**\-Eigenschaft in **Unidirektional**.  
  
-   Fügen Sie in der SQLMetal\-Befehlszeile die **\/serialization**\-Option hinzu.  Weitere Informationen finden Sie unter [SqlMetal.exe \(Tool zur Codegenerierung\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Übersicht  
 Der von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] erzeugte Code bietet standardmäßig die Möglichkeit zum verzögerten Laden.  Verzögertes Laden ist auf der Mittelebene eine komfortable Möglichkeit zum transparenten, bedarfsorientierten Laden der Daten.  Bei der Serialisierung kommt es jedoch zu Problemen, da hierbei das verzögerte Laden auch dann ausgelöst wird, wenn dieses nicht beabsichtigt ist.  Wird ein Objekt serialisiert, wird sein transitiver Abschluss unter allen ausgehenden verzögert geladenen Verweisen serialisiert.  
  
 Die [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Serialisierungsfunktion behebt dieses Problem vor allem durch zwei Mechanismen:  
  
-   Ein <xref:System.Data.Linq.DataContext>\-Modus für die Deaktivierung des verzögerten Ladens \(<xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A>\).  Weitere Informationen finden Sie unter <xref:System.Data.Linq.DataContext>.  
  
-   Ein Codegenerierungsschalter zum Erzeugen des <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=fullName>\-Attributs und des <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=fullName>\-Attributs für erzeugte Entitäten.  Dieser Aspekt, einschließlich des Verhaltens von Klassen zum verzögerten Laden im Rahmen der Serialisierung, ist das Hauptthema dieses Abschnitts.  
  
### Definitionen  
  
-   *DataContract Serializer*: Standard\-Serializer der Windows Communication Framework \(WCF\)\-Komponente von .NET Framework 3.0 oder höher.  
  
-   *Unidirektionale Serialisierung*: Die serialisierte Version einer Klasse enthält nur eine Einweg\-Zuordnungseigenschaft \(um einen Zyklus zu vermeiden\).  Laut Konvention wird die Eigenschaft auf der übergeordneten Seite einer primären Fremdschlüsselbeziehung für die Serialisierung markiert.  Die andere Seite in einer bidirektionalen Zuordnung wird nicht serialisiert.  
  
     Unidirektionale Serialisierung ist der einzige Serialisierungstyp, der von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] unterstützt wird.  
  
## Codebeispiel  
 Im folgenden Beispiel werden die herkömmlichen Klassen `Customer` und `Order` aus der Beispieldatenbank Northwind verwendet. Es wird gezeigt, wie diese Klassen mit Serialisierungsattributen versehen werden.  
  
 [!code-csharp[DLinqSerialization#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#1)]
 [!code-vb[DLinqSerialization#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#1)]  
  
 [!code-csharp[DLinqSerialization#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#2)]
 [!code-vb[DLinqSerialization#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#2)]  
  
 [!code-csharp[DLinqSerialization#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#3)]
 [!code-vb[DLinqSerialization#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#3)]  
  
 Für die `Order`\-Klasse im folgenden Beispiel wird aus Gründen der Übersicht nur die umgekehrte Zuordnungseigenschaft entsprechend der `Customer`\-Klasse dargestellt.  Das `DataMember`\-Attribut zur Vermeidung eines Zyklus fehlt.  
  
 [!code-csharp[DLinqSerialization#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#4)]
 [!code-vb[DLinqSerialization#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#4)]  
  
 [!code-csharp[DLinqSerialization#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#5)]
 [!code-vb[DLinqSerialization#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#5)]  
  
### So serialisieren Sie die Entitäten  
 Sie können die Entitäten im Code im vorherigen Abschnitt wie folgt serialisieren:  
  
 [!code-csharp[DLinqSerialization#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/Program.cs#6)]
 [!code-vb[DLinqSerialization#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/Module1.vb#6)]  
  
### Selbstrekursive Beziehungen  
 Selbstrekursive Beziehungen folgen dem gleichen Muster.  Die dem Fremdschlüssel entsprechende Zuordnungseigenschaft weist im Gegensatz zur übergeordneten Eigenschaft kein `DataMember`\-Attribut auf.  
  
 Beachten Sie die folgende Klasse, die über zwei selbstrekursive Beziehungen verfügt: Employee.Manager\/Reports und Employee.Mentor\/Mentees.  
  
 [!code-csharp[DLinqSerialization#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#7)]
 [!code-vb[DLinqSerialization#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#7)]  
  
## Siehe auch  
 [Hintergrundinformationen](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [SqlMetal.exe \(Tool zur Codegenerierung\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)   
 [Vorgehensweise: Aktivieren der Serialisierbarkeit von Entitäten](../../../../../../docs/framework/data/adonet/sql/linq/how-to-make-entities-serializable.md)