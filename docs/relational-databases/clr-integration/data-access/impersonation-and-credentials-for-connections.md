---
title: 連接的模擬和認證 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 83ca2d7718af4151b375b0db7f2a0942ced8ac4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782136"
---
# <a name="impersonation-and-credentials-for-connections"></a>連接的模擬和認證
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合中，使用 Windows 驗證是很複雜的工作，但是要比使用 SQL Server 驗證來得安全。 當使用 Windows 驗證時，請牢記以下的考量事項。  
  
 根據預設，連接到 Windows 的 SQL Server 處理序需要 SQL Server Windows 服務帳戶的安全性內容。 但是，可將 CLR 函數對應到 Proxy 識別，好讓它的傳出連接具有與 Windows 服務帳戶不同的安全性內容。  
  
 在某些情況下，您可能想要使用模擬呼叫端**SqlContext.WindowsIdentity**屬性而不是服務帳戶身分執行。 **WindowsIdentity**執行個體代表叫用呼叫的程式碼，並只有當用戶端使用 Windows 驗證時使用的用戶端的身分識別。 取得後**WindowsIdentity**執行個體，您可以呼叫**Impersonate**變更執行緒的安全性權杖，然後開啟 ADO.NET 連線，代表用戶端。  
  
 呼叫 SQLContext.WindowsIdentity.Impersonate 之後，您無法存取本機資料，而且您無法存取系統資料。 若要存取的資料同樣地，您必須呼叫 WindowsImpersonationContext.Undo。  
  
 下列範例示範如何使用模擬呼叫端**SqlContext.WindowsIdentity**屬性。  
  
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
>  如需模擬中行為變更的資訊，請參閱[SQL Server 2016 中的 Database Engine 功能的突破性變更](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 此外，如果您已經取得 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 識別執行個體，在預設情況下您無法將該執行個體傳播至另一部電腦；Windows 安全性基礎結構會根據預設來限制這項作業。 但是，有一項機制稱為「委派」，它可啟用多部受信任電腦之間的 Windows 識別傳播。 您可以深入了解委派，在 TechNet 文章中，「[Kerberos 通訊協定轉換與限制委派](http://go.microsoft.com/fwlink/?LinkId=50419)"。  
  
## <a name="see-also"></a>另請參閱  
 [SqlContext 物件](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
