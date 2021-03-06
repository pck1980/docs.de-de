---
title: "Benutzerdefinierte SendMail-Aktivit&#228;t | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 947a9ae6-379c-43a3-9cd5-87f573a5739f
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Benutzerdefinierte SendMail-Aktivit&#228;t
In diesem Beispiel wird das Erstellen einer benutzerdefinierten Aktivität veranschaulicht, die von der <xref:System.Activities.AsyncCodeActivity> abgeleitet wird, um E\-Mail\-Nachrichten zur Verwendung in einer Workflowanwendung via SMTP zu senden.Die benutzerdefinierte Aktivität verwendet die Funktionen des <xref:System.Net.Mail.SmtpClient>, um E\-Mail\-Nachrichten asynchron und mit Authentifizierung zu senden.Außerdem werden Endbenutzerfunktionen wie Testmodus, Tokenersetzung, Dateivorlagen und Testablagepfad bereitgestellt.  
  
 In der folgenden Tabelle werden die Argumente für die `SendMail`\-Aktivität aufgelistet.  
  
||||  
|-|-|-|  
|Name|Typ|Beschreibung|  
|Host|String|Die Adresse des SMTP\-Serverhosts.|  
|Port|String|Der Port des SMTP\-Diensts auf dem Host.|  
|EnableSsl|bool|Gibt an, ob der <xref:System.Net.Mail.SmtpClient> die Verbindung mit SSL \(Secure Sockets Layer\) verschlüsselt.|  
|UserName|String|Der Benutzername zum Einrichten der Anmeldeinformationen und Authentifizieren der <xref:System.Net.Mail.SmtpClient.Credentials%2A>\-Absendereigenschaft.|  
|Password|String|Das Kennwort zum Einrichten der Anmeldeinformationen und Authentifizieren der <xref:System.Net.Mail.SmtpClient.Credentials%2A>\-Absendereigenschaft.|  
|Subject|<xref:System.Activities.InArgument%601>\<string\>|Der Betreff der Nachricht.|  
|Body|<xref:System.Activities.InArgument%601>\<string\>|Der Nachrichtentext.|  
|Attachments|<xref:System.Activities.InArgument%601>\<string\>|Die Anlagenauflistung, die zum Speichern der an diese E\-Mail\-Nachricht angefügten Daten verwendet wird.|  
|From|<xref:System.Net.Mail.MailAddress>|Die Absenderadresse für die E\-Mail\-Nachricht.|  
|To|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|Die Adressenauflistung, die die Empfänger dieser E\-Mail\-Nachricht enthält.|  
|CC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|Die Adressenauflistung, die die Cc\-Empfänger für diese E\-Mail\-Nachricht enthält.|  
|BCC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|Die Adressenauflistung, die die Bcc\-Empfänger für diese E\-Mail\-Nachricht enthält.|  
|Tokens|<xref:System.Activities.InArgument%601>\<IDictionary\<string, string\>\>|Diese Token können im Text ersetzt werden.Mithilfe dieser Funktion können Benutzer bestimmte Werte im Text verwenden, die später durch Tokens ersetzt werden können, die mit dieser Eigenschaft angegeben werden.|  
|BodyTemplateFilePath|String|Der Pfad einer Vorlage für den Text.Mit der `SendMail`\-Aktivität wird der Inhalt dieser Datei in die body\-Eigenschaft kopiert.<br /><br /> Die Vorlage kann Token enthalten, die durch den Inhalt der Tokeneigenschaft ersetzt werden.|  
|TestMailTo|<xref:System.Net.Mail.MailAddress>|Wenn diese Eigenschaft festgelegt wurde, werden alle E\-Mail\-Nachrichten an die darin angegebene Adresse gesendet.<br /><br /> Diese Eigenschaft ist für das Testen von Workflows vorgesehen.Beispielsweise können Sie auf diese Weise sicherstellen, dass alle E\-Mails gesendet, nicht jedoch tatsächlich den Empfängern zugestellt werden.|  
|TestDropPath|String|Wenn diese Eigenschaft festgelegt wurde, werden alle E\-Mail\-Nachrichten zusätzlich in der angegebenen Datei gespeichert.<br /><br /> Diese Eigenschaft ist für das Testen oder Debuggen von Workflows vorgesehen, um sicherzustellen, dass Format und Inhalt der ausgehenden E\-Mail\-Nachrichten geeignet sind.|  
  
## Inhalt der Projektmappe  
 Die Projektmappe enthält zwei Projekte.  
  
