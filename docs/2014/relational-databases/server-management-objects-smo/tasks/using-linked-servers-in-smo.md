---
title: 在 SMO 中使用連結的伺服器 |Microsoft 文件
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
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7ae91209d5786ed976e1c29ed9b51d7d52e0070a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033897"
---
# <a name="using-linked-servers-in-smo"></a>在 SMO 中使用連結的伺服器
  連結的伺服器代表遠端伺服器上的 OLE DB 資料來源。 遠端 OLE DB 資料來源會連結到的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。  
  
 遠端資料庫伺服器可以連結至目前的執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 OLE DB 提供者。 在 SMO 中，連結的伺服器都由<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A>屬性參考的集合<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>物件。 這些物件會儲存與連結的伺服器建立連接所需的登入認證。  
  
## <a name="ole-db-providers"></a>OLE-DB 提供者  
 在 SMO 中，已安裝的 OLE-DB 提供者是由 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 物件的集合表示。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[Visual Studio.NET 中建立 Visual Basic SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[建立 Visual C&#35; SMO Project in Visual Studio](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-basic"></a>在 Visual Basic 中建立與 OLE-DB 提供者伺服器的連結  
 程式碼範例示範如何建立通往[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB、 異質資料來源使用<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 藉由指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]為產品名稱時，資料存取連結的伺服器上使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB 提供者的官方 OLE DB 提供者的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLinkedServers1](SMO How to#SMO_VBLinkedServers1)]  -->  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>在 Visual C# 中建立與 OLE-DB 提供者伺服器的連結  
 程式碼範例示範如何建立通往[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB、 異質資料來源使用<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 藉由指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]為產品名稱時，資料存取連結的伺服器上使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 提供者的官方 OLE DB 提供者的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>在 PowerShell 中建立與 OLE-DB 提供者伺服器的連結  
 程式碼範例示範如何建立通往[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB、 異質資料來源使用<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 藉由指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]為產品名稱時，資料存取連結的伺服器上使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 提供者的官方 OLE DB 提供者的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
```  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  