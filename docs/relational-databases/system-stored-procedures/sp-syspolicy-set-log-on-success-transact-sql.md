---
title: "sp_syspolicy_set_log_on_success (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_set_log_on_success_TSQL
- sp_syspolicy_set_log_on_success
dev_langs: TSQL
helpviewer_keywords: sp_syspolicy_set_log_on_success
ms.assetid: 6b33383b-5949-488a-a911-59299a270f46
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95d79dfcd1e4942cb5604df98b8edc49eb4dc2da
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="spsyspolicysetlogonsuccess-transact-sql"></a>sp_syspolicy_set_log_on_success (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定以原則為基礎的管理的原則記錄檔中是否會記錄成功的原則評估。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syspolicy_set_log_on_success [ @value = ] value  
```  
  
## <a name="arguments"></a>引數  
 [  **@value=** ]*值*  
 判斷是否會記錄成功的原則評估。 *值*是**sqlvariant**，而且可以是下列值之一：  
  
-   0 或 'false' = 成功的原則評估不會記錄下來。  
  
-   1 或 'true' = 成功的原則評估會記錄下來。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須在 msdb 系統資料庫的內容中執行 sp_syspolicy_set_log_on_success。  
  
 當*值*是設定為 0 或 'false'，只將失敗的原則評估都會記錄下來。  
  
## <a name="permissions"></a>Permissions  
 需要 PolicyAdministratorRole 固定資料庫角色中的成員資格。  
  
> **重要！！** 可能會提高認證：PolicyAdministratorRole 角色中的使用者可以建立伺服器觸發程序以及排程可能會影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體作業的原則執行。 例如，PolicyAdministratorRole 角色中的使用者可以建立防止在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中建立大部分物件的原則。 由於可能會提高認證，因此 PolicyAdministratorRole 角色應該只授與可控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 組態的受信任使用者。  
  
## <a name="examples"></a>範例  
 下列範例會啟用成功原則評估的記錄。  
  
```  
EXEC msdb.dbo.sp_syspolicy_set_log_on_success @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [以原則為基礎的管理預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_configure &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)  
  
  
