---
description: sp_help_notification (Transact-SQL)
title: sp_help_notification (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cce6fd1c7645857019399dae9934c8b730e14f77
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536047"
---
# <a name="sp_help_notification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @object_type = ] 'object_type'` 要傳回的資訊類型。 *object_type*是 **char (9) **，沒有預設值。 *object_type* 可以是警示，其中會列出指派給所提供之操作員名稱的警示 *，* 或列出負責所提供之警示名稱的操作員 *。*  
  
`[ @name = ] 'name'` 如果 *object_type* 是操作員) 則為運算子 (名稱，如果 *object_type* 是警示) ，則為 (的警示名稱。 *名稱* 是 **sysname**，沒有預設值。  
  
`[ @enum_type = ] 'enum_type'` 傳回的 *object_type*資訊。 *enum_type* 在大部分情況下都是實際的。 *enum_type*是 **char (10) **，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|ACTUAL|僅列出與*名稱*相關聯的*object_types* 。|  
|ALL|列出所有的*object_types* ，包括未與 *名稱*相關聯的所有。|  
|TARGET|只會列出符合所提供*target_name*的*object_types* ，不論是否有*名稱*關聯。|  
  
`[ @notification_method = ] notification_method` 判斷要傳回之通知方法資料行的數值。 *notification_method* 是 **Tinyint**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|電子郵件：只傳回 **use_email** 資料行。|  
|**2**|呼機：只傳回 **use_pager** 資料行。|  
|**4**|NetSend：只傳回 **use_netsend** 資料行。|  
|**7**|全部：傳回所有資料行。|  
  
`[ @target_name = ] 'target_name'` 如果 *object_type* 是警示) ，則為搜尋 (的警示名稱，如果 *object_type* 是操作員) ，則為搜尋 (的操作員名稱。 只有當*enum_type*為目標時，才需要*target_name* 。 *target_name* 是 **sysname**，預設值是 Null。  
  
## <a name="return-code-valves"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 如果 *object_type* 是 **警示**，結果集會列出指定操作員的所有警示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警示識別碼。|  
|**alert_name**|**sysname**|警示名稱。|  
|**use_email**|**int**|利用電子郵件來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_pager**|**int**|利用呼叫器來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_netsend**|**int**|利用網路快顯視窗來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_email**|**int**|這個警示所傳送的電子郵件通知數目。|  
|**has_pager**|**int**|這個警示所傳送的呼叫器通知數目。|  
|**has_netsend**|**int**|此警示傳送的 **網路傳送** 通知數目。|  
  
 如果 **object_type** 為 **運算子**，結果集會列出給定警示的所有運算子。  
  
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
 這個預存程式必須從 **msdb** 資料庫執行。  
  
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
  
  
