---
title: 從 SQL Server 的執行個體中斷連接 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8a99d5b82f8901d66c1ad25de5de03694e5b3e1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43109006"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>從 SQL Server 的執行個體中斷連接
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  以手動方式關閉和中斷連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Management Objects (SMO) 物件就不需要。 連接會視需要開啟和關閉。  
  
## <a name="connection-pooling"></a>連接共用  
 當[Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect)呼叫方法，不會自動釋放連接。 [中斷連線](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)必須明確地呼叫方法，若要將連接釋放到連接集區。 此外，您也可以要求非共用連接。 您可以設定[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)屬性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>參照屬性[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)物件。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>從 RMO 的 SQL Server 執行個體中斷連接  
 在使用 RMO 進行程式開發時關閉伺服器連接，與使用 SMO 時稍有不同。  
  
 因為 RMO 物件的伺服器連接由維護[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)物件，這個物件也會從執行個體中斷連線時[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]您使用 RMO 進行程式設計時。 使用關閉的連線[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)物件，請呼叫[中斷連線](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)RMO 物件的方法。 在關閉連接之後，就無法使用 RMO 物件。  
  
## <a name="example"></a>範例  
如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱 <<c0> [ 建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。</c0>  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>在 Visual Basic 中關閉和中斷 SMO 物件的連接  
 此程式碼範例示範如何藉由設定要求非共用的連接[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)屬性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>物件屬性。  
  
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
 此程式碼範例示範如何藉由設定要求非共用的連接[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)屬性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>物件屬性。  
  
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
  
  
