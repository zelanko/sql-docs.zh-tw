---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2ff20cdde06a1ee100d711aeab2612f2ef4625f0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422417"
---
# <a name="mssqlserver10519"></a>MSSQLSERVER_10519
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10519|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|訊息文字|無法建立計畫指南 ' %。\*ls' 中指定的提示，因為`@hints`無法套用至指定的陳述式`@stmt`或`@statement_start_offset`。 請確認提示能否套用至陳述式。|  
  
## <a name="explanation"></a>說明  
 無法將 `@hints` 中指定的提示套用至 `@stmt` 或 `@statement_start_offset` 指定的陳述式。  
  
## <a name="user-action"></a>使用者動作  
 請指定能夠套用至陳述式的提示。  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [計畫指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
