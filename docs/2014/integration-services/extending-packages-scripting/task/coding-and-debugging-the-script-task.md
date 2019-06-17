---
title: 編碼和偵錯指令碼工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], debugging
- SSIS Script task, development environment
- SSIS Script task, debugging
- Script task [Integration Services], development environment
- Script task [Integration Services], coding
- debugging [Integration Services], scripts
- VSTA
- SSIS Script task, coding
ms.assetid: 687c262f-fcab-42e8-92ae-e956f3d92d69
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 620b778069ef45deeeb5552296798736a1ebe5f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768407"
---
# <a name="coding-and-debugging-the-script-task"></a>指令碼工作的程式碼撰寫和偵錯
  在 [指令碼工作編輯器]  中設定指令碼工作之後，於指令碼工作開發環境中撰寫自訂程式碼。  
  
## <a name="script-task-development-environment"></a>指令碼工作開發環境  
 指令碼工作使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 作為指令碼本身的開發環境。  
  
 指令碼是以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 撰寫。 您可以在 [指令碼工作編輯器]  中設定 [ScriptLanguage]  屬性來指定指令碼語言。 如果想要使用其他的程式語言，可以用您所選的語言開發自訂組件，然後在指令碼工作中，從程式碼呼叫其功能。  
  
 您在指令碼工作中建立的指令碼會儲存在封裝定義中， 而沒有個別的指令碼檔案。 因此，使用指令碼工作並不會影響封裝部署。  
  
> [!NOTE]  
>  當您設計封裝和偵錯指令碼時，指令碼會暫時寫入專案檔案。 因為將敏感資訊儲存在檔案中會造成潛在的安全性風險，所以我們建議您不要在指令碼中包含密碼之類的敏感資訊。  
  
 依預設，在 IDE 中會停用 `Option Strict`。  
  
## <a name="script-task-project-structure"></a>指令碼工作專案結構  
 當您建立或修改包含在指令碼工作中的指令碼時，VSTA 會開啟空的新專案或是重新開啟現有的專案。 這個 VSTA 專案的建立不會影響專案的部署，因為專案是儲存在封裝檔案中；指令碼工作不會建立其他檔案。  
  
### <a name="project-items-and-classes-in-the-script-task-project"></a>指令碼工作專案中的專案項目和類別  
 依預設，顯示在 VSTA [專案總管] 視窗中的指令碼工作專案包含單一項目：`ScriptMain`。 `ScriptMain` 項目則包含單一類別，同樣名為 `ScriptMain`。 類別中的程式碼項目會根據您針對指令碼工作所選取的程式語言而變更。  
  
-   當指令碼工作已針對[!INCLUDE[vb_orcas_long](../../../includes/vb-orcas-long-md.md)]程式設計語言，`ScriptMain`類別具有公用的副程式： `Main`。 `ScriptMain.Main` 副程式是當您執行指令碼工作時，執行階段呼叫的方法。  
  
     依預設，在新指令碼的 `Main` 副程式中的唯一程式碼是 `Dts.TaskResult = ScriptResults.Success` 這一行。 這行會通知執行階段，工作的作業已成功。 `Dts.TaskResult`屬性中所提及[Returning Results from 指令碼工作](../../extending-packages-scripting/task/returning-results-from-the-script-task.md)。  
  
-   當為 Visual C# 程式語言設定指令碼工作時，`ScriptMain` 類別具有公用的方法 `Main`。 此方法是在指令碼工作執行時呼叫。  
  
     依預設，`Main` 方法包括此行：`Dts.TaskResult = (int)ScriptResults.Success`。 這行會通知執行階段，工作的作業已成功。  
  
 `ScriptMain` 項目可以包含 `ScriptMain` 類別以外的類別。 類別僅可供其所在的指令碼工作使用。  
  
 依預設，`ScriptMain` 專案項目包含下列自動產生的程式碼。 程式碼範本也會提供指令碼工作的概觀，以及有關如何擷取與操作 SSIS 物件 (例如變數、事件與連接) 的其他資訊。  
  
