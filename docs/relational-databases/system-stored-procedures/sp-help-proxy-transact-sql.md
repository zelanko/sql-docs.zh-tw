---
title: sp_help_proxy （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e9c59c6347317d193eafe43c511c0ece3831e29c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750528"
---
# <a name="sp_help_proxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  列出一或多個 Proxy 的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>引數  
`[ @proxy_id = ] id`要列出資訊之 proxy 的 proxy 識別碼。 *Proxy_id*是**int**，預設值是 Null。 可以指定*識別碼*或*proxy_name* 。  
  
`[ @proxy_name = ] 'proxy_name'`要列出資訊之 proxy 的名稱。 *Proxy_name*是**sysname**，預設值是 Null。 可以指定*識別碼*或*proxy_name* 。  
  
`[ @subsystem_name = ] 'subsystem_name'`要列出 proxy 的子系統名稱。 *Subsystem_name*是**sysname**，預設值是 Null。 當指定*subsystem_name*時，也必須指定*名稱*。  
  
 下表列出每個子系統的值。  
  
|值|說明|  
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
|Dts|SSIS 封裝執行|  
|PowerShell|PowerShell 指令碼|  
  
`[ @name = ] 'name'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要列出 proxy 的登入名稱。 名稱是**Nvarchar （256）**，預設值是 Null。 當指定*name*時，也必須指定*subsystem_name* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Proxy 識別碼。|  
|**name**|**sysname**|Proxy 的名稱。|  
|**credential_identity**|**sysname**|Proxy 相關認證的 Microsoft Windows 網域名稱和使用者名稱。|  
|**後**|**tinyint**|是否啟用這個 Proxy。 { **0** = 未啟用， **1** = 已啟用}|  
|**description**|**nvarchar(1024)**|這個 Proxy 的描述。|  
|**user_sid**|**Varbinary （85）**|這個 Proxy 的 Windows 使用者之 Windows 安全性識別碼。|  
|**credential_id**|**int**|這個 Proxy 的相關認證識別碼。|  
|**credential_identity_exists**|**int**|credential_identity 是否存在。 { 0 = 不存在，1 = 存在 }|  
  
## <a name="remarks"></a>備註  
 未提供任何參數時， **sp_help_proxy**會列出實例中所有 proxy 的資訊。  
  
 若要判斷登入可用於指定子系統的 proxy，請指定*name*和*subsystem_name*。 當提供這些引數時， **sp_help_proxy**會列出指定的登入可能會存取的 proxy，以及可用於指定子系統的 proxy。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
 如需**SQLAgentOperatorRole**的詳細資訊，請參閱[SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
> [!NOTE]  
>  只有在**系統管理員（sysadmin** ）的成員執行此預存程式時，才會在結果集中傳回**credential_identity**和**user_sid**資料行。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-information-for-all-proxies"></a>A. 列出所有 Proxy 的資訊  
 下列範例會列出執行個體中所有 Proxy 的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. 列出特定 Proxy 的資訊  
 下列範例會列出名稱為 `Catalog application proxy` 之 Proxy 的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
