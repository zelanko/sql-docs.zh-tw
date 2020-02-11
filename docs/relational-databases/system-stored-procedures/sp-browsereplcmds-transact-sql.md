---
title: sp_browsereplcmds （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
ms.openlocfilehash: d049a5e96d9c7212467595aa70cd44db727bdf6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769002"
---
# <a name="sp_browsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  傳回散發資料庫所儲存的複寫命令之可讀取版本中的結果集，它用來作為一項診斷工具。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>引數  
`[ @xact_seqno_start = ] 'xact_seqno_start'`指定要傳回的最小值確切序號。 *xact_seqno_start*是**Nchar （22）**，預設值是值是0x00000000000000000000。  
  
`[ @xact_seqno_end = ] 'xact_seqno_end'`指定要傳回的確切最大序號。 *xact_seqno_end*是**Nchar （22）**，預設值是值是0xffffffffffffffffffff。  
  
`[ @originator_id = ] 'originator_id'`指定是否傳回具有指定之*originator_id*的命令。 *originator_id*是**int**，預設值是 Null。  
  
`[ @publisher_database_id = ] 'publisher_database_id'`指定是否傳回具有指定之*publisher_database_id*的命令。 *publisher_database_id*是**int**，預設值是 Null。  
  
`[ @article_id = ] 'article_id'`指定是否傳回具有指定之*article_id*的命令。 *article_id*是**int**，預設值是 Null。  
  
`[ @command_id = ] command_id`這是要解碼的[MSrepl_commands &#40;transact-sql&#41;](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)中的命令位置。 *command_id*是**int**，預設值是 Null。 如果指定，則必須同時指定所有其他參數，而且*xact_seqno_start*必須與*xact_seqno_end*相同。  
  
`[ @agent_id = ] agent_id`指定只傳回特定複寫代理程式的命令。 *agent_id*是**int**，預設值是 Null。  
  
`[ @compatibility_level = ] compatibility_level`這是*compatibility_level*為[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**的版本，預設值是9000000。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**Varbinary （16）**|命令的序號。|  
|**originator_srvname**|**sysname**|引發交易的伺服器。|  
|**originator_db**|**sysname**|引發交易的資料庫。|  
|**article_id**|**int**|發行項的識別碼。|  
|**type**|**int**|命令的類型。|  
|**partial_command**|**bit**|指出這是否為部分命令。|  
|**hashkey**|**int**|僅供內部使用。|  
|**originator_publication_id**|**int**|引發交易的發行集識別碼。|  
|**originator_db_version**|**int**|引發交易的資料庫版本。|  
|**originator_lsn**|**Varbinary （16）**|識別命令在原始發行集中的記錄序號 (LSN)。 用於點對點異動複寫中。|  
|**命令**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)]命令.|  
|**command_id**|**int**|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)中的命令識別碼。|  
  
 在結果集中，較長的命令可能會分成許多資料列。  
  
## <a name="remarks"></a>備註  
 **sp_browsereplcmds**用於異動複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，或是散發資料庫上之**db_owner**或**replmonitor**固定資料庫角色的成員，才能夠執行**sp_browsereplcmds**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
