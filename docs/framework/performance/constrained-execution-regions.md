---
title: "Constrained Execution Regions | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "constrained execution regions"
  - "CERs"
ms.assetid: 99354547-39c1-4b0b-8553-938e8f8d1808
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Constrained Execution Regions
Ein eingeschränkter Ausführungsbereich \(Constrained Execution Region, CER\) ist Bestandteil eines Mechanismus zum Erstellen von zuverlässigem verwaltetem Code.  Mit einem CER wird ein Bereich definiert, in dem die Common Language Runtime \(CLR\) keine Out\-of\-Band\-Ausnahmen auslösen kann, die verhindern würden, dass der Code in dem Bereich vollständig ausgeführt werden würde.  Benutzercode kann innerhalb dieses Bereichs keinen Code ausführen, der zum Auslösen von Out\-of\-Band\-Ausnahmen führen könnte.  Die <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>\-Methode muss einem `try`\-Block unmittelbar vorangestellt sein. Sie markiert die Blöcke `catch`, `finally` und `fault` als eingeschränkte Anwendungsbereiche.  Wenn Code als eingeschränkter Anwendungsbereich markiert ist, muss er nur anderen Code mit starken Zuverlässigkeitsvereinbarungen aufrufen. Code sollte keine unvorbereiteten oder nicht zuverlässigen Methoden zuordnen oder virtuelle Aufrufe für diese vornehmen, es sei denn, der Code ist für die Behandlung von Fehlern ausgelegt.  Die Common Language Runtime verzögert Threadabbrüche für Code, der in einem eingeschränkten Ausführungsbereich ausgeführt wird.  
  
 Eingeschränkte Ausführungsbereiche werden in der Common Language Runtime auf unterschiedliche Weise als Ergänzung zu einem `try`\-Block verwendet, insbesondere von entscheidenden Finalizern, die in Klassen ausgeführt werden, die von der <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject>\-Klasse abgeleitet sind, und von Code, der über die <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A>\-Methode ausgeführt wird.  
  
## CER\-Vorbereitung  
 Die Common Language Runtime bereitet CERs vorab vor, um Problemen aufgrund von ungenügendem Arbeitsspeicher vorzubeugen.  Dies ist erforderlich, um zu verhindern, dass die Common Language Runtime bei der JIT\-Kompilierung oder beim Laden der Typen einen Arbeitsspeichermangel verursacht.  
  
 Der Entwickler muss anzugeben, dass ein Codebereich ein CER ist:  
  
-   Der oberste CER\-Bereich und die Methoden im vollständigen Aufrufdiagramm, auf die das <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute>\-Attribut angewendet wurde, werden vorab vorbereitet.  Das <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> kann nur Garantien für <xref:System.Runtime.ConstrainedExecution.Cer> oder <xref:System.Runtime.ConstrainedExecution.Cer> angeben.  
  
-   Aufrufe, die nicht statisch ermittelt werden können, z. B. ein virtueller Dispatch, können nicht vorab vorbereitet werden.  Verwenden Sie in diesen Fällen die <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>\-Methode.  Bei der Verwendung der <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A>\-Methode muss das <xref:System.Runtime.ConstrainedExecution.PrePrepareMethodAttribute>\-Attribut auf den Bereinigungscode angewendet werden.  
  
## Einschränkungen  
 Benutzer können in einem CER nur bestimmte Arten von Code schreiben.  Der Code darf keine Out\-of\-Band\-Ausnahme verursachen, die z. B. aufgrund der folgenden Vorgänge auftreten könnten:  
  
-   Explizite Reservierung.  
  
-   Boxing.  
  
-   Erhalten einer Sperre.  
  
-   Virtuelles Aufrufen unvorbereiteter Methoden.  
  
-   Aufrufen von Methoden mit einer schwachen oder nicht vorhandenen Zuverlässigkeitsvereinbarung.  
  
 In .NET Framework, Version 2.0, sind diese Einschränkungen Richtlinien.  Diagnosen werden anhand von Codeanalysetools bereitgestellt.  
  
## Zuverlässigkeitsvereinbarungen  
 Das <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> ist ein benutzerdefiniertes Attribut, das die Zuverlässigkeitsgarantien und den Beschädigungszustand einer bestimmten Methode angibt.  
  
### Zuverlässigkeitsgarantien  
 Durch <xref:System.Runtime.ConstrainedExecution.Cer>\-Enumerationswerte dargestellte Zuverlässigkeitsgarantien geben den Grad der Zuverlässigkeit einer bestimmten Methode an:  
  
-   <xref:System.Runtime.ConstrainedExecution.Cer>.  Die Methode kann unter Ausnahmebedingungen fehlschlagen.  In diesem Fall meldet die Methode der aufrufenden Methode, ob sie erfolgreich ausgeführt wurde oder fehlschlug.  Die Methode muss sich in einem CER befinden, um die Meldung des Rückgabewerts zu gewährleisten.  
  
-   <xref:System.Runtime.ConstrainedExecution.Cer>.  Die Methode, der Typ oder die Assembly steht nicht mit einem CER in Zusammenhang und kann höchstwahrscheinlich ohne wirksame Schutzmaßnahmen vor Zustandsbeschädigungen nicht sicher aus einem CER aufgerufen werden.  CER\-Garantien können nicht genutzt werden.  Dies impliziert Folgendes:  
  
    1.  Die Methode kann unter Ausnahmebedingungen fehlschlagen.  
  
    2.  Die Methoden kann Fehler melden oder nicht melden.  
  
    3.  Die Methode ist nicht für die Verwendung eines CER vorgesehen, der wahrscheinlichste Fall.  
  
    4.  Wenn einer Methode, einem Typ oder einer Assembly nicht explizit Erfolg garantiert wird, wird implizit <xref:System.Runtime.ConstrainedExecution.Cer> erkannt.  
  
