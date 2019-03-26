---
title: 撰寫自訂連線管理員的程式碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom connection managers [Integration Services], coding
ms.assetid: b12b6778-1f01-4a7d-984d-73f2f7630aa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 48d18edc37d5073ab4346ec58cbb6a341d8870fe
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282412"
---
# <a name="coding-a-custom-connection-manager"></a>撰寫自訂連接管理員的程式碼
  建立繼承自 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 基底類別的類別，並將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 屬性 (attribute) 套用到類別之後，必須覆寫基底類別的屬性 (properties) 與方法的實作，才可提供自訂功能。  
  
 如需連線管理員範例，請參閱[開發自訂連線管理員的使用者介面](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)。 在本主題中所顯示的程式碼範例是取自＜SQL Server 自訂連接管理員＞範例。  
  
> [!NOTE]  
>  已經建置到 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中的大多數工作、來源和目的地只能搭配特定類型的內建連接管理員一起使用。 因此，不能使用內建工作和元件來測試這些範例。  
  
## <a name="configuring-the-connection-manager"></a>設定連接管理員  
  
### <a name="setting-the-connectionstring-property"></a>設定 ConnectionString 屬性  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> 屬性是重要的屬性，而且是自訂連接管理員特有的唯一屬性。 連接管理員使用此屬性值，以連接至外部資料來源。 如果您要結合數個其他的屬性 (例如伺服器名稱與資料庫名稱) 來建立連接字串，可以使用 Helper 函數組合字串，方法是以使用者提供的新值取代連接字串範本中的某些值。 下列程式碼範例顯示 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> 屬性的實作，此屬性依賴 Helper 函數組合字串。  
  
```vb  
' Default values.  
Private _serverName As String = "(local)"  
Private _databaseName As String = "AdventureWorks"  
Private _connectionString As String = String.Empty  
  
Private Const CONNECTIONSTRING_TEMPLATE As String = _  
  "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI"  
  
Public Property ServerName() As String  
  Get  
    Return _serverName  
  End Get  
  Set(ByVal value As String)  
    _serverName = value  
  End Set  
End Property  
  
Public Property DatabaseName() As String  
  Get  
    Return _databaseName  
  End Get  
  Set(ByVal value As String)  
    _databaseName = value  
  End Set  
End Property  
  
Public Overrides Property ConnectionString() As String  
  Get  
    UpdateConnectionString()  
    Return _connectionString  
  End Get  
  Set(ByVal value As String)  
    _connectionString = value  
  End Set  
End Property  
  
Private Sub UpdateConnectionString()  
  
  Dim temporaryString As String = CONNECTIONSTRING_TEMPLATE  
  
  If Not String.IsNullOrEmpty(_serverName) Then  
    temporaryString = temporaryString.Replace("<servername>", _serverName)  
  End If  
  If Not String.IsNullOrEmpty(_databaseName) Then  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName)  
  End If  
  
  _connectionString = temporaryString  
  
End Sub  
```  
  
```csharp  
// Default values.  
private string _serverName = "(local)";  
private string _databaseName = "AdventureWorks";  
private string _connectionString = String.Empty;  
  
private const string CONNECTIONSTRING_TEMPLATE = "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI";  
  
public string ServerName  
{  
  get  
  {  
    return _serverName;  
  }  
  set  
  {  
    _serverName = value;  
  }  
}  
  
public string DatabaseName  
{  
  get  
  {  
    return _databaseName;  
  }  
  set  
  {  
    _databaseName = value;  
  }  
}  
  
public override string ConnectionString  
{  
  get  
  {  
    UpdateConnectionString();  
    return _connectionString;  
  }  
  set  
  {  
    _connectionString = value;  
  }  
}  
  
private void UpdateConnectionString()  
{  
  
  string temporaryString = CONNECTIONSTRING_TEMPLATE;  
  
  if (!String.IsNullOrEmpty(_serverName))  
  {  
    temporaryString = temporaryString.Replace("<servername>", _serverName);  
  }  
  
  if (!String.IsNullOrEmpty(_databaseName))  
  {  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName);  
  }  
  
  _connectionString = temporaryString;  
  
}  
```  
  
