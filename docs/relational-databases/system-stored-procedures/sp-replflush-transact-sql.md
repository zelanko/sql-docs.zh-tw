---
title: sp_replflush (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replflush
- sp_replflush_TSQL
helpviewer_keywords:
- sp_replflush
ms.assetid: 20809f5f-941d-427f-8f0c-de7a6c487584
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44a23ee5d38ba1caf9a16297215d5b21bb1401f7
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037986"
---
# <a name="spreplflush-transact-sql"></a>sp_replflush (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  排清發行項快取。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  您應該不需要手動執行這個程序。 **sp_replflush**只應在資深的複寫支援專家的指示，疑難排解複寫的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replflush  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replflush**用於異動複寫中。  
  
 發行項定義儲存在快取中，以提高效率。 **sp_replflush**每當修改或卸除發行項定義時，由其他複寫預存程序。  
  
 只有單一用戶端連接可以有對於給定資料庫的記錄讀取器存取權。 如果用戶端有記錄讀取器資料庫的存取權，請執行**sp_replflush**可讓用戶端釋放其存取權。 其他用戶端可接著會掃描交易記錄檔使用**sp_replcmds**或是**sp_replshowcmds**。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_replflush**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_repltrans &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
