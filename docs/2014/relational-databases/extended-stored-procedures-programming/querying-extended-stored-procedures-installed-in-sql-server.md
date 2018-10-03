---
title: 查詢擴充預存程序，在 SQL Server 安裝 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f8f8616fe8b5a6c06a8492fc713e4e93004d0dad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057268"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>查詢 SQL Server 中安裝的擴充預存程序
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]經過驗證的使用者可以顯示目前定義的擴充預存程序和執行的每一個 DLL 名稱所屬**sp_helpextendedproc**系統程序。 例如，下列範例會傳回 DLL 要**xp_hello**所屬：  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 如果**sp_helpextendedproc**執行而不指定擴充預存程序，所有擴充預存程序和它們的 Dll 會顯示。  
  
> [!IMPORTANT]  
>  只會針對已登入之使用者所擁有或擁有權限的那些擴充預存程序傳回資訊。 只有成員**sysadmin**固定的伺服器角色和**db_owner**， **db_securityadmin**，而**db_ddladmin**固定的資料庫角色可以檢視所有擴充預存程序的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [sp_helpextendedproc &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [sp_addextendedproc &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
