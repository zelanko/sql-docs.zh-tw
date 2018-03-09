---
title: "重新執行追蹤 (SQL Server Profiler) 的考量 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
caps.latest.revision: "21"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 076b34d06f7644b471dd16694c293baafdb3a8bc
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>重新執行追蹤的考量 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]無法重新執行追蹤下列幾種：  
  
-   包含異動複寫與其他交易記錄活動的追蹤。 略過這些事件。 其他類型的複寫不會標示交易記錄，因此不受影響。  
  
-   包含了涉及全域唯一識別碼 (GUID) 作業的追蹤。 將略過這些事件。  
  
-   包含涉及 **bcp**公用程式、BULK INSERT、READTEXT、WRITETEXT 和 UPDATETEXT 陳述式之 **text**、 **ntext** 和 **image** 資料行上作業的追蹤，以及包含全文檢索作業的追蹤。 略過這些事件。  
  
-   包含工作階段繫結： **sp_getbindtoken** 和 **sp_bindsession** 系統預存程序的追蹤。 略過這些事件。  
  
> [!NOTE]  
>  如果您沒有使用預先設定的重新執行範本 (**TSQL_Replay**)，也沒有擷取所有必要的資料，則 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 不會重新執行追蹤。 如需詳細資訊，請參閱 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
 如需有關重做追蹤時所需之權限的詳細資訊，請參閱＜ [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [SQL Server 事件類別參考](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [READTEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [WRITETEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [UPDATETEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
