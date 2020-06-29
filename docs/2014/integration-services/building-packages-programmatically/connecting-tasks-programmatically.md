---
title: 以程式設計方式連線工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- constraints [Integration Services]
ms.assetid: 23668e88-cef4-4009-a9cf-38e607eab7a2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ef26da592675d9d3b6c7a08b08ebc112a84e55e9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439225"
---
# <a name="connecting-tasks-programmatically"></a>以程式設計方式連接工作
  在物件模型中由 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 類別表示的優先順序條件約束會建立 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 物件在封裝內執行的順序。 此優先順序條件約束可允許根據上一個工作或容器的執行結果來執行封裝中的容器和工作。 優先順序條件約束會在 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 物件配對之間建立，其方式是在容器物件上呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints.Add%2A> 集合的 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints> 方法。 當您在兩個可執行物件之間建立條件約束時，您會設定 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> 屬性，以建立用來執行此條件約束內定義之第二個可執行物件的準則。  
  
 您可以在單一優先順序條件約束內同時使用條件約束和運算式，這是根據您為 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.EvalOp%2A> 屬性指定的值而定，如下表所述：  
  
|EvalOp 屬性的值|描述|  
|----------------------------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Constraint>|指定執行結果會決定是否執行受條件約束的容器或工作。 將 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 屬性設定為 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列舉中所要的值。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Expression>|指定運算式的值會決定是否執行受條件約束的容器或工作。 設定 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 屬性。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionAndConstraint>|指定條件約束結果必須發生而且運算式必須評估，受條件約束的容器或工作才能執行。 設定 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 屬性，並且將其 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> 屬性設為 `true`。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionOrConstraint>|指定必須發生條件約束結果或者必須評估運算式，受條件約束的容器或工作才能執行。 設定 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 屬性，並且將其 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> 屬性設為 `false`。|  
  
 下列程式碼範例示範如何將兩個工作加入封裝中。 在兩者之間建立了 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>，防止第二個工作在第一個工作完成以前執行。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      // Add a File System task.  
      Executable eFileTask1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost1 = eFileTask1 as TaskHost;  
  
      // Add a second File System task.  
      Executable eFileTask2 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost2 = eFileTask2 as TaskHost;  
  
      // Put a precedence constraint between the tasks.  
      // Set the constraint to specify that the second File System task cannot run  
      // until the first File System task finishes.  
      PrecedenceConstraint pcFileTasks =   
        p.PrecedenceConstraints.Add((Executable)thFileHost1, (Executable)thFileHost2);  
      pcFileTasks.Value = DTSExecResult.Completion;  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task.  
    Dim eFileTask1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost1 As TaskHost = CType(eFileTask1, TaskHost)  
  
    ' Add a second File System task.  
    Dim eFileTask2 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost2 As TaskHost = CType(eFileTask2, TaskHost)  
  
    ' Put a precedence constraint between the tasks.  
    ' Set the constraint to specify that the second File System task cannot run  
    ' until the first File System task finishes.  
    Dim pcFileTasks As PrecedenceConstraint = _  
      p.PrecedenceConstraints.Add(CType(thFileHost1, Executable), CType(thFileHost2, Executable))  
    pcFileTasks.Value = DTSExecResult.Completion  
  
  End Sub  
  
End Module  
```  
  
![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式加入資料流程工作](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
  
  
