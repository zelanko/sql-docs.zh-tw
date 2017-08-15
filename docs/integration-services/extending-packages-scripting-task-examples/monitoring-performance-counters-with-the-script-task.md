---
title: "監視效能計數器 with the Script Task |Microsoft 文件"
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
helpviewer_keywords:
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: fd733f7d2fdf9c5d1181df6e7856d729e9a58026
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="monitoring-performance-counters-with-the-script-task"></a>以指令碼工作監視效能計數器
  系統管理員可能需要監視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝在大量資料執行複雜轉換時的效能。 **System.Diagnostics**命名空間的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供類別，以使用現有效能計數器並建立您自己的效能計數器。  
  
 效能計數器會儲存應用程式效能資訊，可用以分析某段時間的軟體效能。 監視效能計數器可以是本機或遠端方式使用**效能監視器**工具。 您可以將效能計數器值儲存在變數中，以供之後在封裝中的控制流程分支使用。  
  
 您可以使用效能計數器的替代方案，以提高<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A>事件到<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>屬性**Dts**物件。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 事件會將增加的進度與百分比完成資訊傳回 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下列範例會建立自訂效能計數器並遞增計數器。 首先，範例會判斷效能計數器是否已經存在。 如果效能計數器尚未建立，指令碼會呼叫**建立**方法**PerformanceCounterCategory**物件來建立它。 在建立效能計數器之後，指令碼會遞增計數器。 最後，此範例會遵循最佳作法來呼叫**關閉**時不再需要效能計數器上的方法。  
  
> [!NOTE]  
>  建立新的效能計數器類別以及效能計數器需要系統管理權限。 另外，在建立新的類別與計數器之後，會保存在電腦上。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
-   使用**匯入**匯入程式碼中的陳述式**System.Diagnostics**命名空間。  
  
### <a name="example-code"></a>範例程式碼  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  

