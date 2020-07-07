---
title: 在 SMO 中使用連結的伺服器 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 06f81e9474a17e8f721d05fa1ba4df3468d3abb0
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008944"
---
# <a name="using-linked-servers-in-smo"></a>在 SMO 中使用連結的伺服器
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  連結的伺服器代表遠端伺服器上的 OLE DB 資料來源。 遠端 OLE DB 資料來源會使用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 物件來連結到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體。  
  
 您可以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 OLE DB 提供者，將遠端資料庫伺服器連結到目前的實例。 在 SMO 中，連結的伺服器會以 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 物件表示。 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> 屬性會參考 <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 物件的集合。 這些物件會儲存與連結的伺服器建立連接所需的登入認證。  
  
## <a name="ole-db-providers"></a>OLE-DB 提供者  
 在 SMO 中，已安裝的 OLE-DB 提供者是由 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 物件的集合表示。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 Visual C&#35; SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>在 Visual C# 中建立與 OLE-DB 提供者伺服器的連結  
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 物件來建立與異質資料來源 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 的連結。 藉由將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 指定為產品名稱，連結伺服器上的資料可藉由使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB Provider ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的官方 OLE DB 提供者) 來存取。  
  
```csharp  
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
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 物件來建立與異質資料來源 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 的連結。 藉由將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 指定為產品名稱，連結伺服器上的資料可藉由使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB Provider ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的官方 OLE DB 提供者) 來存取。  
  
```powershell  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  
