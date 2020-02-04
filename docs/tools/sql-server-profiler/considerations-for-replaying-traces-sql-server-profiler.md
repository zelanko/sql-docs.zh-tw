---
title: 重新執行追蹤的考量
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.openlocfilehash: a8a4288d4810ca137d8e6397188ada0e69b945bd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307342"
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>重新執行追蹤的考量 (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 無法重新執行下列種類的追蹤：  
  
-   包含異動複寫與其他交易記錄活動的追蹤。 略過這些事件。 其他類型的複寫不會標示交易記錄，因此不受影響。  
  
-   包含了涉及全域唯一識別碼 (GUID) 作業的追蹤。 將略過這些事件。  
  
-   包含涉及 **bcp**公用程式、BULK INSERT、READTEXT、WRITETEXT 和 UPDATETEXT 陳述式之 **text**、 **ntext** 和 **image** 資料行上作業的追蹤，以及包含全文檢索作業的追蹤。 略過這些事件。  
  
-   包含工作階段繫結： **sp_getbindtoken** 和 **sp_bindsession** 系統預存程序的追蹤。 略過這些事件。  
  
> [!NOTE]  
>  如果您沒有使用預先設定的重新執行範本 (**TSQL_Replay**)，也沒有擷取所有必要的資料，則 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 不會重新執行追蹤。 如需詳細資訊，請參閱 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
 如需有關重做追蹤時所需之權限的詳細資訊，請參閱＜ [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [SQL Server 事件類別參考](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
