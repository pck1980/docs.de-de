---
title: "CheckBox-Stile und -Vorlagen | Microsoft Docs"
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
  - "CheckBox [WPF], Stile und Vorlagen"
  - "ControlTemplate [WPF], CheckBox"
  - "Bestandteile [WPF], CheckBox"
  - "Zustände [WPF], CheckBox"
  - "Formate [WPF], CheckBox"
  - "Vorlagen [WPF], CheckBox"
ms.assetid: bfdaec96-d101-4d3d-864d-c27e6b621d03
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# CheckBox-Stile und -Vorlagen
In diesem Thema werden die Stile und Vorlagen für das <xref:System.Windows.Controls.CheckBox>\-Steuerelement beschrieben.  Sie können die standardmäßige <xref:System.Windows.Controls.ControlTemplate> ändern, um dem Steuerelement ein individuelles Aussehen zu verleihen.  Weitere Informationen finden Sie unter [Anpassen der Darstellung eines vorhandenen Steuerelements durch Erstellen einer ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## CheckBox\-Teile  
 Das <xref:System.Windows.Controls.CheckBox>\-Steuerelement verfügt über keine benannten Teile.  
  
## CheckBox\-Zustände  
 In der folgenden Tabelle sind die visuellen Zustände für das <xref:System.Windows.Controls.CheckBox>\-Steuerelement aufgelistet.  
  
|VisualState\-Name|VisualStateGroup\-Name|Beschreibung|  
|-----------------------|----------------------------|------------------|  
|Normal|CommonStates|Der Standardzustand.|  
|MouseOver|CommonStates|Der Mauszeiger ist über dem Steuerelement positioniert.|  
|Pressed|CommonStates|Das Steuerelement wird gedrückt.|  
|Disabled|CommonStates|Das Steuerelement ist deaktiviert.|  
|Focused|FocusStates|Das Steuerelement besitzt den Fokus.|  
|Unfocused|FocusStates|Der Fokus liegt nicht auf dem Steuerelement.|  
|Checked|CheckStates|<xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> ist `true`.|  
|Deaktiviert|CheckStates|<xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> ist `false`.|  
|Indeterminate|CheckStates|<xref:System.Windows.Controls.Primitives.ToggleButton.IsThreeState%2A> ist `true`, und <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> ist `null`.|  
|Valid|ValidationStates|Das Steuerelement verwendet die <xref:System.Windows.Controls.Validation>\-Klasse, und die angefügte <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName>\-Eigenschaft ist `false`.|  
|InvalidUnfocused|ValidationStates|Wenn die angefügte <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName>\-Eigenschaft `true` ist, hat das Steuerelement den Fokus.|  
|InvalidFocused|ValidationStates|Wenn die angefügte <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName>\-Eigenschaft `true` ist, hat das Steuerelement nicht den Fokus.|  
  
## Beispiel für ein CheckBox\-ControlTemplate  
 Im folgenden Beispiel wird veranschaulicht, wie eine <xref:System.Windows.Controls.ControlTemplate> für das <xref:System.Windows.Controls.CheckBox>\-Steuerelement definiert wird.  
  
 [!code-xml[ControlTemplateExamples#CheckBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/checkbox.xaml#checkbox)]  
  
 Im vorherigen Beispiel werden eine oder mehrere der folgenden Ressourcen verwendet.  
  
 [!code-xml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Das vollständige Beispiel finden Sie unter          [Beispiel zum Formatieren mit ControlTemplates](http://go.microsoft.com/fwlink/?LinkID=160041) .  
  
## Siehe auch  
 <xref:System.Windows.FrameworkElement.Style%2A>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Steuerelementformate und \-vorlagen](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)   
 [Anpassung von Steuerelementen](../../../../docs/framework/wpf/controls/control-customization.md)   
 [Erstellen von Formaten und Vorlagen](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Anpassen der Darstellung eines vorhandenen Steuerelements durch Erstellen einer ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)