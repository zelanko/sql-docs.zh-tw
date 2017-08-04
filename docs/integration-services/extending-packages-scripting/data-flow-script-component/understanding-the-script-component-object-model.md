---
title: "了解指令碼元件物件模型 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
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
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 09de00344fe94087b6287b07c4b1ffe933d27b7c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="understanding-the-script-component-object-model"></a>了解指令碼元件物件模型
  中所述[編碼和偵錯指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)，指令碼元件專案包含三個專案項目：  
  
1.  **ScriptMain**項目，其中包含**ScriptMain**類別，您可以在其中撰寫程式碼。 **ScriptMain**類別繼承自**UserComponent**類別。  
  
2.  **ComponentWrapper**項目，其中包含**UserComponent**類別的執行個體<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>包含方法和屬性，將會用來處理資料，以及與封裝互動。 **ComponentWrapper**項目也包含**連線**和**變數**集合類別。  
  
3.  **BufferWrapper**項目，包含類別，繼承自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>每個輸入和輸出，和具類型的屬性，每個資料行。  
  
 當您撰寫程式碼**ScriptMain**項目，您將使用物件、 方法和本主題中所討論的屬性。 並非這裡列出的所有方法都會讓每一個元件使用，但是在使用這些方法時，則會以顯示的順序來使用。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 基底類別不包含本主題討論之方法的任何實作程式碼。 因此，將基底類別實作的呼叫加入到您自己的方法實作中是不必要的，但是這樣做也無害。  
  
 如需如何在特定類型的指令碼元件中使用的方法和屬性，這些類別的資訊，請參閱下節[Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。 範例主題也包含完整的程式碼範例。  
  
## <a name="acquireconnections-method"></a>AcquireConnections 方法  
 來源和目的地通常必須連接到外部資料來源。 覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法，從適當的連接管理員擷取連接或連接資訊。  
  
 下列範例會傳回**System.Data.SqlClient.SqlConnection**從 ADO.NET 連接管理員。  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 下列範例會傳回完整路徑和檔案名稱從一般檔案連接管理員，並使用，以開啟檔案**System.IO.StreamReader**。  
  
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
 每個輸入，您已設定， **BufferWrapper**專案項目包含的類別，衍生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>且具有相同名稱做為輸入。 每一個輸入緩衝區類別都包含下列屬性、函數和方法：  
  
-   每一個選定輸入資料行的具名、具類型存取子屬性。 這些屬性是唯讀或讀取/寫入，取決於**使用類型**資料行上指定**的輸入資料行**頁面**指令碼轉換編輯器**。  
  
-   A **\<資料行 > _IsNull**屬性，每一個選定輸入資料行。 這個屬性也是唯讀或讀取/寫入，取決於**使用類型**指定資料行。  
  
-   A **DirectRowTo\<outputbuffer >**設定輸出的每個方法。 在相同的數個輸出的其中一個資料列篩選時，您會使用這些方法**ExclusionGroup**。  
  
-   A **NextRow**函式可取得下一個輸入資料列，以及**EndOfRowset**函式來判斷是否已經處理最後一個資料緩衝區。 您通常不需要這些函式時使用的輸入處理方法中實作**UserComponent**基底類別。 下一節提供有關的詳細資訊**UserComponent**基底類別。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 專案項目提供的內容  
 ComponentWrapper 專案項目包含類別，名為**UserComponent**衍生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>。 **ScriptMain**您用來撰寫自訂程式碼的類別又衍生自**UserComponent**。 **UserComponent**類別包含下列方法：  
  
-   覆寫的實作**ProcessInput**方法。 這是資料流程引擎會呼叫接下來在之後的執行階段方法**PreExecute**方法，而且它會呼叫多次。 **ProcessInput**處理交給 **\<inputbuffer > _ProcessInput**方法。 然後在**ProcessInput**方法會檢查輸入緩衝區的結尾，而如果已到達緩衝區的結尾，會呼叫可覆寫**FinishOutputs**方法和私用**MarkOutputsAsFinished**方法。 **MarkOutputsAsFinished**方法接著呼叫**SetEndOfRowset**上最後一個輸出緩衝區。  
  
-   可覆寫的實作 **\<inputbuffer > _ProcessInput**方法。 這個預設實作只需執行迴圈，每個輸入資料列和呼叫 **\<inputbuffer > _ProcessInputRow**。  
  
-   可覆寫的實作 **\<inputbuffer > _ProcessInputRow**方法。 預設的實作是空的。 這是您通常會覆寫，以撰寫自訂資料處理程式碼的方法。  
  
#### <a name="what-your-custom-code-should-do"></a>自訂程式碼應該做的事  
 您可以使用下列方法來處理中的輸入**ScriptMain**類別：  
  
-   覆寫 **\<inputbuffer > _ProcessInputRow**通過處理每個輸入資料列中的資料。  
  
-   覆寫 **\<inputbuffer > _ProcessInput**只有當您需要執行額外的項目迴圈的輸入資料列時。 (例如，您必須測試**EndOfRowset**採取其他動作在所有已處理的資料列。)呼叫 **\<inputbuffer > _ProcessInputRow**來執行的資料列處理。  
  
-   覆寫**FinishOutputs**如果您必須關閉之前，請執行某個動作，輸出。  
  
 **ProcessInput**方法可確保在適當的時間會呼叫這些方法。  
  
### <a name="processing-outputs"></a>處理輸出  
 設定為來源或轉換的指令碼元件有一個或多個輸出。  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 專案項目提供的內容  
 如果是您已設定的每一個輸出，BufferWrapper 專案項目都會包含一個衍生自 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 的類別，而且名稱與輸出相同。 每一個輸入緩衝區類別都包含下列屬性和方法：  
  
-   每一個輸出資料行的具名、具類型、唯寫的存取子屬性。  
  
-   唯寫**\<資料行 > _IsNull**屬性可用來將資料行值設定為每個選取的輸出資料行**null**。  
  
-   **AddRow**方法，將空的新資料列加入到輸出緩衝區。  
  
-   A **SetEndOfRowset**方法讓資料流程引擎知道有無緩衝區的資料。 另外還有**EndOfRowset**函式，以判斷目前的緩衝區是否為最後一個資料緩衝區。 您通常不需要這些函式時使用的輸入處理方法中實作**UserComponent**基底類別。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 專案項目提供的內容  
 ComponentWrapper 專案項目包含類別，名為**UserComponent**衍生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>。 **ScriptMain**您用來撰寫自訂程式碼的類別又衍生自**UserComponent**。 **UserComponent**類別包含下列方法：  
  
-   覆寫的實作**PrimeOutput**方法。 資料流程引擎會呼叫這個方法之前**ProcessInput**在執行階段，而且只會呼叫一次。 **PrimeOutput**處理交給**CreateNewOutputRows**方法。 然後，如果元件是來源 （也就是該元件具有沒有輸入）， **PrimeOutput**呼叫可覆寫**FinishOutputs**方法和私用**MarkOutputsAsFinished**方法。 **MarkOutputsAsFinished**方法呼叫**SetEndOfRowset**上最後一個輸出緩衝區。  
  
-   可覆寫的實作**CreateNewOutputRows**方法。 預設的實作是空的。 這是您通常會覆寫，以撰寫自訂資料處理程式碼的方法。  
  
#### <a name="what-your-custom-code-should-do"></a>自訂程式碼應該做的事  
 您可以使用下列方法來處理輸出**ScriptMain**類別：  
  
-   覆寫**CreateNewOutputRows**只有當您可以新增和填入輸出資料列之前處理輸入資料列。 例如，您可以使用**CreateNewOutputRows**在來源中，但具有非同步輸出的轉換，您應該呼叫**AddRow**的輸入資料處理期間或之後。  
  
-   覆寫**FinishOutputs**如果您必須關閉之前，請執行某個動作，輸出。  
  
 **PrimeOutput**方法可確保在適當的時間會呼叫這些方法。  
  
## <a name="postexecute-method"></a>PostExecute 方法  
 每當您的處理必須只能在處理資料列之後執行一次時，請覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 例如，在來源中，您可能要關閉**System.Data.SqlClient.SqlDataReader** ，已用來將資料載入資料流程。  
  
> [!IMPORTANT]  
>  集合**[readwritevariables]**僅適用於**PostExecute**方法。 因此您無法在處理每一列資料時，直接增量封裝變數值。 相反地，本機變數的值遞增，並設定封裝變數的值為本機變數中的值**PostExecute**經過處理之後的所有資料的方法。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [在指令碼元件編輯器中設定指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [編碼和偵錯指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
