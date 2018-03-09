---
title: "連接的模擬和認證 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd87459202b3e18af6c16ef16becaccf172eb62e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="impersonation-and-credentials-for-connections"></a>連接的模擬和認證
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合中，使用 Windows 驗證是很複雜的工作，但是要比使用 SQL Server 驗證來得安全。 當使用 Windows 驗證時，請牢記以下的考量事項。  
  
 根據預設，連接到 Windows 的 SQL Server 處理序需要 SQL Server Windows 服務帳戶的安全性內容。 但是，可將 CLR 函數對應到 Proxy 識別，好讓它的傳出連接具有與 Windows 服務帳戶不同的安全性內容。  
  
 在某些情況下，您可能想要使用模擬呼叫者**SqlContext.WindowsIdentity**屬性而不是服務帳戶的身分執行。 **WindowsIdentity**執行個體代表叫用呼叫的程式碼，和用戶端使用 Windows 驗證時才可用的用戶端的身分識別。 取得後**WindowsIdentity**執行個體，您可以呼叫**Impersonate**變更執行緒的安全性權杖，然後開啟 ADO.NET 連接，代表用戶端。  
  
 呼叫 SQLContext.WindowsIdentity.Impersonate 之後，您無法存取本機資料，而且您無法存取系統資料。 若要存取資料，必須呼叫 WindowsImpersonationContext.Undo。  
  
 下列範例示範如何使用模擬呼叫者**SqlContext.WindowsIdentity**屬性。  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  如需模擬中行為變更的資訊，請參閱[SQL Server 2016 中對於 Database Engine 功能的突破性變更](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 此外，如果您已經取得 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 識別執行個體，在預設情況下您無法將該執行個體傳播至另一部電腦；Windows 安全性基礎結構會根據預設來限制這項作業。 但是，有一項機制稱為「委派」，它可啟用多部受信任電腦之間的 Windows 識別傳播。 您可以進一步了解 TechNet 文章中的委派"[Kerberos 通訊協定轉換與限制委派](http://go.microsoft.com/fwlink/?LinkId=50419)"。  
  
## <a name="see-also"></a>另請參閱  
 [SqlContext 物件](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
