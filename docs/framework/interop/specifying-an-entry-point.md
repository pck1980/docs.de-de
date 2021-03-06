---
title: "Specifying an Entry Point | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "EntryPoint field"
  - "platform invoke, attribute fields"
  - "attribute fields in platform invoke, EntryPoint"
ms.assetid: d1247f08-0965-416a-b978-e0b50652dfe3
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Specifying an Entry Point
Ein Einstiegspunkt identifiziert die Position einer Funktion in einer DLL.  In einem verwalteten Projekt wird diese Funktion vom ursprünglichen Namen oder vom Ordinaleinstiegspunkt einer Zielfunktion über die Grenzen der Interoperation hinaus identifiziert.  Außerdem können Sie dem Einstiegspunkt einen anderen Namen zuordnen und damit die Funktion umbenennen.  
  
 Aus folgenden Gründen kann es sinnvoll sein, eine DLL\-Funktion umzubenennen:  
  
-   Um keine API\-Funktionsnamen zu verwenden, die zwischen Groß\- und Kleinschreibung unterscheiden.  
  
-   Um die Konventionen vorhandener Namensstandards einzuhalten.  
  
-   Um Funktionen aufzunehmen, die verschiedene Datentypen verwenden \(indem mehrere Versionen derselben DLL\-Funktion deklariert werden\).  
  
-   Um die Verwendung von APIs zu vereinfachen, die ANSI\- und Unicode\-Versionen enthalten.  
  
 In diesem Abschnitt wird das Umbenennen einer DLL\-Funktion in verwaltetem Code veranschaulicht.  
  
## Umbenennen einer Funktion in Visual Basic  
 In Visual Basic wird das <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=fullName>\-Feld mit dem **Function**\-Schlüsselwort in der **Declare**\-Anweisung festgelegt.  Das folgende Beispiel zeigt eine Basisdeklaration.  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
    Declare Auto Function MessageBox Lib "user32.dll" _  
       (ByVal hWnd As Integer, ByVal txt As String,_  
       ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
 Sie können den **MessageBox**\-Einstiegspunkt durch **MsgBox** ersetzen, indem Sie das **Alias**\-Schlüsselwort in die Definition aufnehmen, wie im folgenden Beispiel dargestellt.  In beiden Beispielen erübrigt sich aufgrund des **Auto**\-Schlüsselwortes die Angabe der Zeichensatzversion des Einstiegspunktes.  Weitere Informationen zum Auswählen eines Zeichensatzes finden Sie unter [Angeben eines Zeichensatzes](../../../docs/framework/interop/specifying-a-character-set.md).  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
    Declare Auto Function MsgBox Lib "user32.dll" _  
       Alias "MessageBox" (ByVal hWnd As Integer, ByVal txt As String,_  
       ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
## Umbenennen einer Funktion in C\# und C\+\+  
 Sie können das <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=fullName>\-Feld verwenden, um eine DLL\-Funktion nach Name oder Ordinalzahl anzugeben.  Wenn der Name der Funktion in der Methodendefinition mit dem Einstiegspunkt in der DLL übereinstimmt, müssen Sie die Funktion nicht explizit mit dem **EntryPoint**\-Feld identifizieren.  Andernfalls verwenden Sie eine der folgenden Attributformen zur Angabe eines Namens oder einer Ordinalzahl:  
  
```  
[DllImport("dllname", EntryPoint="Functionname")]  
[DllImport("dllname", EntryPoint="#123")]  
```  
  
 Hinweis: Für eine Ordinalzahl müssen Sie das Pfundzeichen \(\#\) als Präfix verwenden.  
  
 Im folgenden Beispiel wird veranschaulicht, wie Sie im Code **MessageBoxA** durch **MsgBox** ersetzen, indem Sie das **EntryPoint**\-Feld verwenden.  
  
```csharp  
using System.Runtime.InteropServices;  
  
public class Win32 {  
    [DllImport("user32.dll", EntryPoint="MessageBoxA")]  
    public static extern int MsgBox(int hWnd, String text, String caption,  
                                    uint type);  
}  
  
```  
  
```cpp  
using namespace System::Runtime::InteropServices;  
  
typedef void* HWND;  
[DllImport("user32", EntryPoint="MessageBoxA")]  
extern "C" int MsgBox(HWND hWnd,  
                      String*  pText,  
                      String*  pCaption,  
                      unsigned int uType);  
```  
  
## Siehe auch  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Creating Prototypes in Managed Code](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [Platform Invoke Examples](../../../docs/framework/interop/platform-invoke-examples.md)   
 [Marshaling Data with Platform Invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)