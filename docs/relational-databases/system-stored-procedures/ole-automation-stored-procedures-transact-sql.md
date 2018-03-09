---
title: "OLE Automation 預存程序 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], OLE Automation
- OLE Automation [SQL Server], stored procedures
ms.assetid: ff16a833-01fe-4877-8aa6-55b72603ec2e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd6464e7631d502cbb24eadb7dd0f5a2590d30e4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="ole-automation-stored-procedures-transact-sql"></a>OLE Automation 預存程序 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援下列可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中使用 OLE Automation 物件的系統預存程序。 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會封鎖對 OLE Automation 預存程序的存取，因為在這部伺服器的安全性組態設定期間已關閉這個元件。 系統管理員可以使用 sp_configure 來啟用對 OLE Automation 程序的存取。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
|||  
|-|-|  
|[sp_OACreate](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)|[sp_OAMethod](../../relational-databases/system-stored-procedures/sp-oamethod-transact-sql.md)|  
|[sp_OADestroy](../../relational-databases/system-stored-procedures/sp-oadestroy-transact-sql.md)|[sp_OASetProperty](../../relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql.md)|  
|[sp_OAGetErrorInfo](../../relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql.md)|[sp_OAStop](../../relational-databases/system-stored-procedures/sp-oastop-transact-sql.md)|  
|[sp_OAGetProperty](../../relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql.md)|[物件階層語法 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/object-hierarchy-syntax-transact-sql.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLE Automation 程序伺服器組態選項](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
  
