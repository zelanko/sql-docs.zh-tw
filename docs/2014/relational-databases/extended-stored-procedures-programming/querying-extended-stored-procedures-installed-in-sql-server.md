---
title: 查詢擴充預存程序會安裝在 SQL Server |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 25e9b8d1de6acd52182e090f40d955cc17bf5cd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144935"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>查詢 SQL Server 中安裝的擴充預存程序
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已驗證的使用者可以顯示目前定義的擴充預存程序和執行所屬的每個 DLL 名稱**sp_helpextendedproc**系統程序。 例如，下列範例會傳回 DLL 的**xp_hello**所屬：  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 如果**sp_helpextendedproc**執行而不指定擴充預存程序，所有擴充預存程序和它們的 Dll 會顯示。  
  
> [!IMPORTANT]  
>  只會針對已登入之使用者所擁有或擁有權限的那些擴充預存程序傳回資訊。 只有成員**sysadmin**固定的伺服器角色和**db_owner**， **db_securityadmin**，而**db_ddladmin**固定的資料庫角色可以檢視所有擴充預存程序的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [sp_helpextendedproc &#40;Transact SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [sp_addextendedproc &#40;Transact SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
