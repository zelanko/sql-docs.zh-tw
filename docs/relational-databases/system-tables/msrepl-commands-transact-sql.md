---
title: MSrepl_commands (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7eec90fb29378f4cea3530093f2b505b87593fd8
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102396"
---
# <a name="msreplcommands-transact-sql"></a>MSrepl_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_commands**資料表包含複寫的命令之資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|發行者資料庫的識別碼。|  
|**xact_seqno**|**varbinary(16)**|交易序號。|  
|**type**|**int**|命令類型。|  
|**article_id**|**int**|發行項的識別碼。|  
|**originator_id**|**int**|發起者的識別碼。|  
|**command_id**|**int**|命令的識別碼。|  
|**部分指令**|**bit**|指出這是否為部分命令。|  
|命令|**varbinary(1024)**|命令值。|  
|**hashkey**|**int**|僅供內部使用。|  
|**originator_lsn**|**varbinary(16)**|識別原始發行集中，該命令的 LSN。 用於點對點異動複寫中。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
