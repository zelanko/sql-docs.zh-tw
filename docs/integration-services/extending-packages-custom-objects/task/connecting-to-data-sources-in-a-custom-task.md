---
title: 在自訂工作中連線至資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ConnectionManager objects
- connection managers [Integration Services], external data sources
- data sources [Integration Services], external
- custom tasks [Integration Services], external data sources
- external data sources [Integration Services]
- connections [Integration Services], external data sources
- SSIS custom tasks, external data sources
ms.assetid: 9f0b3a43-3eaa-4b3c-bb08-29b630c11306
author: janinezhang
ms.author: janinez
ms.openlocfilehash: eca56f08abae691cb106e02e0aa3215b78616be0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062855"
---
# <a name="connecting-to-data-sources-in-a-custom-task"></a>連接至自訂工作中的資料來源

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  工作會利用連接管理員連接至外部資料來源，以擷取或儲存資料。 在設計階段，連接管理員代表邏輯連接，並描述伺服器名稱與任何驗證屬性等主要資訊。 在執行階段，工作會呼叫連接管理員的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法，以建立連至資料來源的實體連接。  
  
 因為封裝可以包含許多工作，每個工作都可能有連至不同資料來源的連接，所以封裝會追蹤在 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合中的所有連接管理員。 工作會使用其封裝中的集合，以尋找它們在驗證和執行期間將使用的連接管理員。 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合是 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 方法的第一個參數。  
  
 您可以使用圖形化使用者介面中的對話方塊或是下拉式清單，對使用者顯示集合的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件，以防止工作使用錯誤的連接管理員。 這個方法可讓使用者只能從封裝內適當類型的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件中進行選取。  
  
 工作會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法以建立連至資料來源的實體連接。 方法會傳回基礎連接物件，以供工作使用。 因為連接管理員會將基礎連接物件的實作詳細資料與工作隔離開來，所以工作只需要呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法建立連接，而不必顧慮連接的其他層面。  
  
## <a name="example"></a>範例  
 下列範例程式碼示範 Validate 與 Execute 方法中的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 名稱之驗證，並顯示如何使用 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法來建立 Execute 方法中的實體連接。  
  
```csharp  
private string connectionManagerName = "";  
  
public string ConnectionManagerName  
{  
  get { return this.connectionManagerName; }  
  set { this.connectionManagerName = value; }  
}  
  
public override DTSExecResult Validate(  
  Connections connections, VariableDispenser variableDispenser,  
  IDTSComponentEvents componentEvents, IDTSLogging log)  
{  
  // If the connection manager exists, validation is successful;  
  // otherwise, fail validation.  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception e)  
  {  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
  
public override DTSExecResult Execute(Connections connections,   
  VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,   
  IDTSLogging log, object transaction)  
{  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    object connection = cm.AcquireConnection(transaction);  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception exception)  
  {  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
```  
  
```vb  
Private _connectionManagerName As String = ""  
  
Public Property ConnectionManagerName() As String  
  Get  
    Return Me._connectionManagerName  
  End Get  
  Set(ByVal Value As String)  
    Me._connectionManagerName = value  
  End Set  
End Property  
  
Public Overrides Function Validate( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  ' If the connection manager exists, validation is successful;  
  ' otherwise fail validation.  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Return DTSExecResult.Success  
  Catch e As System.Exception  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
  
Public Overrides Function Execute( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging, ByVal transaction As Object) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Dim connection As Object = cm.AcquireConnection(transaction)  
    Return DTSExecResult.Success  
  Catch exception As System.Exception  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
```  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連線](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [建立連線管理員](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
