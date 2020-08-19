---
description: sp_revoke_proxy_from_subsystem (Transact-SQL)
title: sp_revoke_proxy_from_subsystem (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d58ec6db017fee031a2de2e242a18281eb3b7a68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469213"
---
# <a name="sp_revoke_proxy_from_subsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  撤銷 Proxy 的子系統存取權  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @proxy_id = ] id` 要撤銷其存取權之 proxy 的 proxy 識別碼。 *Proxy_id*是**int**，預設值是 Null。 必須指定 *proxy_id* 或 *proxy_name* ，但不能同時指定兩者。  
  
`[ @proxy_name = ] 'proxy_name'` 要撤銷存取權的 proxy 名稱。 *Proxy_name*是**sysname**，預設值是 Null。 必須指定 *proxy_id* 或 *proxy_name* ，但不能同時指定兩者。  
  
`[ @subsystem_id = ] id` 要撤銷其存取權的子系統識別碼。 *Subsystem_id*是**int**，預設值是 Null。 必須指定 *subsystem_id* 或 *subsystem_name* ，但不能同時指定兩者。 下表列出每個子系統的值。  
  
|值|說明|  
|-----------|-----------------|  
|**2**|ActiveX Script<br /><br /> ** \* \* 重要 \* 事項 \* ：** 在未來的版本中，將會從代理程式移除 ActiveX 腳本子系統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。|  
|**3**|作業系統 (CmdExec)|  
|**4**|複寫快照集代理程式|  
|**5**|複寫記錄讀取器代理程式|  
|**6**|複寫散發代理程式|  
|**7**|Replication Merge Agent|  
|**8**|複寫佇列讀取器代理程式|  
|**9**|Analysis Services 命令|  
|**10**|Analysis Services 查詢|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝執行|  
|**12**|PowerShell 指令碼|  
  
`[ @subsystem_name = ] 'subsystem_name'` 要撤銷其存取權的子系統名稱。 *Subsystem_name*是**sysname**，預設值是 Null。 必須指定 *subsystem_id* 或 *subsystem_name* ，但不能同時指定兩者。 下表列出每個子系統的值。  
  
|值|描述|  
|-----------|-----------------|  
|ActiveScripting|ActiveX Script|  
|CmdExec|作業系統 (CmdExec)|  
|快照式|複寫快照集代理程式|  
|LogReader|複寫記錄讀取器代理程式|  
|散發|複寫散發代理程式|  
|合併|Replication Merge Agent|  
|QueueReader|複寫佇列讀取器代理程式|  
|ANALYSISQUERY|Analysis Services 命令|  
|ANALYSISCOMMAND|Analysis Services 查詢|  
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝執行|  
|PowerShell|PowerShell 指令碼|  
  
## <a name="remarks"></a>備註  
 撤銷對子系統的存取權，並不會變更 Proxy 所指定之主體的權限。  
  
> [!NOTE]  
>  若要判斷哪些作業步驟參考 proxy，請以滑鼠右鍵按一下 Microsoft **SQL Server Agent** **下的 proxy**節點，然後按一下 [內容] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 **Properties** 在 [ **Proxy 帳戶屬性** ] 對話方塊中，選取 [ **參考** ] 頁面，以查看參考此 Proxy 的所有作業步驟。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_revoke_proxy_from_subsystem**。  
  
## <a name="examples"></a>範例  
 下列範例會撤銷 `Catalog application proxy` 這個 Proxy 的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 子系統存取權。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的 SQL Server Agent 預存程式 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [實行 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_grant_proxy_to_subsystem &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
