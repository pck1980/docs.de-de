---
title: "Erforderliche Argumente und &#220;berladungsgruppen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ca3ed06-b9af-4b85-8b70-88c2186aefa3
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Erforderliche Argumente und &#220;berladungsgruppen
Aktivitäten können so konfiguriert werden, dass bestimmte Argumente gebunden werden müssen, wenn die Ausführung der Aktivität gültig sein soll.Das `RequiredArgument`\-Attribut wird verwendet, um anzugeben, dass bestimmte Argumente für eine Aktivität erforderlich sind. Mit dem `OverloadGroup`\-Attribut werden die Kategorien erforderlicher Argumente zusammen anzuordnen.Mit diesen Attributen können Aktivitätsautoren einfache oder komplexe Konfigurationen für die Aktivitätsvalidierung bereitstellen.  
  
## Verwenden von erforderlichen Argumenten  
 Damit das `RequiredArgument`\-Attribut in einer Aktivität verwendet werden kann, geben Sie die gewünschten Argumente mit <xref:System.Activities.RequiredArgumentAttribute> an.In diesem Beispiel wird eine `Add`\-Aktivität definiert, die über zwei erforderliche Argumente verfügt.  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 In XAML werden erforderliche Argumente auch durch die Verwendung des <xref:System.Activities.RequiredArgumentAttribute>\-Objekts angegeben.In diesem Beispiel wird die `Add`\-Aktivität mit drei Argumenten definiert. Sie verwendet eine <xref:System.Activities.Statements.Assign%601>\-Aktivität, um den Hinzufügevorgang auszuführen.  
  
```xaml  
<Activity x:Class="ValidationDemo.Add" ...>  
  <x:Members>  
    <x:Property Name="Operand1" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Operand2" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Result" Type="OutArgument(x:Int32)" />  
  </x:Members>  
  <Assign>  
    <Assign.To>  
      <OutArgument x:TypeArguments="x:Int32">[Result]</OutArgument>  
    </Assign.To>  
    <Assign.Value>  
      <InArgument x:TypeArguments="x:Int32">[Operand1 + Operand2]</InArgument>  
    </Assign.Value>  
  </Assign>  
</Activity>  
```  
  
 Wenn die Aktivität verwendet wird und eines der beiden erforderlichen Argumente nicht gebunden ist, wird der folgende Validierungsfehler zurückgegeben.  
  
 **Für das erforderliche Aktivitätsargument 'Operand1' wurde kein Wert angegeben.**   
> [!NOTE]
>  [!INCLUDE[crabout](../../../includes/crabout-md.md)] Überprüfen und Behandeln von Validierungsfehlern und \-warnungen finden Sie unter [Aufrufen der Aktivitätsvalidierung](../../../docs/framework/windows-workflow-foundation//invoking-activity-validation.md).  
  
## Verwenden von Überladungsgruppen  
 Überladungsgruppen bieten eine Methode zum Angeben der Argumentkombinationen, die in einer Aktivität gültig sind.Argumente werden mit <xref:System.Activities.OverloadGroupAttribute> zusammen angeordnet.Jeder Gruppe erhält einen Namen, der vom <xref:System.Activities.OverloadGroupAttribute>\-Objekt angegeben wird. Die Aktivität ist gültig, wenn nur ein Satz von Argumenten in einer Überladungsgruppe gebunden wird.Im folgenden Ausschnitt aus dem Beispiel [OverloadGroups](../../../docs/framework/windows-workflow-foundation/samples/overloadgroups.md) wird eine `CreateLocation`\-Klasse definiert.  
  
```csharp  
class CreateLocation: Activity  
{  
    [RequiredArgument]  
    public InArgument<string> Name { get; set; }  
  
    public InArgument<string> Description { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Latitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Longitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    [OverloadGroup("G3")]  
    public InArgument<string> Street { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> City { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> State { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G3")]  
    public InArgument<int> Zip { get; set; }                  
}  
```  
  
 Ziel dieser Aktivität ist es, einen Standort in den USA anzugeben.Hierzu kann der Benutzer der Aktivität den Standort mithilfe von drei Argumentgruppen angeben.Zum Angeben gültiger Argumentkombinationen wurden drei Überladungsgruppen definiert.`G1` enthält das `Latitude`\-Argument und `Longitude`\-Argument.`G2` enthält `Street`, `City` und `State`.`G3` enthält `Street` und `Zip`.`Name` ist ebenfalls ein erforderliches Argument, jedoch nicht Teil einer Überladungsgruppe.Damit diese Aktivität gültig ist, müsste `Name` zusammen mit allen Argumenten aus einer \(und nur einer\) der Überladungsgruppen gebunden werden.  
  
 Im folgenden Abschnitt aus dem Beispiel [Datenbankzugriffsaktivitäten](../../../docs/framework/windows-workflow-foundation/samples/database-access-activities.md) gibt es zwei Überladungsgruppen: `ConnectionString` und `ConfigFileSectionName`.Damit diese Aktivität gültig ist, muss das `ProviderName`\-Argument und das `ConnectionString`\-Argument gebunden werden oder das `ConfigName`\-Argument, jedoch nicht beide.  
  
```  
Public class DbUpdate: AsyncCodeActivity  
{  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
  
    [DependsOn("Parameters")]  
    public OutArgument<int> AffectedRecords { get; set; }       
}  
```  
  
 Wann eine Überladungsgruppe definiert wird:  
  
-   Eine Überladungsgruppe darf keine Teilmenge bzw. kein äquivalenter Satz einer anderen Überladungsgruppe sein.  
  
    > [!NOTE]
    >  Es gibt allerdings eine Ausnahme zu dieser Regel.Wenn eine Überladungsgruppe eine Teilmenge einer anderen Überladungsgruppe ist und die Teilmenge nur Argumente enthält, bei denen `RequiredArgument` gleich `false` ist, ist die Überladungsgruppe gültig.  
  
-   Überladungsgruppen können sich überschneiden. Dabei tritt jedoch ein Fehler auf, wenn die Schnittmenge der Gruppen alle erforderlichen Argumente einer oder beider Überladungsgruppen enthält.Im vorherigen Beispiel trat eine Überschneidung zwischen der Überladungsgruppe `G2` und der Überladungsgruppe `G3` auf, aber da die Schnittmenge nicht alle Argumente einer oder beider Gruppen enthielt, war dies gültig.  
  
 Wann Argumente in einer Überladungsgruppe gebunden werden:  
  
-   Eine Überladungsgruppe wird als gebunden angesehen, wenn alle `RequiredArgument`\-Argumente in der Gruppe gebunden sind.  
  
-   Wenn eine Gruppe über 0 `RequiredArgument`\-Argumente verfügt und mindestens ein Argument gebunden ist, wird die Gruppe als gebunden betrachtet.  
  
-   Es tritt ein Validierungsfehler auf, wenn keine der Überladungsgruppen gebunden ist, es sei denn, eine Überladungsgruppe enthält keine `RequiredArgument`\-Argumente.  
  
-   Es tritt ein Fehler auf, wenn mehr als eine Überladungsgruppe gebunden ist, d. h., wenn alle erforderlichen Argumente in einer Überladungsgruppe gebunden sind und zusätzlich ein weiteres Argument in einer anderen Überladungsgruppe gebunden ist.