```vb  
' Microsoft SQL Server Integration Services Script Task  
' Write scripts using Microsoft Visual Basic 2008.  
' The ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime.VSTAProxy  
  
<System.AddIn.AddIn("ScriptMain", Version:="1.0", Publisher:="", Description:="")> _  
Partial Class ScriptMain  
  
Private Sub ScriptMain_Startup(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Startup  
  
End Sub  
  
Private Sub ScriptMain_Shutdown(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Shutdown  
Try  
' Unlock variables from the read-only and read-write variable collection properties  
If (Dts.Variables.Count <> 0) Then  
Dts.Variables.Unlock()  
End If  
Catch ex As Exception  
        End Try  
End Sub  
  
Enum ScriptResults  
Success = DTSExecResult.Success  
Failure = DTSExecResult.Failure  
End Enum  
  
' The execution engine calls this method when the task executes.  
' To access the object model, use the Dts property. Connections, variables, events,  
' and logging features are available as members of the Dts property as shown in the following examples.  
'  
' To reference a variable, call Dts.Variables("MyCaseSensitiveVariableName").Value  
' To post a log entry, call Dts.Log("This is my log text", 999, Nothing)  
' To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, True)  
'  
' To use the connections collection use something like the following:  
' ConnectionManager cm = Dts.Connections.Add("OLEDB")  
' cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;"  
'  
' Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
'   
' To open Help, press F1.  
  
Public Sub Main()  
'  
' Add your code here  
'  
Dts.TaskResult = ScriptResults.Success  
End Sub  
  
End Class  
```  
  
```csharp  
/*  
   Microsoft SQL Server Integration Services Script Task  
   Write scripts using Microsoft Visual C# 2008.  
   The ScriptMain is the entry point class of the script.  
*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime.VSTAProxy;  
using System.Windows.Forms;  
  
namespace ST_1bcfdbad36d94f8ba9f23a10375abe53.csproj  
{  
    [System.AddIn.AddIn("ScriptMain", Version = "1.0", Publisher = "", Description = "")]  
    public partial class ScriptMain  
    {  
        private void ScriptMain_Startup(object sender, EventArgs e)  
        {  
  
        }  
  
        private void ScriptMain_Shutdown(object sender, EventArgs e)  
        {  
            try  
            {  
                // Unlock variables from the read-only and read-write variable collection properties  
                if (Dts.Variables.Count != 0)  
                {  
                    Dts.Variables.Unlock();  
                }  
            }  
            catch  
            {  
            }  
        }  
  
        #region VSTA generated code  
        private void InternalStartup()  
        {  
            this.Startup += new System.EventHandler(ScriptMain_Startup);  
            this.Shutdown += new System.EventHandler(ScriptMain_Shutdown);  
        }  
        enum ScriptResults  
        {  
            Success = DTSExecResult.Success,  
            Failure = DTSExecResult.Failure  
        };  
  
        #endregion  
  
        /*  
The execution engine calls this method when the task executes.  
To access the object model, use the Dts property. Connections, variables, events,  
and logging features are available as members of the Dts property as shown in the following examples.  
  
To reference a variable, call Dts.Variables["MyCaseSensitiveVariableName"].Value;  
To post a log entry, call Dts.Log("This is my log text", 999, null);  
To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, true);  
  
To use the connections collection use something like the following:  
ConnectionManager cm = Dts.Connections.Add("OLEDB");  
cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;";  
  
Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
  
To open Help, press F1.  
*/  
  
        public void Main()  
        {  
            // TODO: Add your code here  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
    }  
```  
  
### <a name="additional-project-items-in-the-script-task-project"></a>指令碼工作專案中的其他專案項目  
 指令碼工作專案可以包含預設 `ScriptMain` 項目以外的項目。 您可以將類別、模組和程式碼檔案加入專案。 您也可以使用資料夾來組織項目的群組。 所有您加入的項目都會保存在封裝內。  
  
