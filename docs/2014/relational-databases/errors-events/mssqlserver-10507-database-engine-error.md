---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: dc1510ff82b619ef4462be95b592ca89133eecdb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133949"
---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10507|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_STMT_DOES_NOT_MATCH|  
|訊息文字|無法建立計畫指南 ' %。\*ls' 所指定的陳述式因為`@stmt`和`@module_or_batch`，或由`@plan_handle`和`@statement_start_offset`、 不符合所指定模組中的任何陳述式或批次。 請將值修改為與模組或批次中的陳述式相符。|  
  
## <a name="explanation"></a>說明  
 指定之模組或批次中的陳述式無法與指定的陳述式或陳述式位移值相符。  
  
## <a name="user-action"></a>使用者動作  
 請將指定的參數值修改為與模組或批次中的陳述式相符。  
  
## <a name="see-also"></a>另請參閱  
 [計畫指南](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
