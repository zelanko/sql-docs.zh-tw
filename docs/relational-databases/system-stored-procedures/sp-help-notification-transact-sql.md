---
title: sp_help_notification (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d003b1f15500b1f6d0b8490d9e712a6a34b100a3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538630"
---
# <a name="sphelpnotification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @object_type = ] 'object_type'` 要傳回的資訊類型。 *object_type*已**char(9)**，沒有預設值。 *object_type*可能是 ALERTS 會列出指派給所提供之操作員名稱的警示 *，* or 運算子，它會列出負責所提供之警示名稱的操作員 *。*  
  
`[ @name = ] 'name'` 運算子名稱 (如果*object_type*是 OPERATORS) 或警示名稱 (如果*object_type*是 ALERTS)。 *名稱*已**sysname**，沒有預設值。  
  
`[ @enum_type = ] 'enum_type'` *Object_type*傳回的資訊。 *enum_type*在大部分情況下是 ACTUAL。 *enum_type*已**char(10)**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|ACTUAL|只列出*object_types*聯*名稱*。|  
|ALL|列出所有*object_types*包括未與相關聯*名稱*。|  
|TARGET|只列出*object_types*符合所提供*target_name*，而不論關聯*名稱*。|  
  
`[ @notification_method = ] notification_method` 數值，決定要傳回的通知方法資料行。 *notification_method*已**tinyint**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|電子郵件： 只會傳回**use_email**資料行。|  
|**2**|呼叫器： 只會傳回**use_pager**資料行。|  
|**4**|NetSend： 只會傳回**use_netsend**資料行。|  
|**7**|全部：傳回所有資料行。|  
  
`[ @target_name = ] 'target_name'` 要搜尋的警示名稱 (如果*object_type*是 ALERTS) 或要搜尋的操作員名稱 (如果*object_type*是 OPERATORS)。 *target_name*才需要*enum_type*是目標。 *target_name*已**sysname**，預設值是 NULL。  
  
## <a name="return-code-valves"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 如果*object_type*是**警示**，結果集會列出給定操作員的所有警示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警示識別碼。|  
|**alert_name**|**sysname**|警示名稱。|  
|**use_email**|**int**|利用電子郵件來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_pager**|**int**|利用呼叫器來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_netsend**|**int**|利用網路快顯視窗來通知操作員：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_email**|**int**|這個警示所傳送的電子郵件通知數目。|  
|**has_pager**|**int**|這個警示所傳送的呼叫器通知數目。|  
|**has_netsend**|**int**|數目**網路傳送**這個警示所傳送的通知。|  
  
 如果**object_type**是**運算子**，結果集會列出給定警示的所有運算子。  
  
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
 這個預存程序必須從執行**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
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
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
