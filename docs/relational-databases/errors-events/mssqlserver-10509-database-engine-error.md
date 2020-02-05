---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0cdf2c06311e703b6a07667ba41d1c853c17eb86
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "72305893"
---
# <a name="mssqlserver_10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10509|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_INVALID_STMT|  
|訊息文字|無法建立計劃指南 '%.\*ls'，因為 **\@stmt** 或 **\@statement_start_offset** 所指定的陳述式中含有語法錯誤或不符計劃指南使用資格。 請提供單一有效 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，或批次中陳述式的有效開始位置。 若要取得有效開始位置，請查詢 sys.dm_exec_query_stats 動態管理函數中的 statement_start_offset 資料行。|  
  
## <a name="explanation"></a>說明  
**\@stmt** 或 **\@statement_start_offset** 所指定的陳述式中含有語法錯誤或不符計劃指南使用資格。  
  
## <a name="user-action"></a>使用者動作  
請提供單一有效 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，或批次中陳述式的有效開始位置。 若要取得有效開始位置，請查詢 sys.dm_exec_query_stats 動態管理函數中的 statement_start_offset 資料行。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
