---
title: sp_helpdistributor (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 0681e82f9e36fd2a2f66bb8b7d3faa2f07a72f13
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770937"
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  列出散發者、散發資料庫、工作目錄和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用者帳戶的相關資訊。 這個預存程序執行於發行集資料庫或任何資料庫的發行者端。  
  
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
`[ @distributor = ] 'distributor' OUTPUT`這是散發者的名稱。 散發者是**sysname**, 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
`[ @distribdb = ] 'distribdb' OUTPUT`這是散發資料庫的名稱。 *distribdb*是**sysname**, 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
`[ @directory = ] 'directory' OUTPUT`是工作目錄。 *目錄*是**Nvarchar (255)** , 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
`[ @account = ] 'account' OUTPUT`[!INCLUDE[msCoName](../../includes/msconame-md.md)]是 Windows 使用者帳戶。 *帳戶*是**Nvarchar (255)** , 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
`[ @min_distretention = ] _min_distretentionOUTPUT`這是最小散發保留期限 (以小時為單位)。 *min_distretention*是**int**, 預設值是 **-1**。  
  
`[ @max_distretention = ] _max_distretentionOUTPUT`這是最大散發保留期限 (以小時為單位)。 *max_distretention*是**int**, 預設值是 **-1**。  
  
`[ @history_retention = ] _history_retentionOUTPUT`這是記錄保留期限 (以小時為單位)。 *history_retention*是**int**, 預設值是 **-1**。  
  
`[ @history_cleanupagent = ] 'history_cleanupagent' OUTPUT`這是記錄清除代理程式的名稱。 *history_cleanupagent*是**Nvarchar (100)** , 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
`[ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT`這是散發清除代理程式的名稱。 *distrib_cleanupagent*是**Nvarchar (100)** , 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**, 預設值是 Null。  
  
`[ @local = ] 'local'`這是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指是否應該取得本機伺服器值。 *local*是**Nvarchar (5)** , 預設值是 Null。  
  
`[ @rpcsrvname = ] 'rpcsrvname' OUTPUT`這是發出遠端程序呼叫的伺服器名稱。 *rpcsrvname*是**sysname**, 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
`[ @publisher_type = ] 'publisher_type' OUTPUT`這是發行者的發行者類型。 *publisher_type*是**sysname**, 預設 **%** 值是, 這是唯一會傳回結果集的值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**伺服器**|**sysname**|散發者的名稱。|  
|**散發資料庫**|**sysname**|散發資料庫的名稱。|  
|**directory**|**nvarchar(255)**|工作目錄的名稱。|  
|**account**|**nvarchar(255)**|Windows 使用者帳戶的名稱。|  
|**最低 distrib.exe 保留期**|**int**|最小散發保留期限。|  
|**最大 distrib.exe 保留期**|**int**|最大散發保留期限。|  
|**記錄保留期**|**int**|記錄保留期限。|  
|**歷程記錄清除代理程式**|**nvarchar(100)**|記錄清除代理程式的名稱。|  
|**散發清除代理程式**|**nvarchar(100)**|散發清除代理程式的名稱。|  
|**rpc 伺服器名稱**|**sysname**|遠端或本機散發者的名稱。|  
|**rpc 登入名稱**|**sysname**|對遠端散發者的遠端程序呼叫所用的登入。|  
|**發行者類型**|**sysname**|發行者的類型；它可以是下列項目之一：<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE 閘道**|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_helpdistributor**用於所有類型的複寫中。  
  
 如果在執行**sp_helpdistributor**時指定了一或多個輸出參數, 則所有設為 Null 的輸出參數都會在結束時指派值, 而且不會傳回任何結果集。 如果未指定任何輸出參數，就會傳回結果集。  
  
## <a name="permissions"></a>Permissions  
 下列結果集資料行或輸出參數會傳回給發行者端的**系統管理員 (sysadmin** ) 固定伺服器角色的成員, 以及發行集資料庫的**db_owner**固定資料庫角色:  
  
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
 [sp_adddistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
