---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7169ed83c3f602a17994e023d1da8ba5c17f94b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver10519"></a>MSSQLSERVER_10519
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10519|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為無法將 **@hints** 中指定的提示套用至 **@stmt** 或 **@statement_start_offset** 指定的陳述式。 請確認提示能否套用至陳述式。|  
  
## <a name="explanation"></a>說明  
無法將 **@hints** 中指定的提示套用至 **@stmt** 或 **@statement_start_offset** 指定的陳述式。  
  
## <a name="user-action"></a>使用者動作  
請指定能夠套用至陳述式的提示。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
