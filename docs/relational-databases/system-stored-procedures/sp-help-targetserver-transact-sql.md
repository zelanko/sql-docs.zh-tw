---
title: sp_help_targetserver (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 236a10fd52508781e503cc2844a49315fe57422e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sphelptargetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出所有目標伺服器。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@server_name=** ] **'***server_name***'**  
 這是要傳回資訊的伺服器名稱。 *server_name*是**nvarchar （30)**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 如果*server_name*未指定， **sp_help_targetserver**傳回下列結果集。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|伺服器識別碼。|  
|**server_name**|**nvarchar(30)**|伺服器名稱。|  
|**location**|**nvarchar(200)**|指定伺服器的位置。|  
|**time_zone_adjustment**|**int**|相對於格林威治標準時間 (GMT) 的時區調整 (以小時為單位)。|  
|**enlist_date**|**datetime**|指定伺服器的編列日期。|  
|**last_poll_date**|**datetime**|前次輪詢伺服器來尋找作業的日期。|  
|**status**|**int**|指定伺服器的狀態。|  
|**unread_instructions**|**int**|伺服器是否有未讀的指示。 如果您已下載所有資料列，這個資料行是**0**。|  
|**local_time**|**datetime**|目標伺服器的本機日期和時間，以前次輪詢主要伺服器之後的目標伺服器本機時間為基礎。|  
|**enlisted_by_nt_user**|**nvarchar(100)**|編列了目標伺服器的 Microsoft Windows 使用者。|  
|**poll_interval**|**int**|目標伺服器輪詢主要 SQLServerAgent 服務來下載作業和上傳作業狀態的頻率 (以秒為單位)。|  
  
## <a name="permissions"></a>Permissions  
 若要執行這個預存程序，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. 列出所有已註冊的目標伺服器的資訊  
 下列範例會列出所有已註冊的目標伺服器的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. 列出特定目標伺服器的資訊  
 下列範例會列出目標伺服器 `SEATTLE2` 的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_targetservergroup &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver 來&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
