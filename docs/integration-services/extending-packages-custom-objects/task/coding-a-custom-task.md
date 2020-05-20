---
title: 撰寫自訂工作的程式碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Validate method
- custom tasks [Integration Services], validating
- validation [Integration Services], design-time tasks
- SSIS custom tasks, validating
ms.assetid: dc224f4f-b339-4eb6-a008-1b4fe0ea4fd2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23cea7d670916db9dfd13fa37170967a3c19d11c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297122"
---
# <a name="coding-a-custom-task"></a>撰寫自訂工作的程式碼

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  建立繼承自 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 基底類別的類別，並將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 屬性 (attribute) 套用到類別之後，必須覆寫基底類別的屬性 (properties) 與方法的實作，才可提供自訂功能。  
  
## <a name="configuring-the-task"></a>設定工作  
  
### <a name="validating-the-task"></a>驗證工作  
 當您在設計 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝時，可以使用驗證來確認每個工作上的設定，這樣您就可以盡早在設定時擷取到不正確或不當的設定值，而不是只能夠在執行階段尋找所有的錯誤。 驗證的目的就是要判斷工作是否包含使其無法成功執行的無效設定或是連接。 這可確保封裝所包含的工作在第一次執行時，就可以順利地執行。  
  
 您可以在自訂程式碼中使用 **Validate** 方法來實作驗證。 執行階段引擎會透過呼叫在工作上的 **Validate** 方法來驗證工作。 工作開發人員的責任就是要定義可判斷工作成功或失敗的驗證準則，並通知執行階段引擎此驗證的結果。  
  
#### <a name="task-abstract-base-class"></a>工作抽象基底類別  
 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 抽象基底類別提供的 **Validate** 方法，可由每個工作覆寫以定義其驗證準則。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計工具會自動在套件設計期間呼叫 **Validate** 方法多次，並在警告或錯誤發生時，提供視覺提示給使用者，以協助識別工作設定中的問題。 工作透過從 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列舉傳回值，以及透過引發警告和錯誤事件，來提供驗證結果。 這些事件包含對 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中的使用者顯示的資訊。  
  
 以下是一些驗證範例：  
  
-   連接管理員會驗證特定的檔案名稱。  
  
-   連接管理員會驗證輸入的類型是否為預期的類型，例如 XML 檔案。  
  
-   需要資料庫輸入的工作會確認它無法從非資料庫連接接收資料。  
  
-   工作會保證其所有屬性都不會與相同工作上設定的其他屬性衝突。  
  
-   工作會保證其在執行時需要使用的全部資源都可以使用。  
  
 在判斷要驗證的項目時，需要考量的另一個層面是效能。 例如，工作的輸入可能是透過低頻寬網路或高流量網路的連接。 如果您決定驗證該資源是否可用，驗證可能需要花費數秒的處理時間。 另一項驗證可能會造成需要大量地往返於伺服器之間，而且驗證常式可能會變慢。 雖然有許多屬性和設定都可加以驗證，但這不表示您該驗證所有項目。  
  
-   在執行工作之前，<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 也會呼叫 **Validate** 方法中的程式碼，而且如果驗證失敗，<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 會取消執行。  
  
#### <a name="user-interface-considerations-during-validation"></a>在驗證期間的使用者介面考量  
 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 包含 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 介面以作為 **Validate** 方法的參數。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 介面包含工作向執行階段引擎引發事件所呼叫的方法。 當警告或是錯誤狀況在驗證期間發生時，會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> 方法。 這兩個警告方法都需要相同的參數，包含錯誤碼、來源元件、描述、說明檔以及說明內容資訊。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師使用此資訊在設計介面上顯示視覺提示。 設計師提供的視覺提示包括出現在設計師介面上工作旁邊的驚嘆號圖示。 此視覺提示提醒使用者工作需要其他組態，執行才可以繼續。  
  
 驚嘆號圖示也會顯示包含錯誤訊息的工具提示。 工作會在事件的描述參數中提供錯誤訊息。 錯誤訊息也會顯示在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 的 [工作清單] 窗格中，這個窗格為使用者提供檢視所有驗證錯誤的集中位置。  
  
