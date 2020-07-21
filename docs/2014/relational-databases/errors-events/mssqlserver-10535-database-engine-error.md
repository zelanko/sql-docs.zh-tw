---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 68070291c5e7f50d423b74338dc1f6baeb9c6dfa
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554113"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10535|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_NO_PLAN|  
|訊息文字|無法建立計畫指南 '%.*ls'，因為在計畫快取中找不到指定計畫控制代碼的對應計畫。 請指定快取的計畫控制代碼。 如需快取的計畫控制代碼清單，請查詢 sys.dm_exec_query_stats 動態管理檢視。|  
  
## <a name="explanation"></a>說明  
 在計畫快取中找不到指定計畫控制代碼的對應計畫。  
  
## <a name="user-action"></a>使用者動作  
 請指定快取的計畫控制代碼。 如需快取的計畫控制代碼清單，請查詢 sys.dm_exec_query_stats 動態管理檢視。  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide_from_handle &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
