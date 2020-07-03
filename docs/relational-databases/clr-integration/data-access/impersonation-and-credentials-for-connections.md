---
title: 連接的模擬和認證 |Microsoft Docs
description: 在 SQL Server CLR 整合中，您可能會想要使用 SqlCoNtext. WindowsIdentity 屬性來模擬 Windows 驗證中的呼叫者。
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
ms.openlocfilehash: 0561c224a8569c2db13ab71e18d24b4a53282656
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896351"
---
# <a name="impersonation-and-credentials-for-connections"></a>連接的模擬和認證
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合中，使用 Windows 驗證是很複雜的工作，但是要比使用 SQL Server 驗證來得安全。 當使用 Windows 驗證時，請牢記以下的考量事項。  
  
 根據預設，連接到 Windows 的 SQL Server 處理序需要 SQL Server Windows 服務帳戶的安全性內容。 但是，可將 CLR 函數對應到 Proxy 識別，好讓它的傳出連接具有與 Windows 服務帳戶不同的安全性內容。  
  
 在某些情況下，您可能會想要使用**SqlCoNtext. WindowsIdentity**屬性來模擬呼叫者，而不是以服務帳戶的身分執行。 **WindowsIdentity**實例代表叫用呼叫程式碼之用戶端的身分識別，只有在用戶端使用 Windows 驗證時才可使用。 取得**WindowsIdentity**實例之後，您**可以呼叫模擬**來變更執行緒的安全性權杖，然後代表用戶端開啟 ADO.NET 連接。  
  
 呼叫 SQLCoNtext WindowsIdentity 之後，您就無法存取本機資料，也無法存取系統資料。 若要再次存取資料，您必須呼叫 WindowsImpersonationCoNtext。  
  
 下列範例示範如何使用**SqlCoNtext. WindowsIdentity**屬性來模擬呼叫端。  
  
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
>  如需模擬中行為變更的相關資訊，請參閱[SQL Server 2016 中資料庫引擎功能的重大變更](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 此外，如果您已經取得 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 識別執行個體，在預設情況下您無法將該執行個體傳播至另一部電腦；Windows 安全性基礎結構會根據預設來限制這項作業。 但是，有一項機制稱為「委派」，它可啟用多部受信任電腦之間的 Windows 識別傳播。 您可以在 TechNet 文章「[Kerberos 通訊協定轉換和限制委派](https://go.microsoft.com/fwlink/?LinkId=50419)」中深入瞭解委派。  
  
## <a name="see-also"></a>另請參閱  
 [SqlContext 物件](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