#### <a name="validation-example"></a>驗證範例  
 下列程式碼範例示範如何使用 **UserName** 屬性的工作。 已指定此屬性為成功驗證所需。 如果未設定此屬性，工作會公佈錯誤，並從 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Failure> 列舉傳回 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>。 **Validate** 方法會包裝在 Try/Catch 區塊中，而且驗證會在發生例外狀況時失敗。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string userName = "";  
  
  public override DTSExecResult Validate(Connections connections,  
     VariableDispenser variableDispenser, IDTSComponentEvents events,  
     IDTSLogging log)  
  {  
    try  
    {  
      if (this.userName == "")  
      {  
        //   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0);  
        //   Fail validation.  
        return DTSExecResult.Failure;  
      }  
      //   Return success.  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string UserName  
  {  
    get  
    {  
      return this.userName;  
    }  
    set  
    {  
      this.userName = value;  
    }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _userName As String = ""  
  
  Public Overrides Function Validate(ByVal connections As Connections, _  
     ByVal variableDispenser As VariableDispenser, _  
     ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging) As DTSExecResult  
  
    Try  
      If Me._userName = "" Then  
        '   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0)  
        '   Fail validation.  
        Return DTSExecResult.Failure  
      End If  
      '   Return success.  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property UserName() As String  
    Get  
      Return Me._userName  
    End Get  
    Set(ByVal Value As String)  
      Me._userName = Value  
    End Set  
  End Property  
  
End Class  
```  
  
### <a name="persisting-the-task"></a>保存工作  
 一般而言，您不必實作工作的自訂持續性。 只有在物件的屬性使用複雜的資料類型時，才需要自訂持續性。 如需詳細資訊，請參閱[開發 Integration Services 的自訂物件](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)。  
  
## <a name="executing-the-task"></a>執行工作  
 本節描述如何使用工作所繼承和覆寫的 **Execute** 方法。 本節也會說明提供工作執行結果相關資訊的各種方法。  
  
### <a name="execute-method"></a>Execute 方法  
 套件中所含的工作會在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段呼叫其 **Execute** 方法時執行。 工作會在此方法中實作其核心商務邏輯與功能，並藉由張貼訊息、從 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列舉傳回值，以及覆寫 **ExecutionValue** 屬性的 **get** 屬性等方式，提供執行的結果。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 基底類別提供 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 方法的預設實作。 自訂工作會覆寫此方法以定義其執行階段功能。 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 物件會包裝工作，將工作與執行階段引擎和封裝中的其他物件隔離。 因為此隔離，工作不會知道它在封裝中與執行順序有關的位置，而且只會在執行階段呼叫工作時才執行。 這個架構可預防工作在執行期間修改封裝時可能發生的問題。 只有透過將封裝中的其他物件當做 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 方法中的參數提供給工作，該工作才能夠存取這些物件。 這些參數可以讓工作引發事件、將項目寫入事件記錄檔、存取變數集合以及將連接編列到交易中的資料來源，同時仍保有可保障封裝的穩定性和可靠性所需的隔離。  
  
 下表列出 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 方法中提供給工作的參數。  
  
|參數|描述|  
|---------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Connections>|包含可供工作使用的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件集合。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.VariableDispenser>|包含工作可用的變數。 工作會透過 VariableDispenser 來使用變數，不會直接使用變數。 變數分配程式會鎖定和解除鎖定變數，並防止死結或是覆寫。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents>|包含工作向執行階段引擎引發事件所呼叫的方法。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSLogging>|包含工作將項目寫入事件記錄檔所使用的方法和屬性。|  
|Object|包含容器所屬的交易物件 (如果有的話)。 這個值會當做參數傳遞至 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 物件的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 方法。|  
  
### <a name="providing-execution-feedback"></a>提供執行回饋  
 工作會在 **try/catch** 區塊中包裝其程式碼，以防止對執行階段引擎引發例外狀況。 這可確保封裝完成執行並且不會意外停止。 不過，執行階段引擎有提供其他機制，以處理可能在工作執行期間發生的錯誤狀況。 這些機制包括公佈錯誤與警告訊息、從 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 結構傳回值、公佈訊息、傳回 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 值，以及透過 <xref:Microsoft.SqlServer.Dts.Runtime.Task.ExecutionValue%2A> 屬性揭露工作執行結果的資訊。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 介面包含 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> 方法，工作可以呼叫這些方法以便將錯誤與警告訊息公佈到執行階段引擎。 這兩個方法都需要錯誤碼、來源元件、描述、說明檔以及說明內容資訊等參數。 視工作的組態而定，執行階段會藉由引發事件和中斷點或是將資訊寫入事件記錄檔中，以回應這些訊息。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 也提供 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> 屬性，可用以提供有關執行結果的其他資訊。 例如，如果工作從資料表刪除資料列，作為其 **Execute** 方法的一部分，它可能會傳回刪除的資料列數，以作為 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> 屬性的值。 此外，<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 提供 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecValueVariable%2A> 屬性。 此屬性可讓使用者將從工作傳回的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> 對應至工作可看到的任何變數。 然後，指定的變數可以用來建立工作間的優先順序條件約束。  
  
### <a name="execution-example"></a>執行範例  
 下列程式碼範例會示範 **Execute** 方法的實作，並顯示覆寫的 **ExecutionValue** 屬性。 工作會刪除工作的 **fileName** 屬性所指定的檔案。 如果檔案不存在，或者 **fileName** 屬性是空字串，則工作會張貼警告。 工作會傳回 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> 屬性中的 **Boolean** 值，以指出是否已刪除檔案。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string fileName = "";  
  private bool fileDeleted = false;  
  
  public override DTSExecResult Execute(Connections cons,  
     VariableDispenser vars, IDTSComponentEvents events,  
     IDTSLogging log, Object txn)  
  {  
    try  
    {  
      if (this.fileName == "")  
      {  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0);  
        this.fileDeleted = false;  
      }  
      else  
      {  
        if (System.IO.File.Exists(this.fileName))  
        {  
          System.IO.File.Delete(this.fileName);  
          this.fileDeleted = true;  
        }  
        else  
          this.fileDeleted = false;  
      }  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string FileName  
  {  
    get { return this.fileName; }  
    set { this.fileName = value; }  
  }  
  public override object ExecutionValue  
  {  
    get { return this.fileDeleted; }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _fileName As String = ""  
  Private _fileDeleted As Boolean = False  
  
  Public Overrides Function Execute(ByVal cons As Connections, _  
     ByVal vars As VariableDispenser, ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging, ByVal txn As Object) As DTSExecResult  
  
    Try  
      If Me._fileName = "" Then  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0)  
        Me._fileDeleted = False  
      Else  
        If System.IO.File.Exists(Me._fileName) Then  
          System.IO.File.Delete(Me._fileName)  
          Me._fileDeleted = True  
        Else  
          Me._fileDeleted = False  
        End If  
      End If  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property FileName() As String  
    Get  
      Return Me._fileName  
    End Get  
    Set(ByVal Value As String)  
      Me._fileName = Value  
    End Set  
  End Property  
  
  Public Overrides ReadOnly Property ExecutionValue() As Object  
    Get  
      Return Me._fileDeleted  
    End Get  
  End Property  
  
End Class  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂工作](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [撰寫自訂工作的程式碼](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [開發自訂工作的使用者介面](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  
