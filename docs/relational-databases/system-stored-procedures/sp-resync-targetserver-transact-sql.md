---
title: sp_resync_targetserver (TRANSACT-SQL) |Microsoft 文件
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
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d91ef10c7f1e98c4ad65d014f90fc42b0317ec5
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "33252457"
---
# <a name="spresynctargetserver-transact-sql"></a>sp_resync_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  重新同步處理指定目標伺服器中的所有多伺服器作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>引數  
 [ **@server_name =**] **'***server***'**  
 要重新同步處理的伺服器名稱。 *server* 是 **sysname**，沒有預設值。 如果**所有**指定，則所有目標伺服器會重新同步都處理。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 報告的結果**sp_post_msx_operation**動作。  
  
## <a name="remarks"></a>備註  
 **sp_resync_targetserver**刪除目前的目標伺服器的指示集，並公佈一組新的目標伺服器下載。 這組新的指示由刪除所有多伺服器作業的指示所組成，後面接著目前鎖定這部目標伺服器的每項作業的插入動作。  
  
## <a name="permissions"></a>Permissions  
 這個程序的執行權限預設會授與 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會重新同步處理 `SEATTLE1` 目標伺服器。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_resync_targetserver  
    N'SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_help_downloadlist &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [sp_post_msx_operation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
