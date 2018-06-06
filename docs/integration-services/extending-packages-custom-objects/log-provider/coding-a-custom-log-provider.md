---
title: 撰寫自訂記錄提供者的程式碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-custom-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom log providers [Integration Services], coding
ms.assetid: 979a29ca-956e-4fdd-ab47-f06e84cead7a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a40454dd0095541bd0b714eaa93a1d296aacdb30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="coding-a-custom-log-provider"></a>撰寫自訂記錄提供者的程式碼
  建立繼承自 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基底類別的類別，並將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 屬性 (attribute) 套用到類別之後，必須覆寫基底類別的屬性 (properties) 與方法的實作，才可提供自訂功能。  
  
 如需自訂記錄提供者的實用範例，請參閱[開發自訂記錄提供者的使用者介面](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)。  
  
## <a name="configuring-the-log-provider"></a>設定記錄提供者  
  
### <a name="initializing-the-log-provider"></a>初始化記錄提供者  
 您覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.InitializeLogProvider%2A> 方法以快取連接集合與事件介面的參考。 您可以稍後在記錄提供者的其他方法中使用這些快取的參考。  
  
### <a name="using-the-configstring-property"></a>使用 ConfigString 屬性  
 在設計階段，記錄提供者會從 [組態] 資料行接收組態資訊。 這個組態資訊會對應至記錄提供者的 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 屬性。 依預設，這個資料行包含您可以從中擷取任何字串資訊的文字方塊。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所含的大部分記錄提供者，都會使用此屬性儲存提供者用以連接外部資料來源之連接管理員的名稱。 如果您的記錄提供者使用 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 屬性，請使用 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> 方法驗證這個屬性，並確定已正確設定屬性。  
  
### <a name="validating-the-log-provider"></a>驗證記錄提供者  
 您覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> 方法以確定已正確設定提供者，而且已準備執行。 一般而言，驗證的最低層級是確定 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 已正確地設定。 必須等到記錄提供者從 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> 方法傳回 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A>，執行才能繼續。  
  
 下列程式碼範例顯示 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> 的實作，以確定已指定連接管理員的名稱、連接管理員存在於封裝中，以及連接管理員傳回 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 屬性中的檔案名稱。  
  
```csharp  
public override DTSExecResult Validate(IDTSInfoEvents infoEvents)  
{  
    if (this.ConfigString.Length == 0 || connections.Contains(ConfigString) == false)  
    {  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
        return DTSExecResult.Failure;  
    }  
    else  
    {  
        string fileName = connections[ConfigString].AcquireConnection(null) as string;  
  
        if (fileName == null || fileName.Length == 0)  
        {  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
            return DTSExecResult.Failure;  
        }  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As IDTSInfoEvents) As DTSExecResult  
    If Me.ConfigString.Length = 0 Or connections.Contains(ConfigString) = False Then  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
        Return DTSExecResult.Failure  
    Else   
        Dim fileName As String =  connections(ConfigString).AcquireConnectionCType(as string, Nothing)  
  
        If fileName = Nothing Or fileName.Length = 0 Then  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
            Return DTSExecResult.Failure  
        End If  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
### <a name="persisting-the-log-provider"></a>保存記錄提供者  
 一般而言，您不必實作連接管理員的自訂持續性。 只有在物件的屬性使用複雜的資料類型時，才需要自訂持續性。 如需詳細資訊，請參閱[開發 Integration Services 的自訂物件](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)。  
  
## <a name="logging-with-the-log-provider"></a>使用記錄提供者進行記錄  
 有三個必須由所有記錄提供者覆寫的執行階段方法：<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>。  
  
> [!IMPORTANT]  
>  在單一封裝的驗證與執行期間，會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 方法一次以上。 請確定您的自訂程式碼不會造成記錄的下一個開啟和關閉覆寫先前的記錄項目。 如果您已選擇記錄測試封裝中的驗證事件，第一個會看到的記錄事件應該是 OnPreValidate；如果您看到的第一個記錄的事件是 PackageStart，表示最初的驗證事件已被覆寫。  
  
### <a name="opening-the-log"></a>開啟記錄  
 大部分的記錄提供者都會連接到外部資料來源，例如檔案或是資料庫，以儲存在封裝執行期間收集的事件資訊。 如同執行階段中的任何其他物件，連接到外部資料來源通常是透過使用連接管理員物件來完成。  
  
 在封裝執行開始時會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 方法。覆寫這個方法會建立連至外部資料來源的連接。  
  
 下列範例程式碼顯示的記錄提供者會開啟一個文字檔案，以供 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 期間寫入。 它會透過呼叫由 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 屬性指定的連接管理員之 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 方法，來開啟檔案。  
  
```csharp  
public override void OpenLog()  
{  
    if(!this.connections.Contains(this.ConfigString))  
        throw new Exception("The ConnectionManager " + this.ConfigString + " does not exist in the Connections collection.");  
  
    this.connectionManager = connections[ConfigString];  
    string filePath = this.connectionManager.AcquireConnection(null) as string;  
  
    if(filePath == null || filePath.Length == 0)  
        throw new Exception("The ConnectionManager " + this.ConfigString + " is not a valid FILE ConnectionManager");  
  
    //  Create a StreamWriter to append to.  
    sw = new StreamWriter(filePath,true);  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString());  
}  
```  
  
```vb  
Public Overrides  Sub OpenLog()  
    If Not Me.connections.Contains(Me.ConfigString) Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " does not exist in the Connections collection.")  
    End If  
  
    Me.connectionManager = connections(ConfigString)  
    Dim filePath As String =  Me.connectionManager.AcquireConnectionCType(as string, Nothing)  
  
    If filePath = Nothing Or filePath.Length = 0 Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " is not a valid FILE ConnectionManager")  
    End If  
  
    '  Create a StreamWriter to append to.  
    sw = New StreamWriter(filePath,True)  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString())  
