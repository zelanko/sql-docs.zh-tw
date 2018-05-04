---
title: sp_helpdistributor (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords:
- sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 641dd06193b6897a703067f24ce7aa5392abe929
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出散發者、 散發資料庫、 工作目錄的相關資訊和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用者帳戶。 這個預存程序執行於發行集資料庫或任何資料庫的發行者端。  
  
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
 [  **@distributor=**] **'***散發者***'** 輸出  
 這是散發者的名稱。 散發者是**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
 [  **@distribdb=**] **'***distribdb***'** 輸出  
 這是散發資料庫的名稱。 *distribdb*是**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
 [  **@directory=**] **'***目錄***'** 輸出  
 這是工作目錄。 *目錄*是**nvarchar （255)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
 [  **@account=**] **'***帳戶***' 輸出**  
 這是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶。 *帳戶*是**nvarchar （255)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
 [  **@min_distretention=**] *min_distretention * * * 輸出**  
 這是最小散發保留期限 (以小時為單位)。 *min_distretention*是**int**，預設值是 **-1**。  
  
 [  **@max_distretention=**] *max_distretention * * * 輸出**  
 這是最大散發保留期限 (以小時為單位)。 *max_distretention*是**int**，預設值是 **-1**。  
  
 [  **@history_retention=**] *history_retention * * * 輸出**  
 這是記錄保留期限 (以小時為單位)。 *history_retention*是**int**，預設值是 **-1**。  
  
 [  **@history_cleanupagent=**] **'***history_cleanupagent***' 輸出**  
 這是記錄清除代理程式的名稱。 *history_cleanupagent*是**nvarchar （100)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
 [  **@distrib_cleanupagent =**] **'***distrib_cleanupagent***' 輸出**  
 這是散發清除代理程式的名稱。 *distrib_cleanupagent*是**nvarchar （100)**，預設值是**%**，這是唯一會傳回結果集的值。  
  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者的名稱。 *發行者*是**sysname**，預設值是 NULL。  
  
 [  **@local=**] **'***本機***'**  
 這是指 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否應該取得本機伺服器值。 *本機*是**nvarchar （5)**，預設值是 NULL。  
  
 [  **@rpcsrvname=**] **'***rpcsrvname***' 輸出**  
 這是發出遠端程序呼叫的伺服器名稱。 *rpcsrvname*是**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
 [ **@publisher_type**=] **'***publisher_type***' 輸出**  
 這是發行者的發行者類型。 *publisher_type*是**sysname**，預設值是**%**，這是唯一會傳回結果集的值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**散發者**|**sysname**|散發者的名稱。|  
|**散發資料庫**|**sysname**|散發資料庫的名稱。|  
|**目錄**|**nvarchar(255)**|工作目錄的名稱。|  
|**帳戶**|**nvarchar(255)**|Windows 使用者帳戶的名稱。|  
|**min 分散保留**|**int**|最小散發保留期限。|  
|**最大分散保留**|**int**|最大散發保留期限。|  
|**記錄保留**|**int**|記錄保留期限。|  
|**記錄清除代理程式**|**nvarchar(100)**|記錄清除代理程式的名稱。|  
|**散發清除代理程式**|**nvarchar(100)**|散發清除代理程式的名稱。|  
|**rpc 伺服器名稱**|**sysname**|遠端或本機散發者的名稱。|  
|**rpc 登入名稱**|**sysname**|對遠端散發者的遠端程序呼叫所用的登入。|  
|**發行者類型**|**sysname**|發行者的類型；它可以是下列項目之一：<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE GATEWAY**|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdistributor**用於所有複寫類型。  
  
 如果執行時，會指定一或多個輸出參數**sp_helpdistributor**，設為 NULL 的所有輸出參數會都指定結束值，並不傳回任何結果集。 如果未指定任何輸出參數，就會傳回結果集。  
  
## <a name="permissions"></a>Permissions  
 下列結果集資料行或輸出參數會傳回成員的**sysadmin**固定的伺服器角色，在 「 發行者 」 和**db_owner**發行集資料庫上的固定的資料庫角色：  
  
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
 [sp_adddistpublisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
