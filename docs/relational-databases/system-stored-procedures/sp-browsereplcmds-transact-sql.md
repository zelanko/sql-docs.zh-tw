---
title: sp_browsereplcmds (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 19c4c3b162d882f3d7a31701ad2cc838fcaaed74
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32991295"
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@xact_seqno_start =**] **'***xact_seqno_start***'**  
 指定要傳回的最低值確實序號。 *xact_seqno_start*是**nchar （22)**，預設值是 0x00000000000000000000。  
  
 [  **@xact_seqno_end =**] **'***xact_seqno_end***'**  
 指定要傳回的最高確實序號。 *xact_seqno_end*是**nchar （22)**，預設值是 0xFFFFFFFFFFFFFFFFFFFF。  
  
 [  **@originator_id =**] **'***originator_id***'**  
 指定如果具有指定的命令*originator_id*會傳回。 *originator_id*是**int**，預設值是 NULL。  
  
 [  **@publisher_database_id =**] **'***publisher_database_id***'**  
 指定如果具有指定的命令*publisher_database_id*會傳回。 *publisher_database_id*是**int**，預設值是 NULL。  
  
 [  **@article_id =**] **'***article_id***'**  
 指定如果具有指定的命令*article_id*會傳回。 *article_id*是**int**，預設值是 NULL。  
  
 [  **@command_id =**] *command_id*  
 是中的命令位置[MSrepl_commands &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)要解碼。 *command_id*是**int**，預設值是 NULL。 如果指定，所有其他參數也必須指定，和*xact_seqno_start*必須與相同*xact_seqno_end*。  
  
 [  **@agent_id =**] *agent_id*  
 指定只傳回特定複寫代理程式的命令。 *agent_id*是**int**，預設值是 NULL。  
  
 [  **@compatibility_level =**] *compatibility_level*  
 版本[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所在*compatibility_level*是**int**，預設值是 9000000。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|命令的序號。|  
|**originator_srvname**|**sysname**|引發交易的伺服器。|  
|**originator_db**|**sysname**|引發交易的資料庫。|  
|**article_id**|**int**|發行項的識別碼。|  
|**type**|**int**|命令的類型。|  
|**部分指令**|**bit**|指出這是否為部分命令。|  
|**hashkey**|**int**|僅供內部使用。|  
|**originator_publication_id**|**int**|引發交易的發行集識別碼。|  
|**originator_db_version**|**int**|引發交易的資料庫版本。|  
|**originator_lsn**|**varbinary(16)**|識別命令在原始發行集中的記錄序號 (LSN)。 用於點對點異動複寫中。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。|  
|**command_id**|**int**|中的命令識別碼[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)。|  
  
 在結果集中，較長的命令可能會分成許多資料列。  
  
## <a name="remarks"></a>備註  
 **sp_browsereplcmds**用於異動複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色或成員的**db_owner**或**replmonitor**散發資料庫上的固定的資料庫角色可以執行**sp_browsereplcmds**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
