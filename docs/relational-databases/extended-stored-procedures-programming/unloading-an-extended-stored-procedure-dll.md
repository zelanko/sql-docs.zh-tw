---
title: "卸載擴充預存程序 DLL |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3bad1f82152cd21d4d5753225842b672016ccec2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>卸載擴充預存程序 DLL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入擴充預存程序 DLL，因為其中的 dll 函式進行呼叫。 該 DLL 在伺服器關閉或系統管理員使用 DBCC 陳述式來卸載它之前，都會保持載入狀態。 例如，此命令會卸載**xp_hello.dll**，允許系統管理員，以較新版的這個檔案複製到目錄，而不會關閉伺服器：  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>另請參閱  
 [DBCC dllname &#40;免費 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
