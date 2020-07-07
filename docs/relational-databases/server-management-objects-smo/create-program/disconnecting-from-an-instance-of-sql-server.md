---
title: 中斷與 SQL Server 實例的連線 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b7d361ab7648c4cc196aaf9ee2d7be88d980e4d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006374"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>從 SQL Server 的執行個體中斷連接
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  您並不需要以手動方式關閉和中斷 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 物件的連接。 連接會視需要開啟和關閉。  
  
## <a name="connection-pooling"></a>連接共用  
 呼叫[Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect)方法時，不會自動釋放連接。 必須明確呼叫[Disconnect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)方法，才能釋放與連接集區的連接。 此外，您也可以要求非共用連接。 若要這麼做，您[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)可以設定 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 參考[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)物件之屬性的 NonPooledConnection 屬性。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>從 RMO 的 SQL Server 執行個體中斷連接  
 在使用 RMO 進行程式開發時關閉伺服器連接，與使用 SMO 時稍有不同。  
  
 由於 RMO 物件的伺服器連接是由[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)物件維護，因此 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 當您使用 RMO 進行程式設計時，也會使用這個物件來與的實例中斷連接。 若要使用[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)物件關閉連接，請呼叫 RMO 物件的[Disconnect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)方法。 在關閉連接之後，就無法使用 RMO 物件。  
  
## <a name="example"></a>範例  
如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 Visual C&#35; SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>在 Visual Basic 中關閉和中斷 SMO 物件的連接  
 這個程式碼範例示範如何藉由設定物件屬性的[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)屬性，來要求非集區連接 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 。  
  
```VBNET
Dim srv As Server
srv = New Server
'Disable automatic disconnection.
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect
'Connect to the local, default instance of SQL Server.
srv.ConnectionContext.Connect()
'The actual connection is made when a property is retrieved.
Console.WriteLine(srv.Information.Version)
'Disconnect explicitly.
srv.ConnectionContext.Disconnect()
```
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>在 Visual C# 中關閉和中斷 SMO 物件的連接  
 這個程式碼範例示範如何藉由設定物件屬性的[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)屬性，來要求非集區連接 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 。  
  
```csharp  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
