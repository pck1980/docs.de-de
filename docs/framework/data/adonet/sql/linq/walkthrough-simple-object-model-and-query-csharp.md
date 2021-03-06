---
title: "Exemplarische Vorgehensweise: Einfaches Objektmodell und Abfrage (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 419961cc-92d6-45f5-ae8a-d485bdde3a37
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Exemplarische Vorgehensweise: Einfaches Objektmodell und Abfrage (C#)
Diese exemplarische Vorgehensweise stellt ein grundlegendes End\-to\-End\-Szenario für [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] mit minimaler Komplexität bereit. Sie erstellen eine Entitätsklasse, die die Customers\-Tabelle in der Beispieldatenbank Northwind modelliert.  Sie erstellen dann eine einfache Abfrage, um Kunden aus London aufzulisten.  
  
 Diese exemplarische Vorgehensweise ist codeorientiert, um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Konzepte zu verdeutlichen.  In der Regel verwenden Sie [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] zum Erstellen des Objektmodells.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Diese exemplarische Vorgehensweise wurde mithilfe von Visual C\#\-Entwicklungseinstellungen geschrieben.  
  
## Vorbereitungsmaßnahmen  
  
-   Diese exemplarische Vorgehensweise verwendet einen dedizierten Ordner \("c:\\linqtest5"\) als Speicherort für Dateien.  Erstellen Sie diesen Ordner, bevor Sie die exemplarische Vorgehensweise starten.  
  
-   Für dieses Beispiel wird die Beispieldatenbank Northwind benötigt.  Befindet sich diese Datenbank nicht auf Ihrem Entwicklungscomputer, können Sie diese von der Microsoft Downloadsite herunterladen.  Anweisungen hierzu finden Sie unter [Herunterladen von Beispieldatenbanken](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  Nachdem Sie die Datenbank heruntergeladen haben, kopieren Sie die Datei in den Ordner c:\\linqtest5.  
  
## Übersicht  
 Diese exemplarische Vorgehensweise umfasst sechs Hauptaufgaben:  
  
-   Erstellen einer [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Lösung in [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
-   Zuordnen einer Datenbanktabelle zu einer Klasse.  
  
-   Festlegen von Eigenschaften für die Klasse, um Datenbankspalten darzustellen.  
  
-   Herstellen einer Verbindung zur Beispieldatenbank Northwind.  
  
-   Erstellen einer einfachen Abfrage der Datenbank.  
  
-   Ausführen der Abfrage und Prüfen der Ergebnisse  
  
## Erstellen einer LINQ to SQL\-Lösung  
 In dieser ersten Aufgabe erstellen Sie eine [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]\-Lösung, die die erforderlichen Verweise zur Erstellung und Ausführung eines [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-Projekts enthält.  
  
#### So erstellen Sie eine LINQ to SQL\-Lösung  
  
1.  Zeigen Sie im [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]\-Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**.  
  
2.  Klicken Sie im Bereich **Projekttypen** des Dialogfelds **Neues Projekt** auf **Visual C\#**.  
  
3.  Klicken Sie im Bereich **Vorlagen** auf **Konsolenanwendung**.  
  
4.  Geben Sie im Feld **Name** die Zeichenfolge LinqConsoleApp ein.  
  
5.  Geben Sie im Feld **Position** an, wo die Projektdateien gespeichert werden sollen.  
  
6.  Klicken Sie auf **OK**.  
  
## Hinzufügen von LINQ\-Verweisen und Richtlinien  
 Diese exemplarische Vorgehensweise verwendet Assemblys, die im Projekt u. U. nicht standardmäßig installiert sind.  Wird System.Data.Linq in Ihrem Projekt nicht als Verweis aufgeführt \(erweitern Sie den Knoten **Verweise** im **Lösungs\-Explorer**\), fügen Sie diesen wie nachfolgend beschrieben hinzu.  
  
#### So fügen Sie System.Data.Linq hinzu  
  
1.  Klicken Sie im **Projektmappen\-Explorer** mit der rechten Maustaste auf **Verweise**, und klicken Sie dann auf **Verweis hinzufügen**.  
  
2.  Klicken Sie im Dialogfeld **Verweis hinzufügen** auf **.NET**, klicken Sie auf die System.Data.Linq\-Assembly und dann auf **OK**.  
  
     Dem Projekt wird die Assembly hinzugefügt.  
  
3.  Fügen Sie die folgenden Direktiven am oberen Rand von **Program.cs** hinzu:  
  
     [!code-csharp[DLinqWalk1CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#1)]  
  
## Zuordnen einer Klasse zu einer Datenbanktabelle.  
 In diesem Schritt erstellen Sie eine Klasse und ordnen diese einer Datenbanktabelle zu.  Eine solche Klasse wird *Entitätsklasse* genannt.  Beachten Sie, dass die Zuordnung durch Hinzufügen des <xref:System.Data.Linq.Mapping.TableAttribute>\-Attributs erreicht wird.  Die <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A>\-Eigenschaft gibt den Namen der Tabelle in der Datenbank an.  
  
#### So erstellen Sie eine Entitätsklasse und weisen diese einer Datenbanktabelle zu  
  
-   Geben Sie den folgenden Code direkt oberhalb der `Program`\-Klassendeklaration in Program.cs ein, oder fügen Sie ihn ein:  
  
     [!code-csharp[DLinqWalk1CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#2)]  
  
## Festlegen von Eigenschaften für die Klasse, um Datenbankspalten darzustellen  
 In diesem Schritt erledigen Sie mehrere Aufgaben.  
  
-   Sie verwenden das <xref:System.Data.Linq.Mapping.ColumnAttribute>\-Attribut, um die `CustomerID`\-Eigenschaft und die `City`\-Eigenschaft der Entitätsklasse für die Darstellung von Spalten in der Datenbanktabelle festzulegen.  
  
-   Sie legen die `CustomerID`\-Eigenschaft zur Darstellung einer Primärschlüsselspalte in der Datenbank fest.  
  
-   Sie legen `_CustomerID`\- und `_City`\-Felder für den privaten Speicher fest.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] kann Werte dann direkt speichern und abrufen, statt öffentliche Accessoren zu verwenden, die möglicherweise Geschäftslogik umfassen.  
  
#### So stellen Sie Eigenschaften von zwei Datenbankspalten dar  
  
-   Geben Sie den folgenden Code in die geschweiften Klammern der `Customer`\-Klasse in Program.cs ein, oder fügen Sie ihn ein.  
  
     [!code-csharp[DLinqWalk1CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#3)]  
  
## Herstellen einer Verbindung zur Beispieldatenbank Northwind  
 In diesem Schritt verwenden Sie ein <xref:System.Data.Linq.DataContext>\-Objekt zur Einrichtung einer Verbindung zwischen Ihren codebasierten Datenstrukturen und der Datenbank selbst.  Der <xref:System.Data.Linq.DataContext> ist der Hauptkanal, durch den Sie Objekte von der Datenbank abrufen und Änderungen übergeben.  
  
 Sie deklarieren außerdem eine `Table<Customer>` als logische, typisierte Tabelle für Ihre Abfragen der Customers\-Tabelle in der Datenbank.  Die Erstellung und Ausführung dieser Abfragen erfolgt später.  
  
#### So definieren Sie die Datenbankverbindung  
  
-   Geben Sie den folgenden Code in die `Main`\-Methode ein, oder fügen Sie ihn ein:  
  
     Beachten Sie, dass die Datei `northwnd.mdf` im Ordner linqtest5 angenommen wird.  Weitere Informationen finden Sie im Abschnitt zu Voraussetzungen weiter oben in dieser exemplarischen Vorgehensweise.  
  
     [!code-csharp[DLinqWalk1CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#4)]  
  
## Erstellen einer einfachen Abfrage  
 In diesem Schritt erstellen Sie eine Abfrage, um zu ermitteln, welche Kunden in der Customers\-Datenbanktabelle aus London stammen.  Im Abfragecode in diesem Schritt wird nur die Abfrage beschrieben.  Die Abfrage wird nicht ausgeführt.  Dieser Ansatz wird als *verzögerte Ausführung* bezeichnet.  Weitere Informationen hierzu finden Sie unter [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md).  
  
 Sie erzeugen auch eine Protokollausgabe, um die SQL\-Befehle anzuzeigen, die [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] erzeugt.  Diese Protokolllierungsfunktion \(die <xref:System.Data.Linq.DataContext.Log%2A> verwendet\), eignet sich für das Debugging. Sie stellt außerdem sicher, dass die an die Datenbank übergebenen Befehle Ihre Abfrage genau wiedergeben.  
  
#### So erstellen Sie eine einfache Abfrage  
  
-   Geben Sie den folgenden Code in die `Main`\-Methode nach der `Table<Customer>`\-Deklaration ein, oder fügen Sie ihn ein:  
  
     [!code-csharp[DLinqWalk1ACS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#5)]  
  
## Ausführen der Abfrage  
 In diesem Schritt führen Sie die Abfrage aus.  Die in den vorherigen Schritten erstellten Abfrageausdrücke werden erst ausgewertet, wenn die Ergebnisse benötigt werden.  Wenn Sie die `foreach`\-Iteration beginnen, wird ein SQL\-Befehl in der Datenbank ausgeführt, und Objekte werden erstellt.  
  
#### So führen Sie die Abfrage aus  
  
1.  Geben Sie den folgenden Code am Ende der `Main`\-Methode \(nach der Abfragebeschreibung\) ein. oder fügen Sie ihn ein:  
  
     [!code-csharp[DLinqWalk1ACS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#6)]  
  
2.  Drücken Sie F5, um die Anwendung zu debuggen.  
  
    > [!NOTE]
    >  Wenn die Anwendung einen Laufzeitfehler erzeugt, lesen Sie den Abschnitt zur Problembehandlung unter [Lernen mit exemplarischen Vorgehensweisen](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md).  
  
     Die Abfrageergebnisse im Konsolenfenster werden wie folgt angezeigt:  
  
     `ID=AROUT, City=London`  
  
     `ID=BSBEV, City=London`  
  
     `ID=CONSH, City=London`  
  
     `ID=EASTC, City=London`  
  
     `ID=NORTS, City=London`  
  
     `ID=SEVES, City=London`  
  
3.  Drücken Sie die EINGABETASTE im Konsolenfenster, um die Anwendung zu schließen.  
  
## Nächste Schritte  
 Das Thema [Exemplarische Vorgehensweise: Beziehungsübergreifende Abfragen \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-csharp.md) beginnt an der Stelle, an der diese exemplarischen Vorgehensweise endet.  Die exemplarische Vorgehensweise zu beziehungsübergreifenden Abfragen zeigt, wie [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tabellenübergreifende Abfragen ausführt, ähnlich wie *Joins* in einer relationalen Datenbank.  
  
 Wenn Sie die exemplarische Vorgehensweise zu beziehungsübergreifenden Abfragen absolvieren möchten, stellen Sie sicher, dass Sie die gerade erstellte Lösung speichern, da diese benötigt wird.  
  
## Siehe auch  
 [Lernen mit exemplarischen Vorgehensweisen](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)