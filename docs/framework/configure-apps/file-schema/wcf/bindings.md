---
title: "&lt;Bindungen&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b62cd369-5409-4030-8490-9759a462dd3a
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;Bindungen&gt;
Dieser Abschnitt enthält eine Auflistung von standardmäßigen und benutzerdefinierten Bindungen.  Jeder Eintrag ist ein `binding`\-Element, das anhand seines eindeutigen `name` identifiziert werden kann.  Dienste verwenden Bindungen, indem sie sie mithilfe des `name` verknüpfen.  Ab [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] müssen Bindungen und Verhalten keinen Namen aufweisen.  Weitere Informationen zu Standardkonfiguration und zu namenlosen Bindungen und Verhalten finden Sie unter [Vereinfachte Konfiguration](../../../../../docs/framework/wcf/simplified-configuration.md) und [Vereinfachte Konfiguration für WCF\-Dienste](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## Vom System bereitgestellte Bindung  
 Vom System bereitgestellte Bindungen verbergen die Komplexität der WCF\-Messagingstapel.  Anwendungen, die vom System bereitgestellte Bindungen einsetzen, erfordern keine volle Kontrolle über den Stapel.  Diese Attribute, die für jede vom System bereitgestellte Bindung verfügbar gemacht werden, eignen sich am besten für das Verwendungsszenario der Bindungsadressen.  
  
 Der Konfigurationsabschnitt für jede vom System bereitgestellte Bindung kann verschiedene Konfigurationen definieren, mit denen die Bindung konfiguriert wird.  Jede Konfiguration wird durch einen eindeutigen Namen identifiziert.  
  
 Es ist nicht möglich, Elemente oder Attribute einer vom System bereitgestellten Bindung hinzuzufügen.  Um dies durchzuführen, müssen Sie eine benutzerdefinierte Bindung definieren, wie im Abschnitt "Benutzerdefinierte Bindung" dieses Themas beschrieben.  Es ist möglich, eine benutzerdefinierte Bindung zu definieren, die eine vom System bereitgestellte Bindung auf perfekte Weise imitiert und einige Einstellungen hinzufügt, über die die Benutzeranwendung die Kontrolle haben möchte.  
  
 Eine Liste der vom System bereitgestellten Bindungen finden Sie unter [Vom System bereitgestellte Bindungen](../../../../../docs/framework/wcf/system-provided-bindings.md).  
  
## Benutzerdefinierte Bindung  
 Benutzerdefinierte Bindungen stellen Vollzugriff auf den WCF\-Messagingstapel bereit.  Eine individuelle Bindung definiert den Nachrichtenstapel durch Angeben der Konfigurationselemente für Stapelelemente in der Reihenfolge des Stapels.  Jedes Element definiert und konfiguriert das eine Element des Stapels.  Es muss genau ein `transport`\-Element in jeder benutzerdefinierten Bindung geben.  Ohne dieses Element ist der Messagingstapel unvollständig.  
  
 Die Reihenfolge der Elemente im Stapel ist von Belang, da sie der Reihenfolge entspricht, in der Vorgänge auf die Meldung angewendet werden.  Die erforderliche Reihenfolge von Stapelelementen ist folgende:  
  
1.  Transaktionen \(optional\)  
  
2.  Zuverlässiges Messaging \(optional\)  
  
3.  Sicherheit \(Security, optional\)  
  
4.  Encoder  
  
5.  Transport  
  
 Benutzerdefinierte Bindungen werden durch ihr `name`\-Attribut identifiziert.  Weitere Informationen zu benutzerdefinierten Bindungen finden Sie unter [Benutzerdefinierte Bindungen](../../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.BindingsSection>   
 <xref:System.ServiceModel.Channels.Binding>   
 <xref:System.ServiceModel.Channels.BindingElement>   
 [Bindungen](../../../../../docs/framework/wcf/bindings.md)   
 [Benutzerdefinierte Bindungen](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [\<Bindung\>](../../../../../docs/framework/misc/binding.md)