---
title: "以程式設計方式使用變數 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 5c8968302f42e1b8fde55894810ecb77cf715ab6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="working-with-variables-programmatically"></a>以程式設計方式使用變數
  變數是在封裝、容器、工作及事件處理常式中動態設定值和控制處理序的方式。 優先順序條件約束也可以使用變數，以控制資料流向不同工作的方向。 變數有各種不同的用途：  
  
-   在執行階段更新封裝的屬性。  
  
-   在執行階段擴展 Transact-SQL 陳述式的參數值。  
  
-   控制 Foreach 迴圈的流程。 如需詳細資訊，請參閱[加入列舉型別控制流程](http://msdn.microsoft.com/library/f212b5fb-3cc4-422e-9b7c-89eb769a812a)。  
  
-   按照運算式中的用途控制優先順序條件約束。 優先順序條件約束可以包含條件約束定義中的變數。 如需詳細資訊，請參閱 [將運算式加入優先順序條件約束](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1)。  
  
-   控制 For 迴圈容器的條件式重複。 如需詳細資訊，請參閱[加入反覆項目控制流程](http://msdn.microsoft.com/library/eb3a7494-88ae-4165-9d0f-58715eb1734a)。  
  
-   建立包含變數值的運算式。  
  
-   您可以建立所有容器類型的自訂變數： 封裝， **Foreach 迴圈**容器**For 迴圈 」**容器，**順序**容器、 Taskhost 和事件處理常式。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="scope"></a>범위  
 每個容器有它自己的 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合。 在建立新變數時，它在其父容器的範圍內。 因為封裝容器位於容器階層的最上層，所以具有封裝範圍的變數在功能上與全域變數相同，而且在封裝中的所有容器都可以看到它們。 透過使用集合中的變數名稱或是變數的索引，容器的子系也可以透過 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合來存取容器的變數集合。  
  
 因為變數的可見性範圍是從上向下，所以封裝中的所有容器都可以看到在封裝層級宣告的變數。 因此，在容器上的 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合除了自己的變數以外，還會包括屬於其父系的所有變數。  
  
 相反的，包含在工作中的變數其範圍和可見性則有限，只有工作看得到它們。  
  
 如果封裝執行其他封裝，則定義在呼叫封裝範圍中的變數可用於所呼叫的封裝。 只有在所呼叫的封裝中有相同名稱的變數時，才會發生例外狀況。 發生衝突時，在所呼叫的封裝中之變數值會覆寫來自呼叫封裝的值。 定義在所呼叫的封裝範圍中之變數絕對無法用於呼叫封裝中。  
  
 下列程式碼範例以程式設計方式在封裝範圍建立變數 `myCustomVar`，然後在封裝可看見的所有變數中反覆運算，以列印其名稱、資料類型與值。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application app = new Application();  
      // Load a sample package that contains a variable that sets the file name.  
      Package pkg = app.LoadPackage(  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",  
        null);  
      Variables pkgVars = pkg.Variables;  
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");  
      foreach (Variable pkgVar in pkgVars)  
      {  
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,  
          pkgVar.DataType, pkgVar.Value.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim app As Application = New Application()  
    ' Load a sample package that contains a variable that sets the file name.  
    Dim pkg As Package = app.LoadPackage( _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _  
      Nothing)  
    Dim pkgVars As Variables = pkg.Variables  
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")  
    Dim pkgVar As Variable  
    For Each pkgVar In pkgVars  
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _  
        pkgVar.DataType, pkgVar.Value.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **範例輸出：**  
  
 `Variable: CancelEvent, Int32, 0`  
  
 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`  
  
 `Variable: CreatorComputerName, String,`  
  
 `Variable: CreatorName, String,`  
  
 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`  
  
 `Variable: FileName, String, Junk`  
  
 `Variable: InteractiveMode, Boolean, False`  
  
 `Variable: LocaleID, Int32, 1033`  
  
 `Variable: MachineName, String, MYCOMPUTERNAME`  
  
 `Variable: myCustomVar, String, 3`  
  
 `Variable: OfflineMode, Boolean, False`  
  
 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`  
  
 `Variable: PackageName, String, DTSPackage1`  
  
 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`  
  
 `Variable: UserName, String, <domain>\<userid>`  
  
 `Variable: VersionBuild, Int32, 198`  
  
 `Variable: VersionComments, String,`  
  
 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`  
  
 `Variable: VersionMajor, Int32, 1`  
  
 `Variable: VersionMinor, Int32, 0`  
  
 請注意，所有的變數範圍中**系統**命名空間會提供給封裝。 如需詳細資訊，請參閱 [系統變數](../../integration-services/system-variables.md)。  
  
## <a name="namespaces"></a>命名空間  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 提供兩個預設命名空間，其中變數存在於**使用者**和**系統**命名空間。 根據預設，開發人員建立的任何自訂變數加入至**使用者**命名空間。 系統變數位於**系統**命名空間。 您可以建立其他命名空間以外**使用者**命名空間來容納自訂變數，而您可以變更名稱**使用者**命名空間，但您無法加入或修改中的變數**系統**命名空間，或系統變數指派給不同的命名空間。  
  
 可使用的系統變數會因容器類型而異。 如需可用來封裝、 容器、 工作和事件處理常式的系統變數的清單，請參閱[系統變數](../../integration-services/system-variables.md)。  
  
## <a name="value"></a>Value  
 自訂變數值可以是常值或是運算式：  
  
-   如果您希望變數包含常值，請設定其 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> 屬性值。  
  
-   如果您想要變數包含運算式，以便您可以使用運算式的結果做為其值，設定<xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A>變數的屬性**true**，並提供的運算式中<xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A>屬性。 在執行階段會評估運算式，而且運算式的結果會做為變數值。 例如，如果變數的運算式屬性是 `"100 * 2""100 * 2"`，則變數會將值評估為 200。  
  
 對於變數，您無法明確地設定其 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 的值。 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 值是從指派給變數的初始值來推斷，而且之後不能變更。 如需有關變數資料類型的詳細資訊，請參閱[Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 下列程式碼範例會建立新的變數集<xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A>至**true**，將運算式指派`"100 * 2"`變數的運算式屬性然後輸出變數的值。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package pkg = new Package();  
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);  
      v100.EvaluateAsExpression = true;  
      v100.Expression = "100 * 2";  
      Console.WriteLine("Expression for myVar: {0}",   
        v100.Properties["Expression"].GetValue(v100));  
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkg As Package = New Package  
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)  
    v100.EvaluateAsExpression = True  
    v100.Expression = "100 * 2"  
    Console.WriteLine("Expression for myVar: {0}", _  
      v100.Properties("Expression").GetValue(v100))  
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **範例輸出：**  
  
 `Expression for myVar: 100 * 2`  
  
 `Value of myVar: 200`  
  
 運算式必須是使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 運算式語法的有效運算式。 除了運算式語法提供的運算子與函數之外，變數運算式中還允許常值，但是運算式無法參考其他變數或是資料行。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)為止。  
  
## <a name="configuration-files"></a>組態檔  
 如果組態檔包含自訂變數，則可以在執行階段更新變數。 這表示當封裝執行時，會使用組態檔中的新值來取代原本在封裝中的變數值。 當將封裝部署到需要不同變數值的多部伺服器時，這個取代技術將特別有用。 例如，變數可以指定的次數**Foreach 迴圈**容器重複其工作流程或清單的收件者的事件處理常式會傳送電子郵件給引發錯誤時，或變更封裝失敗之前可以發生的錯誤數目。 這些變數是在每個環境的組態檔中動態提供的。 因此，在組態檔中只允許讀取/寫入的變數。 如需詳細資訊，請參閱[建立封裝組態](../../integration-services/packages/create-package-configurations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;變數](../../integration-services/integration-services-ssis-variables.md)   
 [在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
