---
title: "Benutzerdefinierter sicherer Metadatenendpunkt | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e369e99-ea4a-49ff-aed2-9fdf61091a48
caps.latest.revision: 19
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 19
---
# Benutzerdefinierter sicherer Metadatenendpunkt
In diesem Beispiel wird veranschaulicht, wie ein Dienst mit einem sicheren Metadatenendpunkt, der eine andere Bindung als die Metadatenaustauschbindungen verwendet, implementiert wird und wie [ServiceModel Metadata Utility\-Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) oder Clients zum Abrufen der Metadaten von einem solchen Metadatenendpunkt konfiguriert werden.Es gibt zwei vom System bereitgestellte Bindungen, die für die Bereitstellung von Metadatenendpunkten verfügbar sind: mexHttpBinding and mexHttpsBinding.mexHttpBinding wird verwendet, um einen Metadatenendpunkt über eine nicht sichere Verbindung über HTTP bereitzustellen.mexHttpsBinding wird verwendet, um einen Metadatenendpunkt über eine sichere Verbindung über HTTPS verfügbar zu machen.In diesem Beispiel wird veranschaulicht, wie ein sicherer Metadatenendpunkt mithilfe der <xref:System.ServiceModel.WSHttpBinding> verfügbar gemacht wird.Diese Vorgehensweise eignet sich, wenn Sie die Sicherheitseinstellungen der Bindung ändern, aber nicht HTTPS verwenden möchten.Wenn Sie mexHttpsBinding verwenden, ist der Metadatenendpunkt sicher, die Bindungseinstellungen können jedoch nicht geändert werden.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
## Dienst  
 Der Dienst in diesem Beispiel hat zwei Endpunkte.Der Anwendungsendpunkt wird vom `ICalculator`\-Vertrag auf einer `WSHttpBinding` mit aktivierter `ReliableSession` und einer `Message`\-Sicherheit mit Zertifikaten genutzt.Der Metadatenendpunkt verwendet ebenfalls `WSHttpBinding` mit denselben Sicherheitseinstellungen, jedoch ohne `ReliableSession`.Nachfolgend wird die relevante Konfiguration dargestellt:  
  
```  
<services>  
    …  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
            behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- use base address provided by host -->  
     <endpoint address=""  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding2"  
       contract="Microsoft.ServiceModel.Samples.ICalculator" />  
     <endpoint address="mex"  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding1"  
       contract="IMetadataExchange" />  
     </service>  
 </services>  
 <bindings>  
   <wsHttpBinding>  
     <binding name="Binding1">  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
     <binding name="Binding2">  
       <reliableSession inactivityTimeout="00:01:00" enabled="true" />  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
   </wsHttpBinding>  
 </bindings>  
```  
  
 In vielen der anderen Beispiele verwendet der Metadatenendpunkt die standardmäßige `mexHttpBinding`, die nicht sicher ist.Hier werden die Metadaten durch `WSHttpBinding` mit `Message`\-Sicherheit gesichert.Damit Metadaten\-Clients diese Metadaten abrufen können, müssen sie mit einer übereinstimmenden Bindung konfiguriert werden.In diesem Beispiel werden zwei dieser Clients dargestellt.  
  
 Der erste Client verwendet zum Abrufen der Metadaten und Generieren von Clientcode sowie der Konfiguration zur Entwurfszeit die Datei "Svcutil.exe".Da der Dienst eine nicht standardmäßige Bindung für die Metadaten verwendet, muss das "Svcutil.exe"\-Tool entsprechend konfiguriert werden, sodass es die Metadaten vom Dienst mithilfe dieser Bindung abrufen kann.  
  
 Der zweite Client nutzt `MetadataResolver`, um die Metadaten für einen bekannten Vertrag dynamisch abzurufen und dann Vorgänge auf dem dynamisch generierten Client auszulösen.  
  
## Svcutil\-Client  
 Wenn Sie die Standardbindung zum Hosten des `IMetadataExchange`\-Endpunkts verwenden, können Sie "Svcutil.exe" mit der Adresse dieses Endpunkts ausführen:  
  
```  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 Und es funktioniert.In diesem Beispiel verwendet der Server jedoch einen nicht standardmäßigen Endpunkt, um die Metadaten zu hosten.Deshalb muss "Svcutil.exe" angewiesen werden, die richtige Bindung zu verwenden.Dazu können Sie eine Datei "Svcutil.exe.config" verwenden.  
  
 Die Datei "Svcutil.exe.config" sieht wie eine normale Clientkonfigurationsdatei aus.Die einzigen ungewöhnlichen Aspekte sind der Clientendpunktname und \-vertrag:  
  
```  
<endpoint name="http"  
          binding="wsHttpBinding"  
          bindingConfiguration="Binding1"  
          behaviorConfiguration="ClientCertificateBehavior"  
          contract="IMetadataExchange" />  
