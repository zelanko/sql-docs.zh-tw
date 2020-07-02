---
title: sp_help_notification （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3fe885be9072f24c18e6115efcf511faea2d8908
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85634364"
---
# <a name="sp_help_notification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  報告一份給定操作員的警示清單，或一份給定警示的操作員清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_notification  
     [ @object_type = ] 'object_type' ,  
     [ @name = ] 'name' ,  
     [ @enum_type = ] 'enum_type' ,   
     [ @notification_method = ] notification_method   
     [ , [ @target_name = ] 'target_name' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @object_type = ] 'object_type'`要傳回的資訊類型。 *object_type*是**char （9）**，沒有預設值。 *object_type*可以是 [警示]，其中會列出指派給所提供之操作員名稱的警示 *，或 [操作員]，其中*列出負責所提供之警示名稱的操作員 *。*  
  
`[ @name = ] 'name'`操作員名稱（如果*object_type*是運算子）或警示名稱（如果*object_type*是警示）。 *名稱*是**sysname**，沒有預設值。  
  
`[ @enum_type = ] 'enum_type'`傳回的*object_type*資訊。 *enum_type*在大多數情況下都是實際的。 *enum_type*是**char （10）**，沒有預設值，而且可以是下列其中一個值。  
  
|值|說明|  
|-----------|-----------------|  
|ACTUAL|僅列出與*名稱*相關聯的*object_types* 。|  
|ALL|列出所有 object_types，包括未與 [*名稱*] 相關聯的*object_types* 。|  
|TARGET|只會列出符合所提供之*target_name*的*object_types* ，不論是否有*名稱*關聯。|  
  
`[ @notification_method = ] notification_method`數值，決定要傳回的通知方法資料行。 *notification_method*是**Tinyint**，它可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|電子郵件：只傳回**use_email**的資料行。|  
|**2**|呼機：只傳回**use_pager**資料行。|  
|**4**|NetSend：只傳回**use_netsend**資料行。|  
|**7**|全部：傳回所有資料行。|  
  
`[ @target_name = ] 'target_name'`要搜尋的警示名稱（如果*object_type*是警示），或要搜尋的操作員名稱（如果*object_type*是運算子）。 只有*enum_type*為目標時，才需要*target_name* 。 *target_name*是**sysname**，預設值是 Null。  
  
## <a name="return-code-valves"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 如果*object_type*是**警示**，結果集會列出指定操作員的所有警示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警示識別碼。|  
|**alert_name**|**sysname**|警示名稱。|  
|**use_email**|**int**|利用電子郵件來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_pager**|**int**|利用呼叫器來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_netsend**|**int**|利用網路快顯視窗來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_email**|**int**|這個警示所傳送的電子郵件通知數目。|  
|**has_pager**|**int**|這個警示所傳送的呼叫器通知數目。|  
|**has_netsend**|**int**|針對此警示傳送的**net send**通知數目。|  
  
 如果**object_type**是**運算子**，則結果集會列出給定警示的所有運算子。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|操作員識別碼。|  
|**operator_name**|**sysname**|操作員名稱。|  
|**use_email**|**int**|利用電子郵件來傳送操作員的通知：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_pager**|**int**|利用呼叫器來傳送操作員的通知：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_netsend**|**int**|這是用來通知操作員的網路快顯視窗：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_email**|**int**|操作員有電子郵件地址：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_pager**|**int**|操作員具有呼叫器號碼：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_netsend**|**int**|操作員已設定了 net send 通知。<br /><br /> **1** = 是<br /><br /> **0** = 否|  
  
## <a name="remarks"></a>備註  
 這個預存程式必須從**msdb**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程序，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>A. 列出特定操作員的警示  
 下列範例會傳回 `François Ajenstat` 操作員收到的任何一種通知所針對的所有警示。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_notification   
    @object_type = N'ALERTS',  
    @name = N'François Ajenstat',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
### <a name="b-listing-operators-for-a-specific-alert"></a>B. 列出特定警示的操作員  
 下列範例會傳回收到 `Test Alert` 警示的任何一種通知的所有操作員。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_notification  
    @object_type = N'OPERATORS',  
    @name = N'Test Alert',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
