---
title: "Ausf&#252;hren von Batchoperationen mit DataAdapters | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Ausf&#252;hren von Batchoperationen mit DataAdapters
Durch Batch\-Unterstützung in ADO.NET kann ein <xref:System.Data.Common.DataAdapter> die Operationen INSERT, UPDATE und DELETE aus einem <xref:System.Data.DataSet> oder einer <xref:System.Data.DataTable> an einen Server zusammenfassen, anstatt nur jeweils eine Operation senden zu können.  Durch das Reduzieren der Anzahl von Roundtrips zum Server kann im Allgemeinen die Leistung beträchtlich gesteigert werden.  Batchupdates werden für die .NET\-Datenanbieter für SQL Server \(<xref:System.Data.SqlClient>\) und Oracle \(<xref:System.Data.OracleClient>\) unterstützt.  
  
 Beim Aktualisieren einer Datenbank mit Änderungen aus einem <xref:System.Data.DataSet> wurde die Datenbank in früheren Versionen von ADO.NET mit der `Update`\-Methode eines `DataAdapter` zeilenweise aktualisiert.  Dabei wurden die Zeilen in der angegebenen <xref:System.Data.DataTable> durchlaufen, wobei jede <xref:System.Data.DataRow> auf Änderungen geprüft wurde.  Wenn die Zeile geändert worden war, wurde, abhängig vom Wert der <xref:System.Data.DataRow.RowState%2A>\-Eigenschaft für die Zeile, der entsprechende `UpdateCommand`, `InsertCommand` oder `DeleteCommand` aufgerufen.  Für jede Zeilenaktualisierung war ein Netzwerkroundtrip zur Datenbank erforderlich.  
  
 Beginnend mit ADO.NET 2.0 wird vom <xref:System.Data.Common.DbDataAdapter>\-Objekt eine <xref:System.Data.Common.DbDataAdapter.UpdateBatchSize%2A>\-Eigenschaft verfügbar gemacht.  Wenn die `UpdateBatchSize`\-Eigenschaft auf einen positiven ganzzahligen Wert festgelegt wird, werden Updates der Datenbank als Batches mit der angegebenen Größe gesendet.  Wenn z. B. für `UpdateBatchSize` der Wert 10 festgelegt wird, bedeutet dies, dass jeweils 10 Anweisungen in einer Gruppe zusammengefasst und zusammen als Batch gesendet werden.  Wird dagegen für `UpdateBatchSize` 0 festgelegt, verwendet der <xref:System.Data.Common.DataAdapter> die größtmöglichen Batches, die der Server unterstützt.  Bei einem Wert von 1 werden Batchupdates deaktiviert, weil die Zeilen einzeln nacheinander gesendet werden.  
  
 Die Ausführung eines extrem großen Batches könnte die Leistung verringern.  Daher sollten Sie die Einstellung für eine optimale Batchgröße vor der Implementierung Ihrer Anwendung austesten.  
  
## Verwenden der "UpdateBatchSize"\-Eigenschaft  
 Wenn Batchupdates aktiviert sind, sollte der <xref:System.Data.IDbCommand.UpdatedRowSource%2A>\-Eigenschaftswert von `UpdateCommand`, `InsertCommand` und `DeleteCommand` des DataAdapter auf <xref:System.Data.UpdateRowSource> oder <xref:System.Data.UpdateRowSource> festgelegt werden.  Beim Update eines Batches sind der <xref:System.Data.UpdateRowSource>\-Wert und der <xref:System.Data.UpdateRowSource>\-Wert der <xref:System.Data.IDbCommand.UpdatedRowSource%2A>\-Eigenschaft des Befehls ungültig.  
  
 In der folgenden Prozedur wird die Verwendung der `UpdateBatchSize`\-Eigenschaft veranschaulicht.  Die Prozedur akzeptiert zwei Argumente: ein <xref:System.Data.DataSet>\-Objekt mit Spalten für das **ProductCategoryID**\-Feld und das **Name**\-Feld in der **Production.ProductCategory**\-Tabelle und eine ganze Zahl, die die Batchgröße \(die Anzahl der Zeilen im Batch\) darstellt.  Der Code erstellt ein neues <xref:System.Data.SqlClient.SqlDataAdapter>\-Objekt und legt dessen Eigenschaften <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> und <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> fest.  Der Code geht davon aus, dass das <xref:System.Data.DataSet>\-Objekt geänderte Zeilen aufweist.  Er legt einen Wert für die `UpdateBatchSize`\-Eigenschaft fest und führt das Update aus.  
  
```vb  
Public Sub BatchUpdate( _  
  ByVal dataTable As DataTable, ByVal batchSize As Int32)  
    ' Assumes GetConnectionString() returns a valid connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    ' Connect to the AdventureWorks database.  
    Using connection As New SqlConnection(connectionString)  
        ' Create a SqlDataAdapter.  
        Dim adapter As New SqlDataAdapter()  
  
        'Set the UPDATE command and parameters.  
        adapter.UpdateCommand = New SqlCommand( _  
          "UPDATE Production.ProductCategory SET " _  
          & "Name=@Name WHERE ProductCategoryID=@ProdCatID;", _  
          connection)  
        adapter.UpdateCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",  _  
          SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.UpdateCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the INSERT command and parameter.  
        adapter.InsertCommand = New SqlCommand( _  
          "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);", _  
  connection)  
        adapter.InsertCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.InsertCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the DELETE command and parameter.  
        adapter.DeleteCommand = New SqlCommand( _  
          "DELETE FROM Production.ProductCategory " _  
          & "WHERE ProductCategoryID=@ProdCatID;", connection)  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID", _  
           SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None  
  
        ' Set the batch size.  
        adapter.UpdateBatchSize = batchSize  
  
        ' Execute the update.  
        adapter.Update(dataTable)  
    End Using  
End Sub  
```  
  