|Projekt|Beschreibung|Wichtige Dateien|  
|-------------|------------------|----------------------|  
|SendMail|Die SendMail\-Aktivität|1.  SendMail.cs: Implementierung für die Hauptaktivität<br />2.  SendMailDesigner.xaml und SendMailDesigner.xaml.cs: Designer für die SendMail\-Aktivität<br />3.  MailTemplateBody.htm: Vorlage für die zu sendende E\-Mail\-Nachricht.|  
|SendMailTestClient|Ein Client zum Testen der SendMail\-Aktivität.In diesem Projekt werden zwei Möglichkeiten zum Aufrufen der SendMail\-Aktivität veranschaulicht: deklarativ und programmgesteuert.|1.  Sequence1.xaml: Workflow zum Aufrufen der SendMail\-Aktivität.<br />2.  Program.cs: ruft Sequence1 auf und erstellt programmgesteuert einen Workflow mit SendMail.|  
  
## Weitere Konfiguration der SendMail\-Aktivität  
 Benutzer können weitere Konfigurationen für die SendMail\-Aktivität angeben, die in diesem Beispiel nicht gezeigt werden.Dies wird in den folgenden drei Abschnitten veranschaulicht.  
  
### Senden einer E\-Mail\-Nachricht mit Token im Text  
 Mit diesem Codeausschnitt wird veranschaulicht, wie Sie eine E\-Mail\-Nachricht mit Token im Text senden können.Die Token werden in der body\-Eigenschaft bereitgestellt.Die Werte für die Token werden in der Tokeneigenschaft bereitgestellt.  
  
```html  
IDictionary<string, string> tokens = new Dictionary<string, string>();  
tokens.Add("@name", "John Doe");  
tokens.Add("@date", DateTime.Now.ToString());  
tokens.Add("@server", "localhost");  
  
new SendMail  
{  
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Body = "Hello @name. This is a test email sent from @server. Current date is @date",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens)  
};  
  
```  
  
### Senden einer E\-Mail\-Nachricht mit einer Vorlage  
 Mit diesem Codeausschnitt wird veranschaulicht, wie Sie eine E\-Mail\-Nachricht mit Vorlagentoken im Text senden können.Beachten Sie, dass beim Festlegen der `BodyTemplateFilePath`\-Eigenschaft kein Wert für die body\-Eigenschaft angegeben werden muss \(der Inhalt der Vorlagendatei wird in den Text kopiert\).  
  
```  
new SendMail  
{    
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
    BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",   
};  
  
```  
  
### Senden von E\-Mails im Testmodus  
 Mit diesem Codeausschnitt wird das Festlegen der beiden Testeigenschaften veranschaulicht: Durch Festlegen von `TestMailTo` für alle Nachrichten werden diese \(ohne Beachtung der Werte von To, Cc und Bcc\) an john.doe@contoso.com gesendet.Durch Festlegen von TestDropPath werden alle ausgehenden E\-Mail\-Nachrichten außerdem unter dem angegebenen Pfad gespeichert.Diese Eigenschaften können unabhängig voneinander festgelegt werden \(sie sind nicht verknüpft\).  
  
```  
new SendMail  
{    
   From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
   Subject = "Test email",  
   Host = "localhost",  
   Port = 25,  
   Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
   BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",  
   TestMailTo= new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   TestDropPath = @"c:\Samples\SendMail\TestDropPath\",  
};  
  
```  
  
## Setupanweisungen  
 Um dieses Beispiel ausführen zu können, ist der Zugriff auf einen SMTP\-Server erforderlich.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] das Einrichten eines SMTP\-Servers finden Sie unter den folgenden Links.  
  
-   [Microsoft Technet](http://go.microsoft.com/fwlink/?LinkId=166060)  
  
-   [Konfigurieren des SMTP\-Diensts \(IIS 6.0\)](http://go.microsoft.com/fwlink/?LinkId=150456)  
  
-   [IIS 7.0: Konfigurieren von SMTP\-E\-Mail](http://go.microsoft.com/fwlink/?LinkId=150457)  
  
-   [Installieren des SMTP\-Diensts](http://go.microsoft.com/fwlink/?LinkId=150458)  
  
 SMTP\-Emulatoren können von Drittanbietern heruntergeladen werden.  
  
##### So führen Sie dieses Beispiel aus  
  
1.  Öffnen Sie mit [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] die Projektmappendatei SendMail.sln.  
  
2.  Stellen Sie sicher, dass sie auf einen funktionierenden SMTP\-Server zugreifen können.Beachten Sie dazu die Setupanweisungen.  
  
3.  Konfigurieren Sie das Programm mit der Serveradresse sowie den E\-Mail\-Adressen von Absender und Empfänger.  
  
     Um dieses Beispiel ordnungsgemäß ausführen zu können, müssen Sie möglicherweise noch den Wert für die E\-Mail\-Adresse von Absender und Empfänger sowie die Adresse des SMTP\-Servers in Program.cs und Sequence.xaml konfigurieren.Die Adressen müssen an beiden Speicherorten geändert werden, da das Programm E\-Mail\-Nachrichten auf unterschiedliche Weise sendet.  
  
4.  Drücken Sie STRG\+UMSCHALT\+B, um die Projektmappe zu erstellen.  
  
5.  Drücken Sie STRG\+F5, um die Projektmappe auszuführen.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SendMail`  
  
## Siehe auch