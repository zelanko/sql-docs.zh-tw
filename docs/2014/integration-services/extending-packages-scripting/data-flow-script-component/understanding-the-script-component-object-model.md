---
title: 了解指令碼元件物件模型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 73016278ce8455a57af78229703e2330bbbd0edf
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370520"
---
# <a name="understanding-the-script-component-object-model"></a>了解指令碼元件物件模型
  在 [程式碼撰寫和偵錯指令碼元件] 中所述 (.../ extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md，指令碼元件專案包含三個專案項目：  
  
1.  `ScriptMain` 項目，其中包含您用來撰寫程式碼的 `ScriptMain` 類別。 `ScriptMain` 類別繼承自 `UserComponent` 類別。  
  
2.  包含 `ComponentWrapper` 類別的 `UserComponent` 項目，該類別是 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 的執行個體 (其中包含您將用來處理資料以及與封裝互動的方法和屬性)。 `ComponentWrapper` 項目也包含 `Connections` 和 `Variables` 集合類別。  
  
3.  包含類別的 `BufferWrapper` 項目，該類別繼承自每一個輸入和輸出的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 及每一個資料行的具類型屬性。  
  
 當您在 `ScriptMain` 項目中撰寫程式碼時，您將會使用本主題討論的物件、方法和屬性。 並非這裡列出的所有方法都會讓每一個元件使用，但是在使用這些方法時，則會以顯示的順序來使用。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 基底類別不包含本主題討論之方法的任何實作程式碼。 因此，將基底類別實作的呼叫加入到您自己的方法實作中是不必要的，但是這樣做也無害。  
  
 如需如何在特定的指令碼元件類型中使用這些類別的方法和屬性的資訊，請參閱[其他指令碼元件範例](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。 範例主題也包含完整的程式碼範例。  
  
## <a name="acquireconnections-method"></a>AcquireConnections 方法  
 來源和目的地通常必須連接到外部資料來源。 覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法，從適當的連接管理員擷取連接或連接資訊。  
  
 下列範例會從 ADO.NET 連接管理員傳回 `System.Data.SqlClient.SqlConnection`。  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 下列範例會從一般檔案連接管理員傳回完整的路徑和檔案名稱，然後使用 `System.IO.StreamReader` 開啟檔案。  
  
```vb  
Private textReader As StreamReader  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    Dim connMgr As IDTSConnectionManager100 = _  
        Me.Connections.MyFlatFileSrcConnectionManager  
    Dim exportedAddressFile As String = _  
        CType(connMgr.AcquireConnection(Nothing), String)  
    textReader = New StreamReader(exportedAddressFile)  
  
End Sub  
```  
  
## <a name="preexecute-method"></a>PreExecute 方法  
 每當您的處理必須只能在您開始處理資料列以前執行一次時，請覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PreExecute%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 例如在目的地中，您可能會想要設定參數化命令，目的地將會使用該命令將每個資料列插入資料來源中。  
  
```vb  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
...  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
```  
  
```csharp  
SqlConnection sqlConn;   
SqlCommand sqlCmd;   
SqlParameter sqlParam;   
  
public override void PreExecute()   
{   
  
    sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " + "VALUES(@addressid, @city)", sqlConn);   
    sqlParam = new SqlParameter("@addressid", SqlDbType.Int);   
    sqlCmd.Parameters.Add(sqlParam);   
    sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);   
    sqlCmd.Parameters.Add(sqlParam);   
  
}  
```  
  
## <a name="processing-inputs-and-outputs"></a>處理輸入和輸出  
  
### <a name="processing-inputs"></a>處理輸入  
 設定為轉換或目的地的指令碼元件有一個輸入。  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 專案項目提供的內容  
 如果是您已設定的每一個輸入，`BufferWrapper` 專案項目都會包含一個衍生自 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 的類別，而且名稱與輸入相同。 每一個輸入緩衝區類別都包含下列屬性、函數和方法：  
  
-   每一個選定輸入資料行的具名、具類型存取子屬性。 這些屬性是唯讀或可讀寫，這取決於在 [指令碼轉換編輯器] 的 [輸入資料行] 頁面上針對資料行所指定的 [使用類型]。  
  
-   每一個選定輸入資料行的 **\<資料行>_IsNull** 屬性。 這個屬性也是唯讀或可讀寫，這取決於針對資料行指定的 [使用類型] 而定。  
  
-   每個已設定輸出的 **DirectRowTo\<輸出緩衝區>** 方法。 當您在相同的 `ExclusionGroup` 中將資料列篩選成數個輸出的其中一個時，您將會使用這些方法。  
  
-   取得下一個輸入資料列的 `NextRow` 函數，以及判斷上一個資料緩衝區是否已經處理的 `EndOfRowset` 函數。 當您使用 `UserComponent` 基底類別內所實作的輸入處理方法時，通常不需要這些函數。 下一節會提供有關 `UserComponent` 基底類別的詳細資訊。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 專案項目提供的內容  
 ComponentWrapper 專案項目包含了衍生自 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 的 `UserComponent` 類別。 接著您撰寫自訂程式碼所使用的 `ScriptMain` 類別就會衍生自 `UserComponent`。 `UserComponent` 類別包含以下的方法：  
  
-   已覆寫的 `ProcessInput` 方法實作。 這是資料流程引擎在執行階段的 `PreExecute` 方法之後所呼叫的方法，而且它可呼叫多次。 `ProcessInput` 處理交給 **\<inputbuffer > n p u t**方法。 然後 `ProcessInput` 方法會檢查輸入緩衝區的結尾，如果到達了緩衝區結尾，會呼叫可覆寫的 `FinishOutputs` 方法和私用 `MarkOutputsAsFinished` 方法。 然後 `MarkOutputsAsFinished` 方法會在最後一個輸出緩衝區上呼叫 `SetEndOfRowset`。  
  
-   可覆寫的 **\<輸入緩衝區>_ProcessInput** 方法實作。 這個預設實作只會在每一個輸入資料列中執行迴圈，並呼叫 **\<輸入緩衝區>_ProcessInputRow**。  
  
-   可覆寫的 **\<輸入緩衝區>_ProcessInputRow** 方法實作。 預設的實作是空的。 這是您通常會覆寫，以撰寫自訂資料處理程式碼的方法。  
  
#### <a name="what-your-custom-code-should-do"></a>自訂程式碼應該做的事  
 您可以使用下列方法，在 `ScriptMain` 類別中處理輸入：  
  
-   覆寫 **\<輸入緩衝區>_ProcessInputRow**，以處理每一個輸入資料列中通過的資料。  
  
-   只有當您在輸入資料列中執行迴圈時必須做其他額外的動作的時候，才會覆寫 **\<輸入緩衝區>_ProcessInput**。 (例如，您必須測試 `EndOfRowset`，在處理完所有資料列以後採取某個其他動作)。呼叫 **\<輸入緩衝區>_ProcessInputRow** 來執行資料列處理。  
  
-   如果您必須在關閉輸出以前先對輸出做某些事，請覆寫 `FinishOutputs`。  
  
 `ProcessInput` 方法可確保這些方法會在適當的時間呼叫。  
  
### <a name="processing-outputs"></a>處理輸出  
 設定為來源或轉換的指令碼元件有一個或多個輸出。  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 專案項目提供的內容  
 如果是您已設定的每一個輸出，BufferWrapper 專案項目都會包含一個衍生自 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 的類別，而且名稱與輸出相同。 每一個輸入緩衝區類別都包含下列屬性和方法：  
  
-   每一個輸出資料行的具名、具類型、唯寫的存取子屬性。  
  
-   唯**\<資料行 > _IsNull**可用來將資料行值設定為每一個選定的輸出資料行的屬性`null`。  
  
-   要將空白的新資料列加入到輸出緩衝區的 `AddRow` 方法。  
  
-   可讓資料流程引擎知道不會預期其他資料緩衝區的 `SetEndOfRowset` 方法。 也有一個 `EndOfRowset` 函數可判斷目前的緩衝區是否為最後一個資料緩衝區。 當您使用 `UserComponent` 基底類別內所實作的輸入處理方法時，通常不需要這些函數。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 專案項目提供的內容  
 ComponentWrapper 專案項目包含了衍生自 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 的 `UserComponent` 類別。 接著您撰寫自訂程式碼所使用的 `ScriptMain` 類別就會衍生自 `UserComponent`。 `UserComponent` 類別包含以下的方法：  
  
-   已覆寫的 `PrimeOutput` 方法實作。 資料流程引擎會在執行階段的 `ProcessInput` 之前呼叫這個方法，而且只會呼叫一次。 `PrimeOutput` 會將處理交給 `CreateNewOutputRows` 方法。 然後，如果此元件是來源 (也就是此元件沒有輸入)，`PrimeOutput` 會呼叫可覆寫的 `FinishOutputs` 方法和私用 `MarkOutputsAsFinished` 方法。 `MarkOutputsAsFinished` 方法會在最後一個輸出緩衝區上呼叫 `SetEndOfRowset`。  
  
-   可覆寫的 `CreateNewOutputRows` 方法實作。 預設的實作是空的。 這是您通常會覆寫，以撰寫自訂資料處理程式碼的方法。  
  
#### <a name="what-your-custom-code-should-do"></a>自訂程式碼應該做的事  
 您可以使用下列方法，在 `ScriptMain` 類別中處理輸出：  
  
-   只有當您在處理輸入資料列以前可以加入及擴展輸出資料列時，才會覆寫 `CreateNewOutputRows`。 例如，您可以在來源中使用 `CreateNewOutputRows`，但如果是具有非同步輸出的轉換，您應該在處理輸入資料的期間或之後呼叫 `AddRow`。  
  
-   如果您必須在關閉輸出以前先對輸出做某些事，請覆寫 `FinishOutputs`。  
  
 `PrimeOutput` 方法可確保這些方法會在適當的時間呼叫。  
  
## <a name="postexecute-method"></a>PostExecute 方法  
 每當您的處理必須只能在處理資料列之後執行一次時，請覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 例如在來源中，您可能會想要關閉已經用來將資料載入資料流程中的 `System.Data.SqlClient.SqlDataReader`。  
  
> [!IMPORTANT]  
>  只有在 `ReadWriteVariables` 方法中才可使用 `PostExecute` 集合。 因此您無法在處理每一列資料時，直接增量封裝變數值。 請改為遞增區域變數值，並在處理所有的資料之後，將封裝變數值設定為 `PostExecute` 方法中的區域變數值。  
  
## <a name="releaseconnections-method"></a>ReleaseConnections 方法  
 來源和目的地通常必須連接到外部資料來源。 覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法，以關閉及釋放您之前在 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 方法中所開啟的連接。  
  
```vb  
    Dim connMgr As IDTSConnectionManager100  
...  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
```  
  
```csharp  
IDTSConnectionManager100 connMgr;  
  
public override void ReleaseConnections()  
{  
  
    connMgr.ReleaseConnection(sqlConn);  
  
}  
```  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [在指令碼元件編輯器中設定指令碼元件](configuring-the-script-component-in-the-script-component-editor.md)   
 [程式碼撰寫和偵錯指令碼元件] (../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md  
  
  
