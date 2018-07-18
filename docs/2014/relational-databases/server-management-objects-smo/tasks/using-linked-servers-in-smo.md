---
title: 在 SMO 中使用連結的伺服器 |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 57c84f885a53fd2b277fbb34c9bfecc178e0fe89
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319918"
---
# <a name="using-linked-servers-in-smo"></a>在 SMO 中使用連結的伺服器
  連結的伺服器代表遠端伺服器上的 OLE DB 資料來源。 遠端 OLE DB 資料來源連結至執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。  
  
 遠端資料庫伺服器可以連結至目前的執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 OLE DB 提供者。 在 SMO 中，連結的伺服器都由<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A>屬性參考的集合<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>物件。 這些物件會儲存與連結的伺服器建立連接所需的登入認證。  
  
## <a name="ole-db-providers"></a>OLE-DB 提供者  
 在 SMO 中，已安裝的 OLE-DB 提供者是由 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 物件的集合表示。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱 < [Visual Studio.NET 中建立 Visual Basic SMO Project](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)並[建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-basic"></a>在 Visual Basic 中建立與 OLE-DB 提供者伺服器的連結  
 在程式碼範例示範如何建立的連結[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB，利用異質資料來源<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 藉由指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]做為產品名稱，資料會連結的伺服器上使用來存取[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB 提供者，也就是正式的 OLE DB 提供者的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLinkedServers1](SMO How to#SMO_VBLinkedServers1)]  -->  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>在 Visual C# 中建立與 OLE-DB 提供者伺服器的連結  
 在程式碼範例示範如何建立的連結[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB，利用異質資料來源<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 藉由指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]做為產品名稱，資料會連結的伺服器上使用來存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 提供者，也就是正式的 OLE DB 提供者的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
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
 在程式碼範例示範如何建立的連結[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB，利用異質資料來源<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>物件。 藉由指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]做為產品名稱，資料會連結的伺服器上使用來存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 提供者，也就是正式的 OLE DB 提供者的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
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
  
  