-   <xref:System.Runtime.ConstrainedExecution.Cer>.  Die Methode ist unter Ausnahmebedingungen garantiert erfolgreich.  Um eine solche Zuverlässigkeit zu erlangen, müssen Sie immer einen CER um die aufgerufene Methode konstruieren, selbst wenn sie aus einem Bereich aufgerufen wird, der kein CER ist.  Eine Methode ist erfolgreich, wenn sie die vorgegebene Aufgabe erfüllt. Erfolg ist jedoch ein subjektiver Begriff.  Ein Beispiel: Count wird mit `ReliabilityContractAttribute(Cer.Success)` markiert. Dies impliziert, dass bei der Ausführung unter einem CER immer ein Wert für die Anzahl von Elementen in der <xref:System.Collections.ArrayList> zurückgegeben wird und die internen Felder niemals in einem unbestimmten Zustand verbleiben.  Die <xref:System.Threading.Interlocked.CompareExchange%2A>\-Methode ist ebenfalls mit einer Erfolgsgarantie versehen. In diesem Fall kann Erfolg jedoch bedeuten, dass der Wert aufgrund einer Racebedingung nicht durch einen neuen Wert ersetzt werden kann.  Die Methode verhält sich genau wie dokumentiert, und beim Schreiben von CER\-Code muss nicht von außergewöhnlichem Verhalten ausgegangen werden, dass jenseits des Verhaltens von korrektem, aber nicht zuverlässigem Code liegt.  
  
### Beschädigungsstufen  
 Beschädigungsstufen, die durch <xref:System.Runtime.ConstrainedExecution.Consistency>\-Enumerationswerte dargestellt werden, geben an, in welchem Ausmaß der Zustand in einer bestimmten Umgebung beschädigt werden kann:  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>.  Die Common Language Runtime \(CLR\) kann unter Ausnahmebedingungen die Zustandskonsistenz in der aktuellen Anwendungsdomäne nicht garantieren.  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>.  Die Methode beschränkt die Zustandsbeschädigung unter Ausnahmebedingungen garantiert auf die aktuelle Instanz.  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>. Die CLR kann unter Ausnahmebedingungen die Zustandskonsistenz nicht garantieren, d. h., die Bedingung kann den Prozess beschädigen.  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>.  Unter Ausnahmebedingungen beschädigt die Methode den Zustand garantiert nicht.  
  
## Zuverlässiger try\/catch\/finally\-Block  
 Der zuverlässige `try/catch/finally`\-Block ist ein Mechanismus für die Ausnahmebehandlung, dessen Vorhersagbarkeitsgarantie der nicht verwalteten Version entspricht.  Der `catch/finally`\-Block ist der CER.  Die Methoden im Block müssen vorab vorbereitet werden und müssen so angelegt sein, dass sie nicht unterbrochen werden können.  
  
 In .NET Framework, Version 2.0, meldet der Code der Laufzeit, dass ein try\-Block zuverlässig ist, indem er <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> unmittelbar vor diesem aufruft.  <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> ist ein Member von <xref:System.Runtime.CompilerServices.RuntimeHelpers>, einer Unterstützungsklasse für Compiler.  Rufen Sie <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> direkt auf, sofern dies vom Compiler unterstütz wird.  
  
## Nicht unterbrechbare Bereiche  
 In einem nicht unterbrechbaren Bereich wird eine Reihe von Anweisungen zu einem CER gruppiert.  
  
 In .NET Framework, Version 2.0, werden, sofern der Compiler dies unterstützt, im Benutzercode nicht unterbrechbare Bereiche mit einem zuverlässigen try\/catch\/finally\-Block erstellt, das einen leeren try\/catch\-Block enthält, dem ein <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>\-Methodenaufruf vorausgeht.  
  
## Entscheidendes Finalizer\-Objekt  
 Ein <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject> garantiert, dass die Garbage Collection den Finalizer ausführt.  Der Finalizer und sein Aufrufdiagramm werden nach der Reservierung vorab vorbereitet.  Die Finalizermethode wird in einem CER ausgeführt und unterliegt allen Einschränkungen der CERs und Finalizer.  
  
 Für alle Typen, die von <xref:System.Runtime.InteropServices.SafeHandle> und <xref:System.Runtime.InteropServices.CriticalHandle> erben, ist garantiert, dass ihre Finalizer in einem CER ausgeführt werden.  Implementieren Sie <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> in von <xref:System.Runtime.InteropServices.SafeHandle> abgeleiteten Klassen, um Code auszuführen, der das Handle freigeben soll.  
  
## In CERs unzulässiger Code  
 Die folgenden Vorgänge sind in CERs unzulässig:  
  
-   Explizite Reservierungen.  
  
-   Erhalten einer Sperre.  
  
-   Boxing.  
  
-   Mehrdimensionaler Arrayzugriff.  
  
-   Methodenaufrufe durch Reflektion.  
  
-   <xref:System.Threading.Monitor.Enter%2A> oder <xref:System.IO.FileStream.Lock%2A>.  
  
-   Sicherheitsüberprüfungen.  Führen Sie keine Anforderungen, sondern nur Linkaufrufe aus.  
  
-   <xref:System.Reflection.Emit.OpCodes.Isinst> und <xref:System.Reflection.Emit.OpCodes.Castclass> für COM\-Objekte und Proxys  
  
-   Abrufen oder Festlegen von Feldern für einen transparenten Proxy.  
  
-   Serialisierung.  
  
-   Funktionszeiger und \-delegaten.  
  
## Siehe auch  
 [Reliability Best Practices](../../../docs/framework/performance/reliability-best-practices.md)