---
title: Umwandlung und Typkonvertierungen (C#-Programmierhandbuch) | Microsoft-Dokumentation
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- type conversion [C#]
- data type conversion [C#]
- numeric conversions [C#]
- conversions [C#], type
- casting [C#]
- converting types [C#]
ms.assetid: 568df58a-d292-4b55-93ba-601578722878
caps.latest.revision: 52
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: d421f0115642efa73dbeb893dba912b96d5f4dc6
ms.contentlocale: de-de
ms.lasthandoff: 03/31/2017

---
# <a name="casting-and-type-conversions-c-programming-guide"></a>Umwandlung und Typkonvertierungen (C#-Programmierhandbuch)
Weil C# zur Laufzeit statisch kompiliert ist, kann eine Variable, nachdem sie deklariert wurde, nicht noch einmal deklariert oder dazu verwendet werden, Werte anderer Typen zu speichern, es sei denn, der Wert ist in den Wert der Variablen konvertierbar. Es gibt z.B. keine Konvertierung einer Ganzzahl in eine willkürliche Zeichenfolge. Deshalb können Sie, nachdem Sie `i` Ganzzahl deklariert haben, die Zeichenfolge „Hello“ nicht zuweisen, wie in folgendem Codebeispiel gezeigt.  
  
```csharp  
int i;  
i = "Hello"; // Error: "Cannot implicitly convert type 'string' to 'int'"  
```  
  
 Manchmal müssen Sie möglicherweise einen Wert in eine Variable oder einen Methodenparameter eines anderen Typen kopieren. Sie haben z.B. möglicherweise eine Ganzzahlvariable, die Sie an eine Methode übergeben müssen, deren Parameter vom Type `double` ist. Möglicherweise müssen Sie auch einer Variablen eines Schnittstellentyps eine Klassenvariable zuweisen. Derartige Vorgänge werden als *Typkonvertierungen* bezeichnet. In C# können Sie folgende Arten von Konvertierungen durchführen:  
  
-   **Implizite Konvertierung**: Es ist keine besondere Syntax erforderlich, da die Konvertierung typsicher ist, und keine Daten verloren gehen. Beispiele sind Konvertierungen von kleinere in größere Ganzzahltypen und Konvertierungen von abgeleiteten in Basisklassen.  
  
-   **Explizite Konvertierungen (Umwandlungen)**: Für explizite Konvertierungen ist ein Umwandlungsoperator erforderlich. Eine Umwandlung ist erforderlich, wenn Informationen bei einer Konvertierung verloren gehen können oder wenn die Konvertierung aus anderen Gründen fehlschlagen könnte.  Häufig auftretende Beispiele sind u.a. numerische Konvertierungen in einen Typen, der eine geringere Genauigkeit oder einen kleineren Bereich aufweist, oder Konvertierungen einer Instanz einer Basisklasse in eine abgeleitete Klasse.  
  
-   **Benutzerdefinierte Konvertierungen**: Benutzerdefinierte Konvertierungen werden anhand spezieller Methoden durchgeführt, die Sie definieren können, um explizite und implizite Konvertierungen zwischen benutzerdefinierten Typen zu ermöglichen, die nicht in einem Verhältnis „Basisklasse – abgeleitete Klasse“ zueinander stehen. Weitere Informationen finden Sie unter [Konvertierungsoperatoren](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md).  
  
-   **Konvertierungen mit Hilfsprogrammen**: Für eine Konvertierung von nicht kompatiblen Typen (wie z.B. von Ganzzahlen und <xref:System.DateTime?displayProperty=fullName>-Objekten, oder hexadezimal Zeichenfolgen und Bytearrays) können Sie die <xref:System.BitConverter?displayProperty=fullName>-Klasse, die <xref:System.Convert?displayProperty=fullName>-Klasse und die `Parse`-Methode der integrierten numerischen Typen (wie z.B. <xref:System.Int32.Parse%2A?displayProperty=fullName>) verwenden. Weitere Informationen finden Sie unter [Vorgehensweise: Konvertieren eines Bytearrays in einen ganzzahligen Typ](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md), [Vorgehensweise: Konvertieren einer Zeichenfolge in eine Zahl](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md) und [Vorgehensweise: Konvertieren zwischen Hexadezimalzeichenfolgen und numerischen Typen](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md).  
  
## <a name="implicit-conversions"></a>Implizite Konvertierungen  
 Eine implizite Konvertierung kann für integrierte numerische Typen durchgeführt werden, wenn der zu speichernde Wert in die Variable passt, ohne abgeschnitten oder abgerundet zu werden. Eine Variable den Typs [long](../../../csharp/language-reference/keywords/long.md) (8-Byte-Ganzzahl) kann z.B. jeden Wert speichern, den eine Variable des Typs [int](../../../csharp/language-reference/keywords/int.md) (4-Bytes auf einem 32-Bit-Computer) speichern kann. In folgendem Beispiel konvertiert der Compiler den Wert auf der rechten Seite implizit in einen Typ `long`, bevor er ihn `bigNum` zuweist.  
  
 [!code-cs[csProgGuideTypes#34](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_1.cs)]  
  
 Eine vollständige Liste aller impliziten numerischen Konvertierungen finden Sie unter [Tabelle für implizite numerische Konvertierungen](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
 Eine implizite Konvertierungen für Verweistypen von einer Klasse in jede ihrer direkten oder indirekten Basisklassen oder Schnittstellen ist immer möglich. Es ist keine spezielle Syntax erforderlich, da eine abgeleitete Klasse immer alle Member der Basisklasse enthält.  
  
```  
Derived d = new Derived();  
Base b = d; // Always OK.  
```  
  
## <a name="explicit-conversions"></a>Explizite Konvertierungen  
 Wenn allerdings eine Konvertierung nicht ohne möglichen Informationsverlust durchgeführt werden kann, fordert der Compiler eine explizite Konvertierung; diese wird als *Umwandlung* bezeichnet. Eine Umwandlung bietet die Möglichkeit, den Compiler explizit zu verständigen, dass Sie eine Konvertierung vornehmen möchten, und dass es Ihnen bewusst ist, dass dies einen Datenverlust zur Folge haben kann. Wenn Sie eine Umwandlung durchführen möchten, geben Sie den Typ, in den umgewandelt werden soll, in Klammern am Anfang des zu konvertierenden Wertes oder der zu konvertierenden Variablen an. Das folgende Programm wandelt ein [double](../../../csharp/language-reference/keywords/double.md) in ein [int](../../../csharp/language-reference/keywords/int.md) um. Das Programm führt ohne die Umwandlung keine Kompilierung durch.  
  
 [!code-cs[csProgGuideTypes#2](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_2.cs)]  
  
 Eine Liste der zulässigen expliziten numerischen Konvertierungen finden Sie unter [Tabelle für explizite numerische Konvertierungen](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
 Eine explizite Umwandlung ist für Verweistypen erforderlich, wenn Sie von einer Basisklasse in eine abgeleitete Klasse konvertieren möchten:  
  
```csharp  
// Create a new derived type.  
Giraffe g = new Giraffe();  
  
// Implicit conversion to base type is safe.  
Animal a = g;  
  
// Explicit conversion is required to cast back  
// to derived type. Note: This will compile but will  
// throw an exception at run time if the right-side  
// object is not in fact a Giraffe.  
Giraffe g2 = (Giraffe) a;  
```  
  
 Ein Umwandlungsvorgang zwischen Verweistypen ändert nicht den Laufzeittypen des zugrunde liegenden Objekts; er ändert lediglich den Typ des Wertes, der als Verweis auf das Objekt verwendet wird. Weitere Informationen finden Sie unter [Polymorphie](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
## <a name="type-conversion-exceptions-at-run-time"></a>Typkonvertierungsausnahmen zur Laufzeit  
 In manchen Verweistypkonvertierungen kann der Compiler nicht bestimmen, ob eine Umwandlung zulässig wäre. Es ist möglich, dass ein Umwandlungsvorgang, der ordnungsgemäß kompiliert, zur Laufzeit fehlschlägt. Eine fehlgeschlagene Typumwandlung zur Laufzeit löst eine <xref:System.InvalidCastException> aus, wie in folgendem Beispiel dargestellt.  
  
 [!code-cs[csProgGuideTypes#41](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_3.cs)]  
  
 C# stellt die Operatoren [is](../../../csharp/language-reference/keywords/is.md) und [as](../../../csharp/language-reference/keywords/as.md) bereit, mit denen Sie vor einer Umwandlung auf Kompatibilität prüfen können. Weitere Informationen finden Sie unter [Vorgehensweise: Sichere Umwandlung mit den Operatoren „as“ und „is“](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md).  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  

## <a name="see-also"></a>Siehe auch  
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Typen](../../../csharp/programming-guide/types/index.md)   
 [()-Operator](../../../csharp/language-reference/operators/invocation-operator.md)   
 [explicit](../../../csharp/language-reference/keywords/explicit.md)   
 [implicit](../../../csharp/language-reference/keywords/implicit.md)   
 [Konvertierungsoperatoren](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)   
 [Verallgemeinerte Typkonvertierung](http://msdn.microsoft.com/library/49253ae6-7657-4810-82ab-1176a6feeada)   
 [Konvertieren exportierter Typen](http://msdn.microsoft.com/en-us/1dfe55f4-07a2-4b61-aabf-a8cf65783a6b)   
 [Gewusst wie: Konvertieren einer Zeichenfolge in eine Zahl](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)