### <a name="references-in-the-script-task-project"></a>指令碼工作專案中的參考  
 您可以在 [專案總管]  中以滑鼠右鍵按一下「指令碼」工作專案，再按 [新增參考]  ，新增 Managed 組件的參考。 如需詳細資訊，請參閱[參考指令碼解決方案中的其他組件](../referencing-other-assemblies-in-scripting-solutions.md)。  
  
> [!NOTE]  
>  您可以在 VSTA IDE 中的 [類別檢視]  或 [專案總管]  中，檢視專案參考。 您可以從 [檢視]  功能表中開啟任一個視窗。 您可以從 [專案]  功能表、[專案總管]  或 [類別檢視]  新增參考。  
  
## <a name="interacting-with-the-package-in-the-script-task"></a>與指令碼工作中的封裝互動  
 指令碼工作使用全域 `Dts` 物件 (<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> 類別的執行個體) 及其成員與包含封裝和 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段互動。  
  
 下表列出 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> 類別的主要公用成員，這個類別是透過全域 `Dts` 物件向指令碼工作程式碼公開。 本節中的主題會更詳細地討論這些成員的使用。  
  
|成員|用途|  
|------------|-------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>|提供定義在封裝中的連接管理員之存取權。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>|提供事件介面，讓指令碼工作引發錯誤、警告及參考訊息。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>|提供簡單的方法將 `TaskResult` 以外的單一物件傳回執行階段，也可用於工作流程分支。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>|將工作進度與結果等資訊記錄到啟用的記錄提供者。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>|報告工作的成功或失敗。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Transaction%2A>|提供工作的容器執行範圍內的交易 (如果有的話)。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>|提供列在 `ReadOnlyVariables` 與 `ReadWriteVariables` 工作屬性中的變數存取權，以供在指令碼中使用。|  
  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> 類別也包含一些您可能不會使用的公用成員。  
  
|成員|描述|  
|------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性會提供更為便利的變數存取方式。 雖然您可以使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>，但是必須明確地呼叫方法以鎖定和解除鎖定要讀取和寫入的變數。 當您使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性時，指令碼工作會為您處理鎖定語意。|  
  
## <a name="debugging-the-script-task"></a>偵錯指令碼工作  
 若要偵錯指令碼工作中的程式碼，請在程式碼中設定至少一個中斷點，然後關閉 VSTA IDE 以便在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中執行封裝。 當封裝執行進入指令碼工作時，VSTA IDE 會在唯讀模式下重新開啟和顯示您的程式碼。 在執行到達中斷點之後，您可以檢查變數值並逐步完成其餘的程式碼。  
  
> [!WARNING]  
>  您可以在以 64 位元模式執行封裝時，為指令碼工作偵錯。  
  
> [!NOTE]  
>  您必須執行封裝以進入指令碼工作中偵錯。 如果您只執行個別的工作，則會忽略指令碼工作程式碼內的中斷點。  
  
> [!NOTE]  
>  當您在「執行封裝工作」的子封裝內執行指令碼工作時，將無法偵錯指令碼工作。 在這些情況下，會略過您在子封裝的指令碼工作中設定的中斷點。 您可以分開執行子封裝，以利正常地偵錯子封裝。  
  
> [!NOTE]  
>  當您偵錯包含多個指令碼工作的封裝時，偵錯工具會偵錯其中一個指令碼工作。 如果偵錯工具完成，系統就可以偵錯另一個指令碼工作，如同 Foreach 迴圈或 For 迴圈容器的情況。  
  
## <a name="external-resources"></a>外部資源  
  
-   blogs.msdn.com 上的部落格文章：[VSTA setup and configuration troubles for SSIS 2008 and R2 installations](https://go.microsoft.com/fwlink/?LinkId=215661) (SSIS 2008 和 R2 安裝的 VSTA 安裝與設定問題)。  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的最新下載、文件、範例和影片以及社群中的選定方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [參考指令碼解決方案中的其他組件](../referencing-other-assemblies-in-scripting-solutions.md)   
 [在指令碼工作編輯器設定指令碼工作](configuring-the-script-task-in-the-script-task-editor.md)  
  
  
