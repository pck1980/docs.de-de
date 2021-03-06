---
title: "Introduction to Windows Service Applications | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ServiceController"
helpviewer_keywords: 
  - "Windows Service applications, deploying"
  - "OnStop method"
  - "OnPause method"
  - "services, about services"
  - "Service class, Windows Service applications"
  - "framework services, creating services"
  - "ServiceController components, about Windows services"
  - "Win32OwnProcess service type"
  - "services, lifetime"
  - "OnContinue method"
  - "Windows Service applications, about Windows Service applications"
  - "services, states"
  - "service states"
  - "WaitForStatus method"
  - "Win32ShareProcess service type"
  - "Windows Service applications, lifetime"
ms.assetid: 1b1b5e67-3ff3-40c0-8154-322cfd6ef0ae
caps.latest.revision: 17
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 17
---
# Introduction to Windows Service Applications
Mit Microsoft Windows\-Diensten, früher als NT\-Dienste bekannt, wird das Erstellen von ausführbaren Anwendungen mit langer Laufzeit ermöglicht, die in eigenen Windows\-Sitzungen ausgeführt werden.  Die Dienste können automatisch gestartet werden, sobald der Computer gestartet wird. Sie können angehalten und neu gestartet werden. Es wird jedoch keine Benutzeroberfläche angezeigt.  Dienste eignen sich mit diesen Features ideal zur Verwendung auf einem Server. Sie sind darüber hinaus für alle Fälle geeignet, in denen Funktionen mit langer Laufzeit benötigt werden und Benutzer, die am gleichen Computer arbeiten, nicht gestört werden sollen.  Dienste können auch im Sicherheitskontext eines bestimmten Benutzerkontos ausgeführt werden, bei dem es sich nicht um einen angemeldeten Benutzer oder das Standardcomputerkonto handelt.  Weitere Informationen zu Diensten und Windows\-Sitzungen finden Sie in der Windows SDK\-Dokumentation in der MSDN Library.  
  
 Dienste können problemlos erstellt werden, indem eine Anwendung erstellt und als Dienst installiert wird.  Nehmen wir z. B. an, dass Leistungsindikatordaten überwacht werden sollen. Sobald die Werte bestimmte Schwellenwerte erreichen, soll reagiert werden.  So könnte eine Windows\-Dienstanwendung zum Überwachen der Leistungsindikatordaten geschrieben werden, die Anwendung bereitgestellt und anschließend mit dem Sammeln und Analysieren von Daten begonnen werden.  
  
 Der Dienst wird als Microsoft Visual Studio\-Projekt erstellt. In ihm wird Code definiert, von dem gesteuert wird, welche Befehle an den Dienst gesendet werden können. Darüber hinaus wird festgelegt, welche Aktionen durchgeführt werden sollen, sobald diese Befehle empfangen werden.  Zu den Befehlen, die an einen Dienst gesendet werden können, zählen das Starten, Anhalten, Fortsetzen und Beenden des Diensts. Zudem können Sie benutzerdefinierte Befehle ausführen.  
  
 Nachdem die Anwendung erstellt wurde, kann sie installiert werden. Dazu wird das Befehlszeilen\-Hilfsprogramm InstallUtil.exe ausgeführt und der Pfad zur ausführbaren Datei des Diensts übergeben.  Dann kann der Dienst mit dem **Dienststeuerungs\-Manager** gestartet, beendet, angehalten, fortgesetzt und konfiguriert werden.  Viele dieser Aufgaben können auch im **Server\-Explorer** im Knoten **Dienste** oder durch Verwenden der <xref:System.ServiceProcess.ServiceController>\-Klasse ausgeführt werden.  
  
## Dienstanwendungen und andere Visual Studio\-Anwendungen  
 Die Funktionsweise von Dienstanwendungen unterscheidet sich von vielen anderen Projekttypen in mehrfacher Hinsicht:  
  
-   Die kompilierte ausführbare Datei, die von einem Dienstanwendungsprojekt erstellt wird, muss auf dem Server installiert werden. Erst dann kann das Projekt sinnvoll funktionieren.  Das Debuggen oder Ausführen einer Dienstanwendung kann nicht durch Drücken von F5 oder F11 gestartet werden. Ein Dienst kann nicht direkt ausgeführt werden, und es besteht keine Möglichkeit, in den Code zu springen.  Stattdessen muss der Dienst installiert und gestartet werden. Ein Debugger muss an den Prozess des Diensts angehängt werden.  Weitere Informationen finden Sie unter [How to: Debug Windows Service Applications](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md).  
  