```csharp  
public static void BatchUpdate(DataTable dataTable,Int32 batchSize)  
{  
    // Assumes GetConnectionString() returns a valid connection string.  
    string connectionString = GetConnectionString();  
  
    // Connect to the AdventureWorks database.  
    using (SqlConnection connection = new   
      SqlConnection(connectionString))  
    {  
  
        // Create a SqlDataAdapter.  
        SqlDataAdapter adapter = new SqlDataAdapter();  
  
        // Set the UPDATE command and parameters.  
        adapter.UpdateCommand = new SqlCommand(  
            "UPDATE Production.ProductCategory SET "  
            + "Name=@Name WHERE ProductCategoryID=@ProdCatID;",   
            connection);  
        adapter.UpdateCommand.Parameters.Add("@Name",   
           SqlDbType.NVarChar, 50, "Name");  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",   
           SqlDbType.Int, 4, "ProductCategoryID");  
         adapter.UpdateCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the INSERT command and parameter.  
        adapter.InsertCommand = new SqlCommand(  
            "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);",   
            connection);  
        adapter.InsertCommand.Parameters.Add("@Name",   
          SqlDbType.NVarChar, 50, "Name");  
        adapter.InsertCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the DELETE command and parameter.  
        adapter.DeleteCommand = new SqlCommand(  
            "DELETE FROM Production.ProductCategory "  
            + "WHERE ProductCategoryID=@ProdCatID;", connection);  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID",   
          SqlDbType.Int, 4, "ProductCategoryID");  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the batch size.  
        adapter.UpdateBatchSize = batchSize;  
  
        // Execute the update.  
        adapter.Update(dataTable);  
    }  
}  
```  
  
## Behandeln von Ereignissen und Fehlern im Zusammenhang mit dem Batchupdate  
 Der **DataAdapter** verfügt über zwei updaterelevante Ereignisse: **RowUpdating** und **RowUpdated**.  In älteren Versionen von ADO.NET werden diese Ereignisse jeweils einmal für jede verarbeitete Zeile generiert, wenn die Batchverarbeitung deaktiviert wurde.  Das **RowUpdating**\-Ereignis wird erstellt, bevor das Update auftritt, und das **RowUpdated**\-Ereignis wird erstellt, nachdem das Datenbankupdate abgeschlossen wurde.  
  
### Änderungen im Ereignisverhalten durch Batchupdates  
 Bei aktivierter Batchverarbeitung werden mehrere Zeilen in einer einzigen Datenbankoperation aktualisiert.  Deshalb findet pro Batch nur ein `RowUpdated`\-Ereignis statt, wohingegen das `RowUpdating`\-Ereignis für jede verarbeitete Zeile auftritt.  Bei deaktivierter Batchverarbeitung werden die beiden Ereignisse mit Einzelverschachtelung ausgelöst, wobei für jede Zeile zunächst ein `RowUpdating`\-Ereignis und dann ein `RowUpdated`\-Ereignis ausgelöst wird. Diese Abfolge der Auslösung von `RowUpdating`\-Ereignissen und `RowUpdated`\-Ereignissen setzt sich so lange fort, bis alle Zeilen verarbeitet wurden.  
  
### Zugreifen auf aktualisierte Zeilen  
 Bei deaktivierter Batchverarbeitung kann auf die zu aktualisierende Zeile mit der <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A>\-Eigenschaft der <xref:System.Data.Common.RowUpdatedEventArgs>\-Klasse zugegriffen werden.  
  
 Bei aktivierter Batchverarbeitung wird für mehrere Zeilen ein einziges `RowUpdated`\-Ereignis generiert.  Daher ist der Wert der `Row`\-Eigenschaft  in jeder Zeile NULL.  Es werden weiterhin `RowUpdating`\-Ereignisse für jede Zeile generiert.  Mit der <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A>\-Methode der <xref:System.Data.Common.RowUpdatedEventArgs>\-Klasse können Sie auf die verarbeiteten Zeilen zugreifen, indem Sie Verweise auf die Zeilen in ein Array kopieren.  Wenn keine Zeilen verarbeitet werden, löst `CopyToRows` eine <xref:System.ArgumentNullException> aus.  Verwenden Sie die <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A>\-Eigenschaft, um vor dem Aufruf der <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A>\-Methode die Anzahl der verarbeiteten Zeilen zurückzugeben.  
  
### Behandeln von Datenfehlern  
 Eine Batchausführung hat dieselben Auswirkungen wie die Ausführung einzelner Anweisungen.  Anweisungen werden in der Reihenfolge ausgeführt, in der sie dem Batch hinzugefügt wurden.  Fehler werden im Batchmodus in derselben Weise behandelt wie bei deaktiviertem Batchmodus.  Jede Zeile wird einzeln verarbeitet.  Nur Zeilen, die erfolgreich in der Datenbank verarbeitet wurden, werden in der entsprechenden <xref:System.Data.DataRow> innerhalb der <xref:System.Data.DataTable> aktualisiert.  
  
 Der Datenanbieter und der Back\-End\-Datenbankserver bestimmen, welche SQL\-Konstrukte für die Batchausführung unterstützt werden.  Wenn eine nicht unterstützte Anweisung ausgeführt werden soll, wird möglicherweise eine Ausnahme ausgelöst.  
  
## Siehe auch  
 [DataAdapter und DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Aktualisieren von Datenquellen mit DataAdapters](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [Umgang mit 'DataAdapter'\-Ereignissen](../../../../docs/framework/data/adonet/handling-dataadapter-events.md)   
 [ADO.NET Verwaltete Anbieter und DataSet\-Entwicklercenter](http://go.microsoft.com/fwlink/?LinkId=217917)