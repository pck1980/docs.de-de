---
title: 'Gewusst wie: Umbenennen einer Datei in Visual Basic'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- I/O [Visual Basic], renaming files
- files, renaming
ms.assetid: 0ea7e0c8-2cb2-4bf5-a00d-7b6e3c08a3bc
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: f003cfc7c7880a47515f7328a0503072f3b02cbf
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-rename-a-file-in-visual-basic"></a>Gewusst wie: Umbenennen einer Datei in Visual Basic
Verwenden Sie die `RenameFile`-Methode des `My.Computer.FileSystem`-Objekts, um eine Datei umzubenennen, indem Sie den aktuellen Standort, Dateinamen sowie den neuen Dateinamen bereitstellen. Diese Methode kann nicht dazu verwendet werden, um eine Datei zu verschieben; verwenden Sie die `MoveFile`-Methode, um die Datei zu verschieben und umzubenennen.  
  
### <a name="to-rename-a-file"></a>So benennen Sie eine Datei um  
  
-   Verwenden Sie die `My.Computer.FileSystem.RenameFile`-Methode, um eine Datei umzubenennen. In diesem Beispiel wird die Datei `Test.txt` in `SecondTest.txt` umbenannt.  
  
     [!code-vb[VbVbcnMyFileSystem#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-rename-a-file_1.vb)]  
  
 Dieses Codebeispiel ist auch als IntelliSense-Codeausschnitt verfügbar. In der Codeausschnittauswahl befindet sich der Ausschnitt unter **Dateisystem - Verarbeiten von Laufwerken, Ordnern und Dateien**. Weitere Informationen finden Sie unter [Codeausschnitte](/visualstudio/ide/code-snippets).  
  
## <a name="robust-programming"></a>Stabile Programmierung  
 Die folgenden Bedingungen können einen Ausnahmefehler verursachen:  
  
-   Der Pfad ist aus einem der folgenden Gründe ungültig: Er ist eine Zeichenfolge der Länge 0, er enthält nur Leerzeichen, er enthält ungültige Zeichen, oder er ist ein Gerätepfad (beginnt mit \\\\.\\) (<xref:System.ArgumentException>).  
  
-   `newName` enthält Pfadinformationen (<xref:System.ArgumentException>).  
  
-   Der Pfad ist ungültig, da er `Nothing` ist (<xref:System.ArgumentNullException>).  
  
-   `newName` ist `Nothing` oder eine leere Zeichenfolge (<xref:System.ArgumentNullException>).  
  
-   Die Quelldatei ist ungültig oder nicht vorhanden (<xref:System.IO.FileNotFoundException>).  
  
-   Eine Datei oder ein Verzeichnis mit dem in `newName` angegebenen Namen (<xref:System.IO.IOException>) ist bereits vorhanden.  
  
-   Der Pfad überschreitet die im System definierte maximale Länge (<xref:System.IO.PathTooLongException>).  
  
-   Der Pfad eines Datei- oder Verzeichnisnamens enthält einen Doppelpunkt (:) oder hat ein ungültiges Format (<xref:System.NotSupportedException>).  
  
-   Dem Benutzer fehlen die erforderlichen Berechtigungen zum Anzeigen des Pfades (<xref:System.Security.SecurityException>).  
  
-   Der Benutzer hat nicht die erforderliche Berechtigung (<xref:System.UnauthorizedAccessException>).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.RenameFile%2A>   
 [Gewusst wie: Verschieben einer Datei](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-move-a-file.md)   
 [Erstellen, Löschen und Verschieben von Dateien und Verzeichnissen](../../../../visual-basic/developing-apps/programming/drives-directories-files/creating-deleting-and-moving-files-and-directories.md)   
 [Gewusst wie: Erstellen einer Kopie einer Datei im gleichen Verzeichnis](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-the-same-directory.md)   
 [Gewusst wie: Erstellen einer Kopie einer Datei in einem anderen Verzeichnis](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)

