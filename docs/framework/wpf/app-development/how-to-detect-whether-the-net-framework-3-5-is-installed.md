---
title: "Gewusst wie: Erkennen einer .NET Framework 3.5-Installation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Erkennen einer .NET Framework 3.5-Installation [WPF]"
  - "Erkennen einer .NET Framework 3.5-Installation [WPF]"
  - "Bestimmen einer .NET Framework 3.5-Installation [WPF]"
  - "Überprüfen einer .NET Framework 3.5-Installation [WPF]"
ms.assetid: 8556a9d2-1eb8-48ef-919c-5baf22a2a9a2
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Gewusst wie: Erkennen einer .NET Framework 3.5-Installation
Bevor Administratoren [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]\-Anwendungen in einem auf [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] ausgerichteten System einsetzen können, müssen sie sich vergewissern, dass die [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)]\-Laufzeit vorhanden ist.  In diesem Thema wird ein in HTML\/JavaScript geschriebenes Skript bereitgestellt, das Administratoren verwenden können, um zu ermitteln, ob [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] auf einem System vorhanden ist.  
  
> [!NOTE]
>  Ausführlichere Informationen zum Installieren, Bereitstellen und Erkennen von [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] finden Sie unter [Installieren von .NET Framework](../../../../docs/framework/install/guide-for-developers.md).  
  
## Beispiel  
 Wenn [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] installiert ist, fügt MSI der UserAgent\-Zeichenfolge ".NET CLR" und die Versionsnummer hinzu.  Im folgenden Beispiel wird ein Skript gezeigt, das in eine einfache HTML\-Seite eingebettet ist.  Das Skript durchsucht die UserAgent\-Zeichenfolge, um festzustellen, ob [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] installiert ist. Daraufhin wird eine Statusmeldung zu den Suchergebnissen angezeigt.  
  
> [!NOTE]
>  Dieses Skript ist für Internet Explorer vorgesehen.  Andere Browser enthalten möglicherweise keine .NET\-CLR\-Informationen in der UserAgent\-Zeichenfolge.  
  
```  
<HTML>  
  <HEAD>  
    <TITLE>Test for the .NET Framework 3.5</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT LANGUAGE="JavaScript">  
    <!--  
    var dotNETRuntimeVersion = "3.5.0.0";  
  
    function window::onload()  
    {  
      if (HasRuntimeVersion(dotNETRuntimeVersion))  
      {  
        result.innerText =   
          "This machine has the correct version of the .NET Framework 3.5."  
      }   
      else  
      {  
        result.innerText =   
          "This machine does not have the correct version of the .NET Framework 3.5." +  
          " The required version is v" + dotNETRuntimeVersion + ".";  
      }  
      result.innerText += "\n\nThis machine's userAgent string is: " +   
        navigator.userAgent + ".";  
    }  
  
    //  
    // Retrieve the version from the user agent string and   
    // compare with the specified version.  
    //  
    function HasRuntimeVersion(versionToCheck)  
    {  
      var userAgentString =   
        navigator.userAgent.match(/.NET CLR [0-9.]+/g);  
  
      if (userAgentString != null)  
      {  
        var i;  
  
        for (i = 0; i < userAgentString.length; ++i)  
        {  
          if (CompareVersions(GetVersion(versionToCheck),   
            GetVersion(userAgentString[i])) <= 0)  
            return true;  
        }  
      }  
  
      return false;  
    }  
  
    //  
    // Extract the numeric part of the version string.  
    //  
    function GetVersion(versionString)  
    {  
      var numericString =   
        versionString.match(/([0-9]+)\.([0-9]+)\.([0-9]+)/i);  
      return numericString.slice(1);  
    }  
  
    //  
    // Compare the 2 version strings by converting them to numeric format.  
    //  
    function CompareVersions(version1, version2)  
    {  
      for (i = 0; i < version1.length; ++i)  
      {  
        var number1 = new Number(version1[i]);  
        var number2 = new Number(version2[i]);  
  
        if (number1 < number2)  
          return -1;  
  
        if (number1 > number2)  
          return 1;  
      }  
  
      return 0;  
    }  
  
    -->  
    </SCRIPT>  
  </HEAD>  
  
  <BODY>  
    <div id="result" />  
  </BODY>  
</HTML>  
  
```  
  
 Wenn die Suche nach der ".NET CLR"\-Version erfolgreich ist, wird die folgende Art von Statusmeldung angezeigt:  
  
 `This machine has the correct version of the .NET Framework 3.5.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; .NET CLR 3.5.20726; MS-RTC LM 8).`  
  
 Andernfalls wird die folgende Art von Statusmeldung angezeigt:  
  
 `This machine does not have the correct version of the .NET Framework 3.5.  The required version is v3.5.0.0.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; MS-RTC LM 8).`  
  
## Siehe auch  
 [Erkennen einer .NET Framework 3.0\-Installation](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-0-is-installed.md)