```  
  
 Der Endpunktname muss mit dem Namen des Schemas der Adresse übereinstimmen, auf der die Metadaten gehostet sind, und der Endpunktvertrag muss `IMetadataExchange` lauten.Wenn also "Svcutil.exe" mit einer Befehlszeile wie der folgenden ausgeführt wird:  
  
```  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 sucht es nach dem Endpunkt namens "http" und dem Vertrag `IMetadataExchange`, um die Bindung und das Verhalten des Kommunikationsaustauschs mit dem Metadatenendpunkt zu konfigurieren.Der übrige Teil der Datei "Svcutil.exe.config" im Beispiel legt die Bindungskonfiguration und Verhaltensanmeldeinformationen fest, um mit der Konfiguration des Servers für den Metadatenendpunkt übereinzustimmen.  
  
 Damit "Svcutil.exe" die Konfiguration in "Svcutil.exe.config" übernehmen kann, muss sich "Svcutil.exe" im selben Verzeichnis wie die Konfigurationsdatei befinden.Demzufolge müssen Sie "Svcutil.exe" aus seinem Installationsort in das Verzeichnis kopieren, in dem die Datei "Svcutil.exe.config" gespeichert ist.Führen Sie dann in diesem Verzeichnis den folgenden Befehl aus:  
  
```  
.\svcutil.exe http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 Die führende Zeichenfolge ".\\"stellt sicher, dass die Kopie von "Svcutil.exe" in diesem Verzeichnis \(dem Verzeichnis mit einer entsprechenden "Svcutil.exe.config"\) ausgeführt wird.  
  
## MetadataResolver\-Client  
 Wenn der Client zur Entwurfszeit den Vertrag kennt und weiß, wie er mit den Metadaten kommuniziert, kann er mithilfe von `MetadataResolver` die Bindung und Adresse der Anwendungsendpunkte dynamisch herausfinden.Dies wird in diesem Beispielclient dargestellt. Es wird gezeigt, wie die vom `MetadataResolver` verwendete Bindung und die Anmeldeinformationen konfiguriert werden, indem ein `MetadataExchangeClient` erstellt und konfiguriert wird.  
  
 Die Bindungs\- und Zertifikatsinformationen, die in "Svcutil.exe.config" angezeigt wurden, können auf dem `MetadataExchangeClient` zwingend angegeben werden:  
  
```  
// Specify the Metadata Exchange binding and its security mode  
WSHttpBinding mexBinding = new WSHttpBinding(SecurityMode.Message);  
mexBinding.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
// Create a MetadataExchangeClient for retrieving metadata, and set the // certificate details  
MetadataExchangeClient mexClient = new MetadataExchangeClient(mexBinding);  
mexClient.SoapCredentials.ClientCertificate.SetCertificate(    StoreLocation.CurrentUser, StoreName.My,  
    X509FindType.FindBySubjectName, "client.com");  
mexClient.SoapCredentials.ServiceCertificate.Authentication.    CertificateValidationMode =    X509CertificateValidationMode.PeerOrChainTrust;  
mexClient.SoapCredentials.ServiceCertificate.SetDefaultCertificate(    StoreLocation.CurrentUser, StoreName.TrustedPeople,  
    X509FindType.FindBySubjectName, "localhost");  
