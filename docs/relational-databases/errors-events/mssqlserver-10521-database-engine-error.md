---
title: MSSQLSERVER_10521 | Microsoft Docs
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
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e6060201dd4211266a0dcbf874826f6c8ef18d70
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10521"></a>MSSQLSERVER_10521
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10521|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_PARAM_NEEDED|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為已將 **@type** 指定為 '%ls'，而且參數 '%ls' 為 NULL， 但這種類型要求參數必須為非 NULL 值。 請為參數指定非 NULL 值，或將參數類型變更為允許 NULL 值的類型。|  
  
## <a name="explanation"></a>說明  
在 **@type** 中指定的類型要求指定的參數必須為非 NULL 值，但是卻提供了 NULL 值。  
  
## <a name="user-action"></a>使用者動作  
請為參數指定非 NULL 值，或將參數類型變更為允許 NULL 值的類型。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

