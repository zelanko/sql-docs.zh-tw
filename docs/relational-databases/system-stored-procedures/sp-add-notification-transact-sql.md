---
title: sp_add_notification (TRANSACT-SQL) |Microsoft Docs
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
- sp_add_notification_TSQL
- sp_add_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d17936912a9adca46ddf64724401432c7ef9d43f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038288"
---
# <a name="spaddnotification-transact-sql"></a>sp_add_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定警示通知。  
  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>引數  
 [ **@alert_name=** ] **'***alert***'**  
 這項通知的警示。 *警示*已**sysname**，沒有預設值。  
  
 [ **@operator_name=** ] **'***operator***'**  
 發生警示時所要通知的操作員。 *運算子*已**sysname**，沒有預設值。  
  
 [  **@notification_method=** ] *notification_method*  
 用來通知操作員的方法。 *notification_method*已**tinyint**，沒有預設值。 *notification_method*可以是下列一個或多個這些值結合**OR**邏輯運算子。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|電子郵件|  
|**2**|呼叫器|  
|**4**|**net send**|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_notification**必須從執行**msdb**資料庫。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統。 建議您利用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來設定您的警示基礎結構。  
  
 若要傳送通知來回應警示，您必須先設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來傳送郵件。  
  
 如果傳送電子郵件訊息或呼叫器通知發生失敗，此失敗會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務錯誤記錄檔中報告。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_add_notification**。  
  
## <a name="examples"></a>範例  
 下列範例會加入指定警示 (`Test Alert`) 的電子郵件通知。  
  
> **注意︰** 這個範例假設`Test Alert`已經存在而且`François Ajenstat`是有效的運算子名稱。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_notification  
 @alert_name = N'Test Alert',  
 @operator_name = N'François Ajenstat',  
 @notification_method = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_notification &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [sp_update_notification &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [sp_add_operator &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
