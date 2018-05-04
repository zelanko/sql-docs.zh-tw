---
title: sp_help_proxy (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f7053bfc6ccbca71783d0bbcdb8b9b5544f9d20
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@proxy_id** = ] *id*  
 要列出資訊的 Proxy 之 Proxy 識別碼。 *Proxy_id*是**int**，預設值是 NULL。 任一*識別碼*或*proxy_name*可指定。  
  
 [ **@proxy_name** = ] **'***proxy_name***'**  
 要列出資訊的 Proxy 名稱。 *Proxy_name*是**sysname**，預設值是 NULL。 任一*識別碼*或*proxy_name*可指定。  
  
 [ **@subsystem_name** =] '*subsystem_name*'  
 要列出 Proxy 的子系統名稱。 *Subsystem_name*是**sysname**，預設值是 NULL。 當*subsystem_name*指定，則*名稱*也必須指定。  
  
 下表列出每個子系統的值。  
  
|Value|Description|  
|-----------|-----------------|  
|ActiveScripting|ActiveX Script|  
|CmdExec|作業系統 (CmdExec)|  
|快照集|複寫快照集代理程式|  
|LogReader|複寫記錄讀取器代理程式|  
|Distribution|複寫散發代理程式|  
|合併式|複寫合併代理程式|  
|QueueReader|複寫佇列讀取器代理程式|  
|ANALYSISQUERY|Analysis Services 命令|  
|ANALYSISCOMMAND|Analysis Services 查詢|  
|Dts|SSIS 封裝執行|  
|PowerShell|PowerShell 指令碼|  
  
 [ **@name** =] '*名稱*'  
 要列出 Proxy 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。 名稱是**nvarchar （256)**，預設值是 NULL。 當*名稱*指定，則*subsystem_name*也必須指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Proxy 識別碼。|  
|**name**|**sysname**|Proxy 的名稱。|  
|**credential_identity**|**sysname**|Proxy 相關認證的 Microsoft Windows 網域名稱和使用者名稱。|  
|**enabled**|**tinyint**|是否啟用這個 Proxy。 { **0** = 未啟用， **1** = 啟用}|  
|**描述**|**nvarchar(1024)**|這個 Proxy 的描述。|  
|**user_sid**|**varbinary(85)**|這個 Proxy 的 Windows 使用者之 Windows 安全性識別碼。|  
|**credential_id**|**int**|這個 Proxy 的相關認證識別碼。|  
|**credential_identity_exists**|**int**|credential_identity 是否存在。 { 0 = 不存在，1 = 存在 }|  
  
## <a name="remarks"></a>備註  
 當未不提供任何參數時， **sp_help_proxy**列出執行個體中的所有 proxy 的資訊。  
  
 若要判斷給定子系統可以使用哪些 proxy 登入，請指定*名稱*和*subsystem_name*。 當未提供這些引數時， **sp_help_proxy**列出指定的登入可能會存取，且可用於指定之子系統的 proxy。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
 如需詳細資訊**SQLAgentOperatorRole**，請參閱[SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
> [!NOTE]  
>  **Credential_identity**和**credential_identity**中只會傳回資料行時的結果集的成員**sysadmin**執行這個預存程序。  
  
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
 [SQL Server Agent 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
