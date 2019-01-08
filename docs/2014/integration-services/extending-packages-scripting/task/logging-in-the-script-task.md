---
title: 登入指令碼工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- logs [Integration Services], scripts
- Integration Services packages, logs
- Log method
- SSIS Script task, logs
- Script task [Integration Services], logs
- packages [Integration Services], logs
ms.assetid: 2e11fc15-df18-4309-bd2d-fc58aa4b9b7a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c46528a51f8dae36b2b47afe2086a6eac1b72428
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359500"
---
# <a name="logging-in-the-script-task"></a>在指令碼工作中記錄
  在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝中使用記錄可以讓您藉由記錄預先定義事件或使用者定義訊息，記錄關於執行進度、結果和問題的詳細資訊以供稍後分析。 指令碼工作可以使用 `Dts` 物件的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法記錄使用者定義的資料。 如果記錄已啟用，而且已在 [設定 SSIS 記錄] 對話方塊的 [詳細資料] 索引標籤上選取 **ScriptTaskLogEntry** 事件以進行記錄，<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法的呼叫會儲存為工作設定之所有記錄提供者中的事件資訊。  
  
> [!NOTE]  
>  雖然您可以直接從指令碼工作執行記錄，不過可能會想考慮實作事件，而不是記錄。 使用事件時，不僅可以啟用事件訊息的記錄，還可用預設或使用者定義的事件處理常式回應事件。  
  
 如需記錄的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../performance/integration-services-ssis-logging.md)。  
  
## <a name="logging-example"></a>記錄範例  
 下列範例示範如何透過記錄代表已處理的資料列數目值，從指令碼工作進行記錄。  
  
```vb  
Public Sub Main()  
  
    Dim rowsProcessed As Integer = 100  
    Dim emptyBytes(0) As Byte  
  
    Try  
        Dts.Log("Rows processed: " & rowsProcessed.ToString, _  
            0, _  
            emptyBytes)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
            //  
            int rowsProcessed = 100;  
            byte[] emptyBytes = new byte[0];  
  
            try  
            {  
                Dts.Log("Rows processed: " + rowsProcessed.ToString(), 0, emptyBytes);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                //An error occurred.  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
```  
  
 }  
  
## <a name="external-resources"></a>外部資源  
  
-   dougbert.com 上的部落格文章：[Logging custom events for Integration Services tasks](https://go.microsoft.com/fwlink/?LinkId=165644) (記錄 Integration Services 工作的自訂事件)  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](../../performance/integration-services-ssis-logging.md)  
  
  
