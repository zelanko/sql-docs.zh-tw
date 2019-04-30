---
title: 從 SQL Server 的執行個體中斷連接 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7783fa93912c305403cc34ad6e52668123d164ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192069"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>從 SQL Server 的執行個體中斷連接
  您並不需要以手動方式關閉和中斷 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 物件的連接。 連接會視需要開啟和關閉。  
  
## <a name="connection-pooling"></a>連接共用  
 呼叫 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> 方法時，並不會自動釋放連接。 您必須明確地呼叫 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 方法，才能釋放對連接集區的連接。 此外，您也可以要求非共用連接。 執行此作業的方法是設定 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 屬性的 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 屬性，該屬性會參考 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>從 RMO 的 SQL Server 執行個體中斷連接  
 在使用 RMO 進行程式開發時關閉伺服器連接，與使用 SMO 時稍有不同。  
  
 因為 RMO 物件的伺服器連接由維護<xref:Microsoft.SqlServer.Management.Common.ServerConnection>物件，這個物件也會從執行個體中斷連線時[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]您使用 RMO 進行程式設計時。 若要使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件關閉連接，請呼叫 RMO 物件的 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 方法。 在關閉連接之後，就無法使用 RMO 物件。  
  
## <a name="example"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>在 Visual Basic 中關閉和中斷 SMO 物件的連接  
 此程式碼範例示範如何設定 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 物件屬性的 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 屬性以要求非共用連接。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>在 Visual C# 中關閉和中斷 SMO 物件的連接  
 此程式碼範例示範如何設定 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 物件屬性的 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 屬性以要求非共用連接。  
  
```  
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
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