### <a name="validating-the-connection-manager"></a>驗證連接管理員  
 您覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A> 方法以確定已正確設定連接管理員。 至少，您應該驗證連接字串的格式，並確定已為所有的引數提供值。 必須等到連接管理員從 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> 方法傳回 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A>，執行才能繼續。  
  
 下列程式碼範例顯示 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A> 的實作，以確定使用者已指定連接的伺服器名稱。  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  If String.IsNullOrEmpty(_serverName) Then  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0)  
    Return DTSExecResult.Failure  
  Else  
    Return DTSExecResult.Success  
  End If  
  
End Function  
```  
  
```csharp  
public override Microsoft.SqlServer.Dts.Runtime.DTSExecResult Validate(Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  if (String.IsNullOrEmpty(_serverName))  
  {  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0);  
    return DTSExecResult.Failure;  
  }  
  else  
  {  
    return DTSExecResult.Success;  
  }  
  
}  
```  
  
### <a name="persisting-the-connection-manager"></a>保存連接管理員  
 通常，您不必實作連接管理員的自訂持續性。 只有在物件的屬性使用複雜的資料類型時，才需要自訂持續性。 如需詳細資訊，請參閱[開發 Integration Services 的自訂物件](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)。  
  
## <a name="working-with-the-external-data-source"></a>使用外部資料來源  
 支援連接至外部資料來源的方法是自訂連接管理員最重要的方法。 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> 方法是在設計階段與執行階段的不同時間呼叫。  
  
### <a name="acquiring-the-connection"></a>取得連接  
 您需要決定哪些類型的物件適用於 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 方法，從自訂連接管理員傳回。 例如，檔案連接管理員只會傳回包含路徑與檔案名稱的字串，而 ADO.NET 連接管理員則會傳回已經開啟的 Managed 連接物件。 OLE DB 連接管理員會傳回原生 OLE DB 連接物件，而此物件無法從 Managed 程式碼中加以使用。 本主題中的程式碼片段是取自 SQL Server 連線管理員，它會傳回已開啟的 **SqlConnection** 物件。  
  
 連接管理員的使用者需要事先知道需要哪些類型的物件，這樣他們才能將傳回的物件轉換為適當的類型，並存取其方法與屬性。  
  
```vb  
Public Overrides Function AcquireConnection(ByVal txn As Object) As Object  
  
  Dim sqlConnection As New SqlConnection  
  
  UpdateConnectionString()  
  
  With sqlConnection  
    .ConnectionString = _connectionString  
    .Open()  
  End With  
  
  Return sqlConnection  
  
End Function  
```  
  
```csharp  
public override object AcquireConnection(object txn)  
{  
  
  SqlConnection sqlConnection = new SqlConnection();  
  
  UpdateConnectionString();  
  
  {  
    sqlConnection.ConnectionString = _connectionString;  
    sqlConnection.Open();  
  }  
  
  return sqlConnection;  
  
}  
```  
  
### <a name="releasing-the-connection"></a>解除連接  
 您在 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> 方法中所採取的動作，取決於從 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 方法傳回的物件類型。 如果有開啟的連接物件，您應該關閉它並釋放其所使用的任何資源。 如果 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 只傳回字串值，則不需要採取任何動作。  
  
```vb  
Public Overrides Sub ReleaseConnection(ByVal connection As Object)  
  
  Dim sqlConnection As SqlConnection  
  
  sqlConnection = DirectCast(connection, SqlConnection)  
  
  If sqlConnection.State <> ConnectionState.Closed Then  
    sqlConnection.Close()  
  End If  
  
End Sub  
```  
  
```csharp  
public override void ReleaseConnection(object connection)  
{  
  SqlConnection sqlConnection;  
  sqlConnection = (SqlConnection)connection;  
  if (sqlConnection.State != ConnectionState.Closed)  
    sqlConnection.Close();  
}  
```  
 
## <a name="see-also"></a>另請參閱  
 [建立自訂連線管理員](../../../integration-services/extending-packages-custom-objects/connection-manager/creating-a-custom-connection-manager.md)   
 [開發自訂連線管理員的使用者介面](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  
