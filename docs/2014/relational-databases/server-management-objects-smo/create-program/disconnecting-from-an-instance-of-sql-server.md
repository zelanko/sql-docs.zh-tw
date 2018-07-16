---
title: 從 SQL Server 的執行個體中斷連接 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a232aefef8293ef84b99dce5aa3864e9702dab1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225258"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>從 SQL Server 的執行個體中斷連接
  以手動方式關閉和中斷連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Management Objects (SMO) 物件就不需要。 連接會視需要開啟和關閉。  
  
## <a name="connection-pooling"></a>連接共用  
 當<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A>呼叫方法，不會自動釋放連接。 您必須明確地呼叫 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 方法，才能釋放對連接集區的連接。 此外，您也可以要求非共用連接。 執行此作業的方法是設定 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 屬性的 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 屬性，該屬性會參考 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>從 RMO 的 SQL Server 執行個體中斷連接  
 在使用 RMO 進行程式開發時關閉伺服器連接，與使用 SMO 時稍有不同。  
  
 因為 RMO 物件的伺服器連接由維護<xref:Microsoft.SqlServer.Management.Common.ServerConnection>物件，這個物件也會從執行個體中斷連線時[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]您使用 RMO 進行程式設計時。 使用關閉的連線<xref:Microsoft.SqlServer.Management.Common.ServerConnection>物件，請呼叫<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A>RMO 物件的方法。 在關閉連接之後，就無法使用 RMO 物件。  
  
## <a name="example"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>在 Visual Basic 中關閉和中斷 SMO 物件的連接  
 此程式碼範例示範如何藉由設定要求非共用的連接<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A>屬性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>物件屬性。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>在 Visual C# 中關閉和中斷 SMO 物件的連接  
 此程式碼範例示範如何藉由設定要求非共用的連接<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A>屬性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>物件屬性。  
  
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
  
  
