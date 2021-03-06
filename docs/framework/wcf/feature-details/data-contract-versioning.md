---
title: "Datenvertragsversionsverwaltung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Datenverträge [WCF], Versionskontrolle"
  - "Versionskontrolle [WCF]"
  - "Versionskontrolle [WCF], Datenverträge"
ms.assetid: 4a0700cb-5f5f-4137-8705-3a3ecf06461f
caps.latest.revision: 35
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 35
---
# Datenvertragsversionsverwaltung
Durch die Weiterentwicklung der Anwendungen müssen Sie möglicherweise auch die Datenverträge ändern, die die Dienste verwenden.  Dieses Thema erklärt, wie man die Versionsverwaltung von Datenverträgen durchführt.  In diesem Thema werden die Datenvertragsversionsmechanismen beschrieben.  Eine vollständige Übersicht und normative Versionsverwaltungsanleitung finden Sie unter [Empfohlene Vorgehensweisen: Versionsverwaltung von Datenverträgen](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md).  
  
## Breaking Changes gegenüberNon\-breaking Changes  
 Änderungen an einem Datenvertrag können "breaking" oder "non\-breaking" sein.  Wird ein Datenvertrag auf eine "non\-breaking"\-Art geändert, kann eine Anwendung, die die ältere Version des Vertrags verwendet, mit einer Anwendung kommunizieren, die die neuere Version verwendet; und eine Anwendung, die die neuere Version des Vertrags verwendet, kann mit einer Anwendung kommunizieren, die die ältere Version verwendet.  Andererseits verhindert ein "Breaking Change" die Kommunikation in eine oder beide Richtungen.  
  
 Jede Änderung eines Typs, der nicht beeinflusst, wie er gesendet und empfangen wird, ist "non\-breaking".  Solche Änderungen ändern nicht den Datenvertrag, nur den zugrunde liegenden Typ.  Beispielsweise kann der Name eines Felds auf "non\-breaking"\-Art geändert werden, indem die Eigenschaft <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A> des <xref:System.Runtime.Serialization.DataMemberAttribute> auf den älteren Versionsnamen festgelegt wird.  Der folgende Code zeigt Version 1 eines Datenvertrags.  
  
 [!code-csharp[C_DataContractVersioning#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#1)]
 [!code-vb[C_DataContractVersioning#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#1)]  
  
 Im folgenden Code wird ein "Non\-Breaking Change" veranschaulicht.  
  
 [!code-csharp[C_DataContractVersioning#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#2)]
 [!code-vb[C_DataContractVersioning#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#2)]  
  
 Einige Änderungen ändern die gesendeten Daten, müssen aber nicht unbedingt "breaking" sein.  Die folgenden Änderungen sind immer "breaking":  
  
-   Das Ändern der Werte <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>oder <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A> eines Datenvertrags.  
  
-   Das Ändern der Reihenfolge der Datenelemente über die Eigenschaft <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> der Klasse <xref:System.Runtime.Serialization.DataMemberAttribute>.  
  
-   Das Umbenennen eines Datenelements.  
  
-   Das Ändern des Datenvertrags eines Datenelements.  Beispielsweise die Änderung des Typs eines Datenelements von ganzer Zahl zu Zeichenfolge oder von einem Typ mit Datenvertrag namens "Kunde" in einen Typ mit einem Datenvertrag namens "Person".  
  
 Ebenfalls möglich sind die folgenden Änderungen.  
  
## Das Hinzufügen und Entfernen von Datenelementen  
 In den meisten Fällen ist das Hinzufügen oder Entfernen eines Datenelements kein "Breaking Change", sofern keine strikte Schemavalidierung \(neue Instanzen, die gegen das alte Schema validiert werden\) erforderlich ist.  
  
 Wenn ein Typ mit einem Extrafeld in einen Typ mit einem fehlenden Feld deserialisiert wird, werden die Extrainformationen ignoriert.  \(Möglicherweise werden sie auch für Round\-Tripping\-Zwecke gespeichert. Weitere Informationen hierzu finden Sie unter [Aufwärtskompatible Datenverträge](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)\).  
  
 Wenn ein Typ mit einem fehlenden Feld in einen Typ mit einem Extrafeld deserialisiert wird, behält das Extrafeld seinen Standardwert bei, normalerweise `null`.  \(Der Standardwert kann geändert werden. Weitere Informationen hierzu finden Sie unter [Versionstolerante Serialisierungsrückrufe](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md).\)  
  
 Beispielsweise können Sie die Klasse `CarV1` für einen Client und die Klasse `CarV2` für einen Dienst verwenden; oder Sie können die Klasse `CarV1` für einen Dienst und die Klasse `CarV2` für einen Client verwenden.  
  
 [!code-csharp[C_DataContractVersioning#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#3)]
 [!code-vb[C_DataContractVersioning#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#3)]  
  
 Der Version 2\-Endpunkt kann Daten erfolgreich an den Version 1\-Endpunkt senden.  Eine Serialisierung von Version 2 des `Car`\-Datenvertrags führt zu einer XML\-Darstellung, die in etwa der folgenden entspricht.  
  
```  
<Car>  
    <Model>Porsche</Model>  
    <HorsePower>300</HorsePower>  
</Car>  
```  
  
 Das Deserialisierungsmodul auf V1 findet kein entsprechendes Datenelement für das Feld `HorsePower` und verwirft die Daten.  
  
 Außerdem kann der Version 1\-Endpunkt Daten erfolgreich an den Version 2\-Endpunkt senden.  Eine Serialisierung von Version 1 des `Car`\-Datenvertrags führt zu einer der folgenden ähnlichen XML\-Darstellung.  
  
```  
<Car>  
    <Model>Porsche</Model>  
</Car>  
```  
  
 Der Version 2\-Deserialisierer weiß nicht, auf was er das Feld `HorsePower` festlegen soll, da in der eingehenden XML keine entsprechenden Daten vorliegen.  Stattdessen wird das Feld auf den Standardwert 0 \(null\) festgelegt.  
  
## Erforderliche Datenelemente  
 Ein Datenelement kann als "erforderlich" markiert werden, indem die Eigenschaft <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> der Klasse <xref:System.Runtime.Serialization.DataMemberAttribute> auf `true` festgelegt wird.  Wenn erforderliche Daten während der Deserialisierung fehlen, wird eine Ausnahme verwendet, anstatt die Datenelemente auf ihren Standardwert festzulegen.  
  
 Das Hinzufügen von erforderlichen Datenelementen ist ein "Breaking Change".  Das bedeutet, dass der neuere Typ noch immer an Endpunkte mit dem älteren Typ gesendet werden kann, aber nicht umgekehrt.  Das Löschen eines Datenelements, das in einer vorherigen Version als "erforderlich" markiert war, ist ebenfalls ein "Breaking Change".  
  
 Die Änderung des Eigenschaftswerts <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> von `true` nach `false` ist nicht "breaking", aber die Änderung von `false` nach `true` kann "breaking" sein, wenn eine frühere Version des Typs das fragliche Datenelement nicht besitzt.  
  
> [!NOTE]
>  Auch wenn die Eigenschaft <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> auf `true` festgelegt ist, müssen die eingehenden Daten NULL oder 0 \(null\) sein, und es muss ein Typ vorbereitet sein, um diese Möglichkeit abzudecken.  <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> sollte nicht als Sicherheitsmechanismus zum Schutz gegen ungültige eingehende Daten verwendet werden.  
  
## Ausgelassene Standardwerte  
 Es ist möglich \(wenn auch nicht empfehlenswert\), die Eigenschaft `EmitDefaultValue` des DataMemberAttribute\-Attributs auf `false` festzulegen, wie unter  [Standardwerte der Datenelemente](../../../../docs/framework/wcf/feature-details/data-member-default-values.md) beschrieben wird.  Wenn diese Einstellung `false` ist, wird das Datenelement nicht ausgegeben, wenn es auf seinen Standardwert \(normalerweise NULL oder 0 \(null\)\) festgelegt ist.  Dies ist in anderen Versionen auf zwei Arten nicht kompatibel mit erforderlichen Datenelementen:  
  
-   Ein Datenvertrag mit einem Datenelement, das in einer Version erforderlich ist, kann keine Standarddaten \(NULL oder 0\(null\)\) von einer anderen Version erhalten, in der das Datenelement `EmitDefaultValue` auf `false` festgelegt hat.  
  
-   Ein erforderliches Datenelement, dessen `EmitDefaultValue` auf `false` festgelegt ist, kann nicht verwendet werden, um seinen Standardwert \(NULL oder 0 \(null\)\) zu deserialisieren, aber es kann bei der Deserialisierung einen derartigen Wert erhalten.  Dies schafft ein Round\-Tripping\-Problem \(Daten können eingelesen werden, aber die gleichen Daten können nicht ausgegeben werden\).  Wenn daher in einer Version `IsRequired` `true` und `EmitDefaultValue` `false` ist, sollte die gleiche Kombination für alle anderen Versionen gelten, damit keine Version des Datenvertrags einen Wert produzieren kann, der nicht zu einem Roundtrip führt.  
  
## Schemaüberlegungen  
 Eine Erklärung, welches Schema für welche Datenvertragstypen produziert wird, finden Sie unter [Datenvertrags\-Schemareferenz](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).  
  
 Das Schema, das [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] für Datenvertragstypen erstellt, macht keine Bereitstellungen für die Versionsverwaltung.  Das bedeutet, dass das Schema, das von einer bestimmten Version eines Typs exportiert wurde, nur diejenigen Datenelemente enthält, die in dieser Version vorliegen.  Die Implementierung der <xref:System.Runtime.Serialization.IExtensibleDataObject>\-Schnittstelle ändert nicht das Schema eines Typs.  
  
 Datenelemente werden standardmäßig als optionale Elemente ins Schema exportiert.  Dies bedeutet, dass der Wert von `minOccurs` \(XML\-Attribut\) auf 0 \(null\) gesetzt wird.  Erforderliche Datenmember werden exportiert, wenn `minOccurs` auf 1 festgelegt wurde.  
  
 Viele der Änderungen, die als "non\-breaking" gelten, sind tatsächlich "breaking", wenn eine strenge Einhaltung des Schemas erforderlich ist.  Im vorherigen Beispiel würde eine `CarV1`\-Instanz, die nur das Element `Model` enthält, gegen das `CarV2`\-Schema \(das sowohl über `Model` als auch `Horsepower` verfügt, die aber beide optional sind\) positiv geprüft werden.  Das Gegenteil stimmt aber nicht: eine `CarV2`\-Instanz würde keine Validierung gegen das `CarV1`\-Schema bestehen.  
  
 Round\-Tripping bringt auch einige zusätzliche Überlegungen mit sich.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] dem Abschnitt "Schemaüberlegungen" unter [Aufwärtskompatible Datenverträge](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
### Andere zulässige Änderungen  
 Die Implementierung der <xref:System.Runtime.Serialization.IExtensibleDataObject>\-Schnittstelle ist ein "Non\-Breaking Change".  Es besteht jedoch kein Round\-Tripping\-Support für Versionen des Typs vor der Version, in der <xref:System.Runtime.Serialization.IExtensibleDataObject> implementiert wurde.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Aufwärtskompatible Datenverträge](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)  
  
## Enumerationen  
 Das Hinzufügen oder Entfernen einer Enumeration ist ein "Breaking Change".  Die Änderung des Namens einer Enumeration ist "breaking", sofern nicht der Vertragsname durch die Verwendung des Attributs `EnumMemberAtttribute` der gleiche wie in der alten Version geblieben ist.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Enumerationstypen in Datenverträgen](../../../../docs/framework/wcf/feature-details/enumeration-types-in-data-contracts.md)  
  
## Auflistungen  
 Die meisten Sammlungsänderungen sind "non\-breaking", da die meisten Sammlungstypen im Datenvertragsmodell gegeneinander austauschbar sind.  Eine nicht angepasste Sammlung angepasst zu machen oder umgekehrt ist jedoch ein "Breaking Change".  Außerdem ist die Änderung der Anpassungseinstellungen der Sammlung ein "Breaking Change", d. h. eine Änderung des Namens und Namespace ihres Datenvertrags und eine Wiederholung des Elementnamens, des Schlüsselelementnamens und des Wertelementnamens.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] Sammlungsanpassung finden Sie unter [Sammlungstypen in Datenverträgen](../../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md).    
Natürlich ist die Änderung des Datenvertrags der Inhalte einer Sammlung \(z. B. die Änderung von einer Liste ganzer Zahlen zu einer Liste von Zeichenfolgen\) ein "Breaking Change".  
  
## Siehe auch  
 <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>   
 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>   
 <xref:System.Runtime.Serialization.SerializationException>   
 <xref:System.Runtime.Serialization.IExtensibleDataObject>   
 [Versionstolerante Serialisierungsrückrufe](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)   
 [Empfohlene Vorgehensweisen: Versionsverwaltung von Datenverträgen](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)   
 [Verwenden von Datenverträgen](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Datenvertragsäquivalenz](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [Aufwärtskompatible Datenverträge](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)