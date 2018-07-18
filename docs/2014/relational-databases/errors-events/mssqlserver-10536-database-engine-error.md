---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00ca6874fc2b46c1b01495c5c7a0808265b0dd77
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428947"
---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10536|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_TOO_MANY_STMTS|  
|訊息文字|無法建立計畫指南 ' %。\*ls' 因為批次或對應到指定的模組`@plan_handle`包含超過 1000 個適合的陳述式。 請為批次或模組中的每個陳述式分別指定 `statement_start_offset` 值，以各建立一個計畫指南。|  
  
## <a name="explanation"></a>說明  
 指定的 `@plan_handle` 所對應的批次或模組中包含超過 1000 個適合的陳述式。  
  
## <a name="user-action"></a>使用者動作  
 請為批次或模組中的每個陳述式分別指定 `statement_start_offset` 值，以各建立一個計畫指南。  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [計畫指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
