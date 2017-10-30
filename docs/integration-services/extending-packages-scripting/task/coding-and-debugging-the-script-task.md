---
title: "編碼和偵錯指令碼工作 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 81
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8c706fc1db3e31130a7754b9e4c3d16f9a13eaf4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="coding-and-debugging-the-script-task"></a>指令碼工作的程式碼撰寫和偵錯
  之後設定指令碼工作中**指令碼工作編輯器**，您在指令碼工作開發環境中撰寫自訂程式碼。  
  
## <a name="script-task-development-environment"></a>指令碼工作開發環境  
 指令碼工作使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 做為指令碼本身的開發環境。  
  
 指令碼是以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 撰寫。 您可以設定指定的指令碼語言**ScriptLanguage**屬性**指令碼工作編輯器**。 如果想要使用其他的程式語言，可以用您所選的語言開發自訂組件，然後在指令碼工作中，從程式碼呼叫其功能。  
  
 您在指令碼工作中建立的指令碼會儲存在封裝定義中， 而沒有個別的指令碼檔案。 因此，使用指令碼工作並不會影響封裝部署。  
  
> [!NOTE]  
>  當您設計封裝和偵錯指令碼時，指令碼會暫時寫入專案檔案。 因為將敏感資訊儲存在檔案中會造成潛在的安全性風險，所以我們建議您不要在指令碼中包含密碼之類的敏感資訊。  
  
 根據預設， **Option Strict** IDE 中已停用。  
  
## <a name="script-task-project-structure"></a>指令碼工作專案結構  
 當您建立或修改包含在指令碼工作中的指令碼時，VSTA 會開啟空的新專案或是重新開啟現有的專案。 這個 VSTA 專案的建立不會影響專案的部署，因為專案是儲存在封裝檔案中；指令碼工作不會建立其他檔案。  
  
### <a name="project-items-and-classes-in-the-script-task-project"></a>指令碼工作專案中的專案項目和類別  
 根據預設，在 VSTA [專案總管] 視窗中顯示的指令碼工作專案包含單一項目， **ScriptMain**。 **ScriptMain**項目，依序包含單一類別，也稱為**ScriptMain**。 類別中的程式碼項目會根據您針對指令碼工作所選取的程式語言而變更。  
  
-   當指令碼工作時設定為[!INCLUDE[vb_orcas_long](../../../includes/vb-orcas-long-md.md)]程式設計語言， **ScriptMain**類別具有公用的副程式： **Main**。 **ScriptMain.Main**副程式是當您執行指令碼工作時，執行階段呼叫的方法。  
  
     根據預設，唯一的程式碼中**Main**副程式，新的指令碼是以`Dts.TaskResult = ScriptResults.Success`。 這行會通知執行階段，工作的作業已成功。 **Dts.TaskResult**屬性述[Returning Results from 指令碼工作](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)。  
  
-   設定指令碼工作時的 Visual C# 程式語言， **ScriptMain**類別具有公用的方法， **Main**。 此方法是在指令碼工作執行時呼叫。  
  
     根據預設， **Main**方法包括此行`Dts.TaskResult = (int)ScriptResults.Success`。 這行會通知執行階段，工作的作業已成功。  
  
 **ScriptMain**項目可以包含類別以外**ScriptMain**類別。 類別僅可供其所在的指令碼工作使用。  
  
 根據預設， **ScriptMain**專案項目包含下列自動產生程式碼。 程式碼範本也會提供指令碼工作的概觀，以及有關如何擷取與操作 SSIS 物件 (例如變數、事件與連接) 的其他資訊。  
  
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
 指令碼工作專案可以包含預設值以外的項目**ScriptMain**項目。 您可以將類別、模組和程式碼檔案加入專案。 您也可以使用資料夾來組織項目的群組。 所有您加入的項目都會保存在封裝內。  
  
### <a name="references-in-the-script-task-project"></a>指令碼工作專案中的參考  
 您可以加入至 managed 組件的參考，以滑鼠右鍵按一下中的指令碼工作專案**Project Explorer**，然後按一下**加入參考**。 如需詳細資訊，請參閱[指令碼的方案中參考其他組件](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)。  
  
> [!NOTE]  
>  您可以在 VSTA IDE 中檢視專案參考**類別檢視**或**Project Explorer**。 您可以開啟其中一個這些 windows 從**檢視**功能表。 您可以加入新的參考從**專案**功能表上，從**Project Explorer**，或從**類別檢視**。  
  
## <a name="interacting-with-the-package-in-the-script-task"></a>與指令碼工作中的封裝互動  
 指令碼工作使用全域**Dts**物件，它是執行個體的<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel>類別和互動與包含封裝和其成員[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]執行階段。  
  
 下表列出主要公用成員<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel>類別公開給指令碼工作程式碼，透過全域**Dts**物件。 本節中的主題會更詳細地討論這些成員的使用。  
  
|成員|目的|  
|------------|-------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>|提供定義在封裝中的連接管理員之存取權。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>|提供事件介面，讓指令碼工作引發錯誤、警告及參考訊息。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>|提供簡單的方法來傳回單一物件執行階段 (除了**TaskResult**)，可以也可用於工作流程分支。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>|將工作進度與結果等資訊記錄到啟用的記錄提供者。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>|報告工作的成功或失敗。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Transaction%2A>|提供工作的容器執行範圍內的交易 (如果有的話)。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>|提供變數中所列的存取權**[readonlyvariables]**和**[readwritevariables]**工作屬性以供在指令碼中使用。|  
  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> 類別也包含一些您可能不會使用的公用成員。  
  
|成員|Description|  
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
  
-   部落格文章： [SSIS 2008 和 R2 安裝的 VSTA 設定與組態問題](http://go.microsoft.com/fwlink/?LinkId=215661)，blogs.msdn.com 上。  
  
## <a name="see-also"></a>另請參閱  
 [參考指令碼的方案中其他組件](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)   
 [在指令碼工作編輯器中設定指令碼工作](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
  
  

