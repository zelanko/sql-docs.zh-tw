---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0943ae13586a5ceefe2a6ec7e07b7cb498a1b525
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10507|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_STMT_DOES_NOT_MATCH|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為 **@stmt** 和 **@module_or_batch** 或是 **@plan_handle** 和 **@statement_start_offset** 所指定的陳述式不符合指定的模組或批次中的任何陳述式。 請將值修改為與模組或批次中的陳述式相符。|  
  
## <a name="explanation"></a>說明  
指定之模組或批次中的陳述式無法與指定的陳述式或陳述式位移值相符。  
  
## <a name="user-action"></a>使用者動作  
請將指定的參數值修改為與模組或批次中的陳述式相符。  
  
## <a name="see-also"></a>另請參閱  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

