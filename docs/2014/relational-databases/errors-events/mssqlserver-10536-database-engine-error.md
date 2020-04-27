---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5ddb4df0089b488d3a15c76a76abef8be154848
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870521"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10536|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_TOO_MANY_STMTS|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為指定的 `@plan_handle` 所對應的批次或模組中包含超過 1000 個適合的陳述式。 請為批次或模組中的每個陳述式分別指定 `statement_start_offset` 值，以各建立一個計畫指南。|  
  
## <a name="explanation"></a>說明  
 指定的 `@plan_handle` 所對應的批次或模組中包含超過 1000 個適合的陳述式。  
  
## <a name="user-action"></a>使用者動作  
 請為批次或模組中的每個陳述式分別指定 `statement_start_offset` 值，以各建立一個計畫指南。  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [計劃指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
