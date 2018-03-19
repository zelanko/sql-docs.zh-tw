---
title: "系統統計函式 (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statistical functions [SQL Server]
- system statistical functions [SQL Server]
- functions [SQL Server], statistical
ms.assetid: 45828c67-1b9a-4653-bb24-86246084d8ba
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c5b437038aa63c4e0ae1a5d5f0a8ef2b435cde66
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="system-statistical-functions-transact-sql"></a>系統統計函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列純量函數會傳回系統的統計資訊：  
  
|||  
|-|-|  
|[@@CONNECTIONS](../../t-sql/functions/connections-transact-sql.md)|[@@PACK_RECEIVED](../../t-sql/functions/pack-received-transact-sql.md)|  
|[@@CPU_BUSY](../../t-sql/functions/cpu-busy-transact-sql.md)|[@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)|  
|[fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)|[@@TIMETICKS](../../t-sql/functions/timeticks-transact-sql.md)|  
|[@@IDLE](../../t-sql/functions/idle-transact-sql.md)|[@@TOTAL_ERRORS](../../t-sql/functions/total-errors-transact-sql.md)|  
|[@@IO_BUSY](../../t-sql/functions/io-busy-transact-sql.md)|[@@TOTAL_READ](../../t-sql/functions/total-read-transact-sql.md)|  
|[@@PACKET_ERRORS](../../t-sql/functions/packet-errors-transact-sql.md)|[@@TOTAL_WRITE](../../t-sql/functions/total-write-transact-sql.md)|  
  
 所有系統統計函數都不具決定性。 這表示這些函數並非每次呼叫時，都會傳回相同的結果，即便使用同一組輸入值也是如此。 如需函式確定性的詳細資訊，請參閱[確定性與非確定性函式](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
