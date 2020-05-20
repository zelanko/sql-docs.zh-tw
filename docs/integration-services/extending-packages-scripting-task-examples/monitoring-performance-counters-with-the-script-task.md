---
title: 以指令碼工作監視效能計數器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ed4bca496d48e5fe268c1a425223fe03c8fcc6e7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297032"
---
# <a name="monitoring-performance-counters-with-the-script-task"></a>以指令碼工作監視效能計數器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  系統管理員可能需要監視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝在大量資料執行複雜轉換時的效能。   的 [!INCLUDE[msCoName](../../includes/msconame-md.md)]System.Diagnostics[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 命名空間提供可讓您使用現有效能計數器或建立自訂效能計數器的類別。  
  
 效能計數器會儲存應用程式效能資訊，可用以分析某段時間的軟體效能。 透過使用 [效能監視器]  工具，就可以在本機或是遠端監視效能計數器。 您可以將效能計數器值儲存在變數中，以供之後在封裝中的控制流程分支使用。  
  
 若不使用效能計數器，您也可以透過 **Dts** 物件的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 屬性，引發 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 事件。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 事件會將增加的進度與百分比完成資訊傳回 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>描述  
 下列範例會建立自訂效能計數器並遞增計數器。 首先，範例會判斷效能計數器是否已經存在。 如果尚未建立效能計數器，指令碼會呼叫 **PerformanceCounterCategory** 物件的 **Create** 方法。 在建立效能計數器之後，指令碼會遞增計數器。 最後，下面將提供範例說明當不再需要效能計數器時，呼叫效能計數器上的 **Close** 方法之最佳做法。  
  
> [!NOTE]  
>  建立新的效能計數器類別以及效能計數器需要系統管理權限。 另外，在建立新的類別與計數器之後，會保存在電腦上。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
-   使用程式碼中的 **Imports** 陳述式匯入 **System.Diagnostics** 命名空間。  
  
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
