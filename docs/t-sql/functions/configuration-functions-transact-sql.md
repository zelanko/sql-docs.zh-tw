---
title: "組態函數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
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
- functions [SQL Server], configuration
- configuration options [SQL Server], functions
- current configuration information
- configuration functions [SQL Server]
ms.assetid: 066f15e7-3406-437e-93c4-3f247c529169
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 56bab03c9e25db7e425a0bbb4416b47f1d39b4a9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="configuration-functions-transact-sql"></a>組態函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

下列純量函數會傳回目前組態選項設定的相關資訊：
  
|||  
|-|-|  
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|[@@OPTIONS](../../t-sql/functions/options-transact-sql.md)|  
|[@@DBTS](../../t-sql/functions/dbts-transact-sql.md)|[@@REMSERVER](../../t-sql/functions/remserver-transact-sql.md)|  
|[@@LANGID](../../t-sql/functions/langid-transact-sql.md)|[@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|[@@SERVICENAME](../../t-sql/functions/servicename-transact-sql.md)|  
|[@@LOCK_TIMEOUT](../../t-sql/functions/lock-timeout-transact-sql.md)|[@@SPID](../../t-sql/functions/spid-transact-sql.md)|  
|[@@MAX_CONNECTIONS](../../t-sql/functions/max-connections-transact-sql.md)|[@@TEXTSIZE](../../t-sql/functions/textsize-transact-sql.md)|  
|[@@MAX_PRECISION](../../t-sql/functions/max-precision-transact-sql.md)|[@@VERSION](../../t-sql/functions/version-transact-sql-configuration-functions.md)|  
|[@@NESTLEVEL](../../t-sql/functions/nestlevel-transact-sql.md)||  
  
所有組態函數都不具決定性。 這表示這些函數並非每次呼叫時，都會傳回相同的結果，即便使用同一組輸入值也是如此。 如需函數決定論的詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="see-also"></a>另請參閱
[函式 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/functions.md)
  
  