End Sub  
```  
  
### <a name="writing-log-entries"></a>寫入記錄項目  
 每次封裝中的物件呼叫其中一個事件介面上的 Fire\<event> 方法來引發事件時，就會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 方法。 每個引發的事件都會帶有關於其內容且通常是說明訊息的資訊。 不過，並不是每次呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 方法都包括每個方法參數的資訊。 例如，有些其名稱字面意義明白的標準事件並未提供 MessageText，而且 DataCode 與 DataBytes 是為了提供選擇性的補充資訊。  
  
 下列程式碼範例會實作 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 方法，並將事件寫入上一節所開啟的資料流。  
  
```csharp  
public override void Log(string logEntryName, string computerName, string operatorName, string sourceName, string sourceID, string executionID, string messageText, DateTime startTime, DateTime endTime, int dataCode, byte[] dataBytes)  
{  
    sw.Write(logEntryName + ",");  
    sw.Write(computerName + ",");  
    sw.Write(operatorName + ",");  
    sw.Write(sourceName + ",");  
    sw.Write(sourceID + ",");  
    sw.Write(messageText + ",");  
    sw.Write(dataBytes + ",");  
    sw.WriteLine("");  
}  
```  
  
```vb  
Public Overrides  Sub Log(ByVal logEnTryName As String, ByVal computerName As String, ByVal operatorName As String, ByVal sourceName As String, ByVal sourceID As String, ByVal executionID As String, ByVal messageText As String, ByVal startTime As DateTime, ByVal endTime As DateTime, ByVal dataCode As Integer, ByVal dataBytes() As Byte)  
    sw.Write(logEnTryName + ",")  
    sw.Write(computerName + ",")  
    sw.Write(operatorName + ",")  
    sw.Write(sourceName + ",")  
    sw.Write(sourceID + ",")  
    sw.Write(messageText + ",")  
    sw.Write(dataBytes + ",")  
    sw.WriteLine("")  
End Sub  
```  
  
### <a name="closing-the-log"></a>關閉記錄  
 在封裝中的所有物件都完成執行之後，或是當封裝因為錯誤而停止時，會在封裝執行結束時呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 方法。  
  
 下列程式碼範例示範 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 方法的實作，這個方法會關閉在 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 方法期間開啟的檔案資料流。  
  
```csharp  
public override void CloseLog()  
{  
    if (sw != null)  
    {  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString());  
        sw.Close();  
    }  
}  
```  
  
```vb  
Public Overrides  Sub CloseLog()  
    If Not sw Is Nothing Then  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString())  
        sw.Close()  
    End If  
End Sub  
```  
 
## <a name="see-also"></a>另請參閱  
 [建立自訂記錄提供者](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [開發自訂記錄提供者的使用者介面](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
  
  