-   Im Gegensatz zu einigen Projekttypen müssen für Dienstanwendungen Installationskomponenten erstellt werden.  Mit den Installationskomponenten wird der Dienst auf dem Server installiert und registriert. Zudem wird mit dem **Dienststeuerungs\-Manager** von Windows ein Eintrag für den Dienst erstellt.  Weitere Informationen finden Sie unter [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
-   Von der `Main`\-Methode der Dienstanwendung muss der Befehl zum Ausführen der Dienste erteilt werden, die im Projekt enthalten sind.  Von der `Run`\-Methode werden die Dienste in den **Dienststeuerungs\-Manager** auf dem entsprechenden Server geladen.  Wenn die Projektvorlage für **Windows\-Dienste** verwendet wird, wird diese Methode automatisch geschrieben.  Beachten Sie, dass das Laden eines Diensts und das Starten eines Diensts unterschiedliche Vorgänge darstellen.  Weitere Informationen finden Sie weiter unten unter "Lebensdauer von Diensten".  
  
-   Windows\-Dienstanwendungen werden in einer anderen Windowstation ausgeführt als der interaktiven Station des angemeldeten Benutzers.  Eine Windowstation ist ein sicheres Objekt, das eine Zwischenablage, einen Satz globaler Atome und eine Gruppe von Desktopobjekten enthält.  Da die Station des Windows\-Diensts keine interaktive Station ist, sind aus einem Windows\-Dienst ausgelöste Dialogfelder nicht sichtbar, sodass das Programm möglicherweise nicht mehr reagiert.  Entsprechend ist es notwendig, Fehlermeldungen im Windows\-Ereignisprotokoll zu protokollieren, anstatt sie in der Benutzeroberfläche auszulösen.  
  
     Die von .NET Framework unterstützten Windows\-Dienstklassen unterstützen keine Interaktion mit interaktiven Stationen, das heißt angemeldeten Benutzern.  .NET Framework enthält auch keine Klassen, die Stationen und Desktops enthalten.  Wenn der Windows\-Dienst mit anderen Stationen interagieren muss, müssen Sie auf die nicht verwaltete Windows\-API zugreifen.  Weitere Informationen finden Sie in der Windows SDK\-Dokumentation.  
  
     Die Interaktion des Windows\-Diensts mit dem Benutzer oder anderen Stationen muss sorgfältig entwickelt werden, um Szenarios zu berücksichtigen, wie das Nichtvorhandensein von angemeldeten Benutzern oder Situationen, in denen der Benutzer über eine unerwartete Gruppe von Desktopobjekten verfügt.  In einigen Fällen kann es zweckmäßiger sein, eine Windows\-Anwendung zu schreiben, die durch die Steuerung des Benutzers ausgeführt wird.  
  
-   Windows\-Dienstanwendungen werden in einem eigenen Sicherheitskontext ausgeführt. Sie werden gestartet, bevor sich der Benutzer an dem Windows\-Computer anmeldet, auf dem sie installiert sind.  Es sollte genau geplant werden, in welchem Benutzerkonto ein Dienst ausgeführt wird. Ein Dienst, der unter dem Systemkonto ausgeführt wird, verfügt über mehr Berechtigungen als ein Benutzerkonto.  
  
## Lebensdauer von Diensten  
 Während seiner Lebensdauer durchläuft ein Dienst mehrere interne Statuswerte.  Zuerst wird der Dienst auf dem System installiert, auf dem er ausgeführt werden soll.  Bei diesem Vorgang werden die Installationsprogramme für das Dienstprojekt ausgeführt. Der Dienst wird auf dem Computer in den **Dienststeuerungs\-Manager** geladen.  Der **Dienststeuerungs\-Manager** stellt das zentrale Dienstprogramm dar, das von Windows für die Verwaltung von Diensten bereitgestellt wird.  
  
 Nachdem der Dienst geladen worden ist, muss er gestartet werden,  damit die Funktion des Diensts bereitgestellt wird.  Sie können einen Dienst aus dem **Dienststeuerungs\-Manager**, aus dem **Server\-Explorer** oder aus dem Code starten, indem Sie die <xref:System.ServiceProcess.ServiceController.Start%2A>\-Methode aufrufen.  Die <xref:System.ServiceProcess.ServiceController.Start%2A>\-Methode übergibt die Verarbeitung an die <xref:System.ServiceProcess.ServiceBase.OnStart%2A>\-Methode der Anwendung und verarbeitet den dort definierten Code.  
  
 Ein Dienst, der ausgeführt wird, kann sich beliebig lange in diesem Status befinden, bis er beendet oder angehalten oder der Computer heruntergefahren wird.  Ein Dienst kann einen von drei grundlegenden Zustandswerten aufweisen: <xref:System.ServiceProcess.ServiceControllerStatus>, <xref:System.ServiceProcess.ServiceControllerStatus> oder <xref:System.ServiceProcess.ServiceControllerStatus>.  Der Dienst kann zudem den Zustand eines ausstehenden Befehls melden: <xref:System.ServiceProcess.ServiceControllerStatus>, <xref:System.ServiceProcess.ServiceControllerStatus>, <xref:System.ServiceProcess.ServiceControllerStatus> oder <xref:System.ServiceProcess.ServiceControllerStatus>.  Von diesen Statuswerten wird angezeigt, dass ein Befehl zwar erteilt, aber noch nicht ausgeführt worden ist. Beispielsweise soll ein Dienst angehalten werden, der ausgeführt wird.  Sie können den <xref:System.ServiceProcess.ServiceController.Status%2A> abfragen, um zu bestimmen, in welchem Zustand sich ein Dienst befindet, oder <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A> verwenden, um eine Aktion auszuführen, wenn einer dieser Zustände eintritt.  
  
 Ein Dienst kann angehalten, beendet oder fortgesetzt werden, indem der **Dienststeuerungs\-Manager** oder der **Server\-Explorer** verwendet wird. Außerdem können Methoden programmgesteuert aufgerufen werden.  Von jeder dieser Aktionen kann im Dienst eine zugeordnete Prozedur aufgerufen werden \(<xref:System.ServiceProcess.ServiceBase.OnStop%2A>, <xref:System.ServiceProcess.ServiceBase.OnPause%2A>, oder <xref:System.ServiceProcess.ServiceBase.OnContinue%2A>\), in der Sie eine zusätzliche Verarbeitung definieren können, die ausgeführt werden soll, sobald sich der Zustand eines Diensts ändert.  
  
## Diensttypen  
 In Visual Studio mit .NET Framework können zwei Diensttypen erstellt werden.  Diensten, die den einzigen Dienst in einem Prozess darstellen, wird der Typ <xref:System.ServiceProcess.ServiceType> zugewiesen.  Diensten, die einen Prozess mit einem anderen Dienst gemeinsam verwenden, wird der Typ <xref:System.ServiceProcess.ServiceType> zugewiesen.  Zum Abrufen des Diensttyps fragen Sie die <xref:System.ServiceProcess.ServiceController.ServiceType%2A>\-Eigenschaft ab.  
  
 Möglicherweise werden andere Diensttypen angezeigt, wenn Sie vorhandene Dienste abfragen, die nicht in Visual Studio erstellt wurden.  Weitere Informationen dazu finden Sie unter <xref:System.ServiceProcess.ServiceType>.  
  
## Dienste und die ServiceController\-Komponente  
 Die <xref:System.ServiceProcess.ServiceController>\-Komponente wird verwendet, um die Verbindung zu einem Dienst herzustellen und seinen Zustand zu ändern. Mit einer <xref:System.ServiceProcess.ServiceController>\-Komponente besteht die Möglichkeit, einen Dienst zu starten, zu beenden, anzuhalten und fortzusetzen. Außerdem können benutzerdefinierte Befehle an einen Dienst gesendet werden.  Die <xref:System.ServiceProcess.ServiceController>\-Komponente muss jedoch nicht notwendigerweise verwendet werden, sobald eine Dienstanwendung erstellt wird.  Tatsächlich sollte die <xref:System.ServiceProcess.ServiceController>\-Komponente in den meisten Fällen in einer separaten Anwendung vorhanden sein, nicht in der Windows\-Dienstanwendung, in der der Dienst definiert wird.  
  
 Weitere Informationen finden Sie unter <xref:System.ServiceProcess.ServiceController>.  
  
## Anforderungen  
  
-   Dienste müssen in einem Projekt für **Windows\-Dienst**\-Anwendungen oder einem anderen .NET Framework\-fähigen Projekt erstellt werden. Dieses muss beim Erstellen eine EXE\-Datei erstellen und von der <xref:System.ServiceProcess.ServiceBase>\-Klasse erben.  
  
-   Projekte mit Windows\-Diensten müssen Installationskomponenten für das Projekt und seine Dienste aufweisen.  Dies kann problemlos im **Eigenschaftenfenster** ausgeführt werden.  Weitere Informationen finden Sie unter [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
## Siehe auch  
 [Windows Service Applications](../../../docs/framework/windows-services/index.md)   
 [Service Application Programming Architecture](../../../docs/framework/windows-services/service-application-programming-architecture.md)   
 [How to: Create Windows Services](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)   
 [How to: Start Services](../../../docs/framework/windows-services/how-to-start-services.md)   
 [How to: Debug Windows Service Applications](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)   
 [Walkthrough: Creating a Windows Service Application in the Component Designer](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)   
 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)