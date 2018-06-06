---
title: sp_help_operator (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0fc94dd72bdb96516c6cd65f1e405951cbf8ff45
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpoperator-transact-sql"></a>sp_help_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告定義給伺服器之操作員的相關資訊。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>引數  
 [ **@operator_name=** ] **'***operator_name***'**  
 操作員名稱。 *operator_name*是**sysname**。 如果*operator_name*是未指定，會傳回有關所有操作員的資訊。  
  
 [ **@operator_id=** ] *operator_id*  
 所要求為其相關資訊之操作員的識別碼。 *operator_id*是**int**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*operator_id*或*operator_name*必須指定，但不可同時指定兩者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|操作員識別碼。|  
|**name**|**sysname**|操作員名稱。|  
|**enabled**|**tinyint**|操作員可以接收任何通知：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**email_address**|**nvarchar(100)**|操作員電子郵件地址。|  
|**last_email_date**|**int**|操作員前次收到電子郵件通知的日期。|  
|**last_email_time**|**int**|操作員前次收到電子郵件通知的時間。|  
|**pager_address**|**nvarchar(100)**|操作員呼叫器號碼。|  
|**last_pager_date**|**int**|操作員前次收到呼叫器通知的日期。|  
|**last_pager_time**|**int**|操作員前次收到呼叫器通知的時間。|  
|**weekday_pager_start_time**|**int**|操作員在工作日能夠收到呼叫器通知的期間之起始時間。|  
|**weekday_pager_end_time**|**int**|操作員在工作日能夠收到呼叫器通知的期間之最終時間。|  
|**saturday_pager_start_time**|**int**|操作員在星期六能夠收到呼叫器通知的期間之起始時間。|  
|**saturday_pager_end_time**|**int**|操作員在星期六能夠收到呼叫器通知的期間之最終時間。|  
|**sunday_pager_start_time**|**int**|操作員在星期日能夠收到呼叫器通知的期間之起始時間。|  
|**sunday_pager_end_time**|**int**|操作員在星期日能夠收到呼叫器通知的期間之最終時間。|  
|**pager_days**|**tinyint**|位元遮罩 (**1** = 星期日、 **64** = 星期六) 天的當週，指出操作員能夠收到呼叫器通知的時間。|  
|**netsend_address**|**nvarchar(100)**|網路快顯通知的操作員位址。|  
|**last_netsend_date**|**int**|操作員前次收到網路快顯通知的日期。|  
|**last_netsend_time**|**int**|操作員前次收到網路快顯通知的時間。|  
|**category_name**|**sysname**|這位操作員所屬的操作員類別目錄名稱。|  
  
## <a name="remarks"></a>備註  
 **sp_help_operator**必須從執行**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
## <a name="examples"></a>範例  
 下列範例會報告 `François Ajenstat` 這位操作員的相關資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_operator &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
