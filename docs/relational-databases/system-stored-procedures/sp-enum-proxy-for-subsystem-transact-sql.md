---
title: "sp_enum_proxy_for_subsystem (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf94c94aed1f43e747703d5f82a7b842252dafef
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="spenumproxyforsubsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 存取子系統的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>引數  
 [ **@proxy_id** = ] *proxy_id*  
 要列出資訊之 Proxy 的識別碼。 *Proxy_id*是**int**，預設值是 NULL。 任一*識別碼*或*proxy_name*可指定。  
  
 [ **@proxy_name** = ] **'***proxy_name***'**  
 要列出資訊的 Proxy 名稱。 *Proxy_name*是**sysname**，預設值是 NULL。 任一*識別碼*或*proxy_name*可指定。  
  
 [ **@subsystem_id** = ] *subsystem_id*  
 要列出資訊之子系統的識別碼。 *Syssubsystems*是**int**，預設值是 NULL。 任一*syssubsystems*或*subsystem_name*可指定。  
  
 [ **@subsystem_name** = ] **'***subsystem_name***'**  
 要列出資訊的子系統名稱。 *Subsystem_name*是**sysname**，預設值是 NULL。 任一*syssubsystems*或*subsystem_name*可指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系統識別碼。|  
|**subsystem_name**|**sysname**|子系統的名稱。|  
|**proxy_id**|**int**|Proxy 識別碼。|  
|**proxy_name**|**sysname**|Proxy 的名稱。|  
  
## <a name="remarks"></a>備註  
 當未不提供任何參數時， **sp_enum_proxy_for_subsystem**列出每個子系統的執行個體中的所有 proxy 的相關資訊。  
  
 當提供 proxy 識別碼或 proxy 名稱時， **sp_enum_proxy_for_subsystem** proxy 有列出子系統存取權。 當提供子系統識別碼或子系統名稱時， **sp_enum_proxy_for_subsystem**列出有權存取這個子系統的 proxy。  
  
 當同時提供 Proxy 資訊和子系統資訊時，如果指定的 Proxy 有權存取指定的子系統，結果集會傳回一個資料列。  
  
 這個預存程序位於**msdb**。  
  
## <a name="permissions"></a>Permissions  
 這個成員的程序預設值的執行權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-associations"></a>A. 列出所有關聯  
 下列範例會列出在目前執行個體的 Proxy 和子系統之間所建立的所有權限。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. 判斷 Proxy 是否有權存取特定子系統  
 如果 `Catalog application proxy` Proxy 有權存取 `ActiveScripting` 子系統，下列範例會傳回一個資料列。 否則，這個範例會傳回空的結果集。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
