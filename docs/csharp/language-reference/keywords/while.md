---
title: while (C#-Referenz)
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- while_CSharpKeyword
- while
dev_langs:
- CSharp
helpviewer_keywords:
- while keyword [C#]
ms.assetid: 72a0765c-6852-4aca-b327-4a11cb7f5c59
caps.latest.revision: 22
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ed531c83dba02b38576bf8354b1ff92f075048bc
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="while-c-reference"></a>while (C#-Referenz)
Die `while`-Anweisung führt eine Anweisung oder einen Anweisungsblock aus, bis ein bestimmter Ausdruck `false` ergibt.  
  
## <a name="example"></a>Beispiel  
 [!code-cs[csrefKeywordsIteration#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_1.cs)]  
  
## <a name="example"></a>Beispiel  
 [!code-cs[csrefKeywordsIteration#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_2.cs)]  
  
## <a name="example"></a>Beispiel  
 Da der `while`-Ausdruck vor jeder Ausführung der Schleife getestet wird, wird eine `while`-Schleife entweder nie oder mehrmals ausgeführt. Dies unterscheidet sich von der [do](../../../csharp/language-reference/keywords/do.md)-Schleife, die ein oder mehrmals ausgeführt wird.  
  
 Eine `while`-Schleife kann beendet werden, wenn eine [break](../../../csharp/language-reference/keywords/break.md), [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md) oder [throw](../../../csharp/language-reference/keywords/throw.md)-Anweisung die Steuerung außerhalb der Schleife überträgt. Verwenden Sie die [continue](../../../csharp/language-reference/keywords/continue.md)-Anweisung, um die Steuerung an die nächste Iteration zu übertragen, ohne die Schleife zu beenden. Beachten Sie den Unterschied in der Ausgabe in den drei vorherigen Beispielen. Der Unterschied ist abhängig davon, wo `int n` inkrementiert wird. Im Beispiel unten wird keine Ausgabe generiert.  
  
 [!code-cs[csrefKeywordsIteration#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_3.cs)]  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)   
 [while-Anweisung (C++)](/cpp/cpp/while-statement-cpp)   
 [Iterationsanweisungen](../../../csharp/language-reference/keywords/iteration-statements.md)