```  
  
 Nachdem der `mexClient` konfiguriert ist, können Sie die für Sie interessanten Verträge auflisten und `MetadataResolver` verwenden, um eine Liste der Endpunkte mit diesen Verträgen abzurufen:  
  
```  
// The contract we want to fetch metadata for  
Collection<ContractDescription> contracts =    new Collection<ContractDescription>();  
ContractDescription contract =    ContractDescription.GetContract(typeof(ICalculator));  
contracts.Add(contract);  
// Find endpoints for that contract  
EndpointAddress mexAddress = new    EndpointAddress(ConfigurationManager.AppSettings["mexAddress"]);  
ServiceEndpointCollection endpoints =    MetadataResolver.Resolve(contracts, mexAddress, mexClient);  
```  
  
 Abschließend können Sie die Informationen von diesen Endpunkten dazu verwenden, die Bindung und die Adresse einer `ChannelFactory` zu initialisieren, die zum Erstellen von Kanälen für die Kommunikation mit den Anwendungsendpunkten verwendet wird.  
  
```  
ChannelFactory<ICalculator> cf = new    ChannelFactory<ICalculator>(endpoint.Binding, endpoint.Address);  
```  
  
 Als wichtigster Punkt soll in diesem Beispielclient veranschaulicht werden, dass Sie einen `MetadataExchangeClient` zum Festlegen dieser benutzerdefinierten Einstellungen verwenden können, wenn Sie `MetadataResolver` verwenden und benutzerdefinierte Bindungen oder Verhalten für die Metadatenaustauschkommunikation festlegen müssen.  
  
#### So richten Sie das Beispiel ein und erstellen es  
  
1.  Stellen Sie sicher, dass Sie die [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) ausgeführt haben.  
  
2.  Befolgen Sie die Anweisungen unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md), um die Projektmappe zu erstellen.  
  
#### So führen Sie das Beispiel auf demselben Computer aus  
  
1.  Führen Sie "Setup.bat" im Beispielinstallationsordner aus.Hiermit werden alle Zertifikate installiert, die zum Ausführen des Beispiels erforderlich sind.Beachten Sie, dass Setup.bat das Tool "FindPrivateKey.exe" verwendet, das durch Ausführen von "setupCertTool.bat" von [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) aus installiert wird.  
  
2.  Führen Sie die Clientanwendung von "\\MetadataResolverClient\\bin" oder von ""\\SvcutilClient\\bin" aus.In der Clientkonsolenanwendung wird Clientaktivität angezeigt.  
  
3.  Wenn der Client und der Dienst nicht miteinander kommunizieren können, finden Sie weitere Informationen unter [Troubleshooting Tips](http://msdn.microsoft.com/de-de/8787c877-5e96-42da-8214-fa737a38f10b).  
  
4.  Wenn Sie mit dem Beispiel fertig sind, führen Sie die Datei Cleanup.bat aus, um die Zertifikate zu entfernen.In anderen Sicherheitsbeispielen werden die gleichen Zertifikate verwendet.  
  
#### So führen Sie das Beispiel computerübergreifend aus  
  
1.  Führen Sie auf dem Server `setup.bat service` aus.Durch Ausführen von `setup.bat` mit dem Argument `service` wird ein Dienstzertifikat mit dem vollqualifizierten Domänennamen des Computers erstellt und in die Datei Service.cer exportiert.  
  
2.  Bearbeiten Sie auf dem Server die Datei "Web.config", damit sie dem neuen Zertifikatnamen entspricht,Ändern Sie dazu das `findValue`\-Attribut im [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)\-Element so, dass es dem vollqualifizierten Domänennamen des Computers entspricht.  
  
3.  Kopieren Sie die Datei Service.cer aus dem Dienstverzeichnis in das Clientverzeichnis auf dem Clientcomputer.  
  
4.  Führen Sie auf dem Client `setup.bat client` aus.Durch Ausführen von `setup.bat` mit dem Argument `client` wird ein Clientzertifikat mit dem Namen client.com erstellt und in die Datei Client.cer exportiert.  
  
5.  Ändern Sie in der Datei "App.config" des `MetadataResolverClient` auf dem Clientcomputer den Wert für die Adresse des MEX\-Endpunkts, sodass er mit der neuen Adresse des Diensts übereinstimmt.Ersetzen Sie dazu localhost durch den vollqualifizierten Domänennamen des Servers.Ändern Sie auch das Vorkommen von localhost in der Datei "metadataResolverClient.cs" in den neuen Namen des Dienstzertifikats \(den vollqualifizierten Domänennamen des Servers\).Führen Sie denselben Schritt für die Datei "App.config" des "SvcutilClient"\-Projekts aus.  
  
6.  Kopieren Sie die Datei Client.cer aus dem Clientverzeichnis in das Dienstverzeichnis auf dem Server.  
  
7.  Führen Sie auf dem Client `ImportServiceCert.bat` aus.Dadurch wird das Dienstzertifikat aus der Datei Service.cer in den Speicher CurrentUser – TrustedPeople importiert.  
  
8.  Führen Sie auf dem Server `ImportClientCert.bat` aus. Dadurch wird das Clientzertifikat aus der Datei Client.cer in den Speicher LocalMachine – TrustedPeople importiert.  
  
9. Erstellen Sie auf dem Dienstcomputer das Dienstprojekt in Visual Studio, und wählen Sie die Hilfeseite in einem Webbrowser aus, um zu überprüfen, ob sie ausgeführt wird.  
  
10. Führen Sie auf dem Clientcomputer den MetadataResolverClient oder den SvcutilClient von Visual Studio aus.  
  
    1.  Wenn der Client und der Dienst nicht miteinander kommunizieren können, finden Sie weitere Informationen unter [Troubleshooting Tips](http://msdn.microsoft.com/de-de/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### So stellen Sie den Zustand vor Ausführung des Beispiels wieder her  
  
-   Führen Sie Cleanup.bat im Beispielordner aus, nachdem Sie das Beispiel fertig ausgeführt haben.  
  
    > [!NOTE]
    >  Wenn dieses Beispiel computerübergreifend ausgeführt wird, entfernt dieses Skript keine Dienstzertifikate auf einem Client.Wenn Sie [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Beispiele ausgeführt haben, die Zertifikate computerübergreifend verwenden, müssen Sie die Dienstzertifikate entfernen, die im Speicher CurrentUser \- TrustedPeople installiert wurden.Führen Sie dazu folgenden Befehl aus: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`Beispiel: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Metadata\CustomMexEndpoint`  
  
## Siehe auch