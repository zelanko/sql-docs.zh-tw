---
description: sp_grant_proxy_to_subsystem (Transact-SQL)
title: sp_grant_proxy_to_subsystem (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_subsystem_TSQL
- sp_grant_login_to_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_proxy_to_subsystem
ms.assetid: 866aaa27-a1e0-453a-9b1b-af39431ad9c2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 964bab1ac95d80d05f16fa8b538f1ecd5f15352c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469396"
---
# <a name="sp_grant_proxy_to_subsystem-transact-sql"></a>sp_grant_proxy_to_subsystem (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  授與子系統的 Proxy 存取權。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @proxy_id = ] id` 要授與存取權之 proxy 的 proxy 識別碼。 *Proxy_id*是**int**，預設值是 Null。 必須指定 *proxy_id* 或 *proxy_name* ，但不能同時指定兩者。  
  
`[ @proxy_name = ] 'proxy_name'` 要授與存取權的 proxy 名稱。 *Proxy_name*是**sysname**，預設值是 Null。 必須指定 *proxy_id* 或 *proxy_name* ，但不能同時指定兩者。  
  
`[ @subsystem_id = ] id` 要授與存取權的子系統識別碼。 *Subsystem_id*是**int**，預設值是 Null。 必須指定 *subsystem_id* 或 *subsystem_name* ，但不能同時指定兩者。 下表列出每個子系統的值。  
  
|值|說明|  
|-----------|-----------------|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX Script<br /><br /> ** \* \* 重要 \* 事項 \* ：** 在未來的版本中，將會從代理程式移除 ActiveX 腳本子系統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。|  
|**3**|作業系統 (**CmdExec**)|  
|**4**|複寫快照集代理程式|  
|**5**|複寫記錄讀取器代理程式|  
|**6**|複寫散發代理程式|  
|**7**|Replication Merge Agent|  
|**8**|複寫佇列讀取器代理程式|  
|**9**|Analysis Services 查詢|  
|**10**|Analysis Services 命令|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝執行|  
|**12**|PowerShell 指令碼|  
| &nbsp; | &nbsp; |
  
`[ @subsystem_name = ] 'subsystem_name'` 要授與存取權的子系統名稱。 **Subsystem_name**是**sysname**，預設值是 Null。 必須指定 *subsystem_id* 或 *subsystem_name* ，但不能同時指定兩者。 下表列出每個子系統的值。  
  
|值|描述|  
|-----------|-----------------|  
|**ActiveScripting**|ActiveX Script|  
|**CmdExec**|作業系統 (**CmdExec**)|  
|**快照式**|複寫快照集代理程式|  
|**LogReader**|複寫記錄讀取器代理程式|  
|**Distribution**|複寫散發代理程式|  
|**合併式**|Replication Merge Agent|  
|**QueueReader**|複寫佇列讀取器代理程式|  
|**ANALYSISQUERY**|Analysis Services 查詢|  
|**ANALYSISCOMMAND**|Analysis Services 命令|  
|**Dts**|SSIS 封裝執行|  
|**PowerShell**|PowerShell 指令碼|  
| &nbsp; | &nbsp; |
  
## <a name="remarks"></a>備註  
 授與對子系統的 Proxy 存取權，並不會變更 Proxy 所指定之主體的權限。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_grant_proxy_to_subsystem**。  
  
## <a name="examples"></a>範例  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>A. 依識別碼授與子系統的存取權  
 下列範例會授與 `Catalog application proxy` 這個 Proxy 之 ActiveX Scripting 子系統存取權。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>B. 依名稱授與子系統的存取權  
 下列範例會授與 `Catalog application proxy` 這個 Proxy 的 SSIS 封裝執行子系統存取權。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [實行 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_revoke_proxy_from_subsystem &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_update_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
