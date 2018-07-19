---
title: sp_update_notification (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc08790ad08ce6bb4e94e61a8c3bdfc58615edf9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260201"
---
# <a name="spupdatenotification-transact-sql"></a>sp_update_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新警示通知的通知方法。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>引數  
 [  **@alert_name =**] **'***警示***'**  
 與此通知相關聯的警示名稱。 *警示*是**sysname**，沒有預設值。  
  
 [ **@operator_name =**]  **'***operator***'**  
 發生警示時所要通知的操作員。 *運算子*是**sysname**，沒有預設值。  
  
 [  **@notification_method =**]*通知*  
 用來通知操作員的方法。 *通知*是**tinyint**，沒有預設值，它可以是下列一或多個這些值。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|電子郵件|  
|**2**|呼叫器|  
|**4**|**net send**|  
|**7**|所有方法|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_update_notification**必須從執行**msdb**資料庫。  
  
 您可以更新並沒有使用指定的所需的位址資訊之操作員的通知*notification_method*。 如果傳送電子郵件訊息或呼叫器通知失敗，會在 Microsoft SQL Server Agent 錯誤記錄中報告這項失敗。  
  
## <a name="permissions"></a>Permissions  
 若要執行這個預存程序，使用者必須授與**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會修改傳送通知的通知方法`François Ajenstat`警示`Test Alert`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_notification &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
