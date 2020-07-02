---
title: sp_enum_proxy_for_subsystem （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 8b857472b72081c6368fa3c0a112c7d4729e2c72
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771113"
---
# <a name="sp_enum_proxy_for_subsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

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
`[ @proxy_id = ] proxy_id`要列出資訊的 proxy 識別碼。 *Proxy_id*是**int**，預設值是 Null。 可以指定*識別碼*或*proxy_name* 。  
  
`[ @proxy_name = ] 'proxy_name'`要列出資訊之 proxy 的名稱。 *Proxy_name*是**sysname**，預設值是 Null。 可以指定*識別碼*或*proxy_name* 。  
  
`[ @subsystem_id = ] subsystem_id`要列出資訊的子系統識別碼。 *Subsystem_id*是**int**，預設值是 Null。 可以指定*subsystem_id*或*subsystem_name* 。  
  
`[ @subsystem_name = ] 'subsystem_name'`要列出資訊之子系統的名稱。 *Subsystem_name*是**sysname**，預設值是 Null。 可以指定*subsystem_id*或*subsystem_name* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系統識別碼。|  
|**subsystem_name**|**sysname**|子系統的名稱。|  
|**proxy_id**|**int**|Proxy 識別碼。|  
|**proxy_name**|**sysname**|Proxy 的名稱。|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>備註  
 未提供任何參數時， **sp_enum_proxy_for_subsystem**會列出每個子系統之實例中所有 proxy 的相關資訊。  
  
 當提供 proxy 識別碼或 proxy 名稱時， **sp_enum_proxy_for_subsystem**會列出 proxy 可存取的子系統。 提供子系統識別碼或子系統名稱時， **sp_enum_proxy_for_subsystem**會列出可存取該子系統的 proxy。  
  
 當同時提供 Proxy 資訊和子系統資訊時，如果指定的 Proxy 有權存取指定的子系統，結果集會傳回一個資料列。  
  
 這個預存程式位於**msdb**中。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-associations"></a>A. 列出所有關聯  
 下列範例會列出在目前執行個體的 Proxy 和子系統之間所建立的所有權限。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. 判斷 Proxy 是否有權存取特定子系統  
 如果 `Catalog application proxy` Proxy 有權存取 `ActiveScripting` 子系統，下列範例會傳回一個資料列。 否則，這個範例會傳回空的結果集。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_grant_proxy_to_subsystem &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
