---
title: sp_helpdistributor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords:
- sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c86f2b8ba6b9cc7223fa9fa16794ee69aa9cf46e
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533260"
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出散發者、 散發資料庫、 工作目錄的相關資訊並[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式的使用者帳戶。 這個預存程序執行於發行集資料庫或任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
`[ @distributor = ] 'distributor' OUTPUT` 是散發者的名稱。 散發者已**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
`[ @distribdb = ] 'distribdb' OUTPUT` 是散發資料庫的名稱。 *distribdb*已**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
`[ @directory = ] 'directory' OUTPUT` 是工作目錄。 *目錄*已**nvarchar(255)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
`[ @account = ] 'account' OUTPUT` 是[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 使用者帳戶。 *帳戶*已**nvarchar(255)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
`[ @min_distretention = ] _min_distretentionOUTPUT` 是最短散發保留期限，以小時為單位。 *min_distretention*已**int**，預設值是 **-1**。  
  
`[ @max_distretention = ] _max_distretentionOUTPUT` 是最長散發保留期限，以小時為單位。 *max_distretention*已**int**，預設值是 **-1**。  
  
`[ @history_retention = ] _history_retentionOUTPUT` 是記錄保留期限，以小時為單位。 *history_retention*已**int**，預設值是 **-1**。  
  
`[ @history_cleanupagent = ] 'history_cleanupagent' OUTPUT` 是記錄清除代理程式的名稱。 *history_cleanupagent*已**nvarchar(100)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
`[ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT` 是散發清除代理程式的名稱。 *distrib_cleanupagent*已**nvarchar(100)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
`[ @publisher = ] 'publisher'` 是 「 發行者 」 的名稱。 *發行者*已**sysname**，預設值是 NULL。  
  
`[ @local = ] 'local'` 是是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]應該取得本機伺服器值。 *本機*已**nvarchar(5)**，預設值是 NULL。  
  
`[ @rpcsrvname = ] 'rpcsrvname' OUTPUT` 是發出遠端程序呼叫的伺服器名稱。 *rpcsrvname*已**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
`[ @publisher_type = ] 'publisher_type' OUTPUT` 是 「 發行者 」 端的發行者類型。 *publisher_type*已**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**distributor**|**sysname**|散發者的名稱。|  
|**散發資料庫**|**sysname**|散發資料庫的名稱。|  
|**directory**|**nvarchar(255)**|工作目錄的名稱。|  
|**account**|**nvarchar(255)**|Windows 使用者帳戶的名稱。|  
|**最小發佈保留**|**int**|最小散發保留期限。|  
|**最大發佈保留**|**int**|最大散發保留期限。|  
|**記錄保留**|**int**|記錄保留期限。|  
|**記錄清除代理程式**|**nvarchar(100)**|記錄清除代理程式的名稱。|  
|**散發清除代理程式**|**nvarchar(100)**|散發清除代理程式的名稱。|  
|**rpc 伺服器名稱**|**sysname**|遠端或本機散發者的名稱。|  
|**rpc login name**|**sysname**|對遠端散發者的遠端程序呼叫所用的登入。|  
|**發行者類型**|**sysname**|發行者的類型；它可以是下列項目之一：<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE GATEWAY**|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdistributor**用於所有類型的複寫。  
  
 如果執行時，會指定一或多個輸出參數**sp_helpdistributor**，設為 NULL 的所有輸出參數會都指定結束值，並不傳回任何結果集。 如果未指定任何輸出參數，就會傳回結果集。  
  
## <a name="permissions"></a>Permissions  
 下列結果集資料行或輸出參數傳回的成員**sysadmin**固定的伺服器角色，在發行者端和有**db_owner**發行集資料庫的固定的資料庫角色：  
  
|結果集資料行|輸出參數|  
|-----------------------|----------------------|  
|account|**@account**|  
|min distrib retention|**@min_distretention**|  
|max distrib retention|**@max_distretention**|  
|history retention|**@history_retention**|  
|history cleanup agent|**@history_cleanupagent**|  
|distribution cleanup agent|**@distrib_cleanupagent**|  
|rpc login name|無|  
  
 下列結果集資料行會傳回給在散發者端的發行集之發行集存取清單中的使用者：  
  
-   directory  
  
 下列結果集資料行會傳回給所有使用者。  
  
|結果集資料行|輸出參數|  
|-----------------------|----------------------|  
|distributor|**@distributor**|  
|distribution database|**@distribdb**|  
|rpc server name|**@rpcsrvname**|  
|publisher type|**@publisher_type**|  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
