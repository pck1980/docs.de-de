---
title: Entfernen von Elementen, Attributen und Knoten aus einem XML-Baum (C#) | Microsoft-Dokumentation
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 07dd06d6-1117-4077-bf98-9120cf51176e
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 23091224f314582908438f29340b811498d4c90e
ms.lasthandoff: 03/13/2017


---
# <a name="removing-elements-attributes-and-nodes-from-an-xml-tree-c"></a>Entfernen von Elementen, Attributen und Knoten aus einem XML-Baum (C#)
Sie können eine XML-Struktur ändern, indem Sie Elemente, Attribute und andere Knotentypen entfernen.  
  
 Das Entfernen eines einzelnen Elements oder Attributs aus einem XML-Dokument ist unkompliziert. Wenn Sie aber Auflistungen von Elementen oder Attributen entfernen, sollten Sie zuerst eine Auflistung in einer Liste materialisieren, bevor Sie die Elemente oder Attribute aus der Liste löschen. Verwenden Sie dazu am besten die Erweiterungsmethode <xref:System.Xml.Linq.Extensions.Remove%2A>, die diese Aufgabe für Sie übernimmt.  
  
 Der Hauptgrund für diese Vorgehensweise besteht darin, dass die meisten Auflistungen, die Sie aus einer XML-Struktur abrufen, mit verzögerter Ausführung zurückgegeben werden. Wenn Sie die Auflistungen nicht zunächst in einer Liste materialisieren oder wenn Sie nicht die Erweiterungsmethoden verwenden, kommt es möglicherweise zu einer bestimmten Form von Fehlern. Weitere Informationen finden Sie unter [Mixed Declarative Code/Imperative Code Bugs (LINQ to XML) (C#) (Fehler durch Vermischung von deklarativem und imperativem Code (LINQ to XML) (C#))](../../../../csharp/programming-guide/concepts/linq/mixed-declarative-code-imperative-code-bugs-linq-to-xml.md).  
  
 Die folgenden Methoden entfernen Knoten und Attribute aus einer XML-Struktur.  
  
|Methode|Beschreibung|  
|------------|-----------------|  
|[XAttribute.Remove](https://msdn.microsoft.com/library/system.xml.linq.xattribute.remove\(v=vs.110\).aspx)|Entfernt ein <xref:System.Xml.Linq.XAttribute> vom übergeordneten Element.|  
|[XContainer.RemoveNodes](https://msdn.microsoft.com/library/system.xml.linq.xcontainer.removenodes\(v=vs.110\).aspx)|Entfernt untergeordnete Knoten aus einem <xref:System.Xml.Linq.XContainer>.|  
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=fullName>|Entfernt Inhalt und Attribute aus einem <xref:System.Xml.Linq.XElement>.|  
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=fullName>|Entfernt die Attribute aus einem <xref:System.Xml.Linq.XElement>.|  
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=fullName>|Entfernt das Attribut, wenn Sie als Wert `null` übergeben.|  
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=fullName>|Entfernt das untergeordnete Element, wenn Sie als Wert `null` übergeben.|  
|<xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=fullName>|Entfernt <xref:System.Xml.Linq.XNode> aus dessen übergeordnetem Element.|  
|<xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=fullName>|Entfernt jedes Attribut oder Element in der Quellauflistung aus seinem übergeordneten Element.|  
  
## <a name="example"></a>Beispiel  
  
### <a name="description"></a>Beschreibung  
 In diesem Beispiel werden drei Ansätze zum Entfernen von Elementen gezeigt. Zuerst entfernt das Beispiel ein einzelnes Element. Als Zweites ruft das Beispiel eine Auflistung von Elementen ab, materialisiert diese mit dem <xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>-Operator und entfernt die Auflistung. Zum Schluss ruft das Beispiel eine Auflistung von Elementen ab und entfernt diese mit der Erweiterungsmethode <xref:System.Xml.Linq.Extensions.Remove%2A>.  
  
 Weitere Informationen über den <xref:System.Linq.Enumerable.ToList%2A>-Operator finden Sie unter [Converting Data Types (C#) (Konvertieren von Datentypen (C#))](../../../../csharp/programming-guide/concepts/linq/converting-data-types.md).  
  
### <a name="code"></a>Code  
  
```csharp  
XElement root = XElement.Parse(@"<Root>  
    <Child1>  
        <GrandChild1/>  
        <GrandChild2/>  
        <GrandChild3/>  
    </Child1>  
    <Child2>  
        <GrandChild4/>  
        <GrandChild5/>  
        <GrandChild6/>  
    </Child2>  
    <Child3>  
        <GrandChild7/>  
        <GrandChild8/>  
        <GrandChild9/>  
    </Child3>  
</Root>");  
root.Element("Child1").Element("GrandChild1").Remove();  
root.Element("Child2").Elements().ToList().Remove();  
root.Element("Child3").Elements().Remove();  
Console.WriteLine(root);  
```  
  
### <a name="comments"></a>Kommentare  
 Dieser Code erzeugt die folgende Ausgabe:  
  
```xml  
<Root>  
  <Child1>  
    <GrandChild2 />  
    <GrandChild3 />  
  </Child1>  
  <Child2 />  
  <Child3 />  
</Root>  
```  
  
 Beachten Sie, dass das erste Element der zweiten Unterebene aus `Child1` entfernt wurde. Alle Elemente der zweiten Unterebene wurden aus `Child2` und `Child3` entfernt.  
  
## <a name="see-also"></a>Siehe auch  
 [Modifying XML Trees (LINQ to XML) (C#) (Ändern von XML-Strukturen (LINQ to XML) (C#))](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
