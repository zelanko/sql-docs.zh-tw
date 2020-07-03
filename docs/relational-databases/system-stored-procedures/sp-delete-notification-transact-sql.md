---
title: sp_delete_notification （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_notification_TSQL
- sp_delete_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_notification
ms.assetid: b55d3898-596d-47a5-a4f0-d65dc736223b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 05682482a720bbf14a17497299676ac6a0cc23d4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85862639"
---
# <a name="sp_delete_notification-transact-sql"></a>sp_delete_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  移除特定警示和操作員的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 通知定義。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_notification  
     [ @alert_name = ] 'alert' ,   
     [ @operator_name = ] 'operator'   
```  
  
## <a name="arguments"></a>引數  
`[ @alert_name = ] 'alert'`警示的名稱。 *警示*為**sysname**，沒有預設值。  
  
`[ @operator_name = ] 'operator'`操作員的名稱。 *運算子*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 移除通知只會移除通知；警示和操作員會保留不動。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程式，使用者必須被授與**系統管理員（sysadmin** ）固定伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會在發生 `François Ajenstat` 警示時，移除傳給 `Test Alert` 操作員的通知。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_notification  
    @alert_name = 'Test Alert',  
    @operator_name = 'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_add_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_add_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_help_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [sp_help_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
