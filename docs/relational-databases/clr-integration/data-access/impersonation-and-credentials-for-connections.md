---
title: 連接的類比和認證微軟文件
description: 在 SQL Server CLR 整合中,您可能希望使用 SqlContext.WindowsIdentity 屬性在 Windows 身份驗證中模擬呼叫者。
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
ms.openlocfilehash: 382185c036055bb9ea689f551c256a26ee83b0b4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485174"
---
# <a name="impersonation-and-credentials-for-connections"></a>連接的模擬和認證
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合中，使用 Windows 驗證是很複雜的工作，但是要比使用 SQL Server 驗證來得安全。 當使用 Windows 驗證時，請牢記以下的考量事項。  
  
 根據預設，連接到 Windows 的 SQL Server 處理序需要 SQL Server Windows 服務帳戶的安全性內容。 但是，可將 CLR 函數對應到 Proxy 識別，好讓它的傳出連接具有與 Windows 服務帳戶不同的安全性內容。  
  
 在某些情況下,您可能希望使用**SqlContext.WindowsIdentity**屬性類比調用方,而不是作為服務帳戶運行。 **WindowsIdentity**實例表示調用調用代碼的用戶端的標識,並且僅在用戶端使用 Windows 身份驗證時才可用。 獲得**WindowsIdentity**實例後,可以調用**Impersonate**以更改線程的安全權杖,然後代表客戶端打開 ADO.NET 連接。  
  
 呼叫 SQLContext.WindowsIdentity.模擬後,您無法存取本地資料,也無法存取系統資料。 要再次存取資料,必須調用 Windows ImpersonationContext.Undo。  
  
 下面的範例展示如何使用**SqlContext.WindowsIdentity**屬性類比調用方。  
  
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
>  有關模擬行為更改的資訊,請參閱[SQL Server 2016 中資料庫引擎功能的中斷更改](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 此外，如果您已經取得 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 識別執行個體，在預設情況下您無法將該執行個體傳播至另一部電腦；Windows 安全性基礎結構會根據預設來限制這項作業。 但是，有一項機制稱為「委派」，它可啟用多部受信任電腦之間的 Windows 識別傳播。 您可以在 TechNet 文章中瞭解有關委派的更多詳細資訊[,"Kerberos 協定轉換和約束委派](https://go.microsoft.com/fwlink/?LinkId=50419)"。  
  
## <a name="see-also"></a>另請參閱  
 [SqlContext 物件](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
