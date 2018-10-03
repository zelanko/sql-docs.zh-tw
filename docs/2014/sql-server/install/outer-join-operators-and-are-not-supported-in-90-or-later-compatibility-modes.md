---
title: 外部聯結運算子 *= 和 =* 90 或之後的相容性模式中不支援 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- =* join
- '*= join'
- joins [SQL Server]
ms.assetid: ca4aa11f-1048-411f-9c6c-3d0a8e319f2f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc4cab3fac4a49535b2178332b6e355ed95647b7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064898"
---
# <a name="outer-join-operators--and--are-not-supported-in-90-or-later-compatibility-modes"></a>在 90 (含) 之後的相容性模式中不支援外部聯結運算 *= 和 =*
  Upgrade Advisor 偵測到使用外部聯結運算子 * = 和 =\*。 在 90 或之後的相容性模式中並不支援這些運算子。 當您升級時，使用者資料庫會維持其相容性模式。 使用這些運算子的陳述式將會失敗。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 變更為 90 或之後時，資料庫相容性模式之前，請修改陳述式使用外部聯結運算子 * = 和 =\*使用對等的 OUTER JOIN 關鍵字。 下列範例會顯示使用 `*=` 運算子的查詢以及使用 `LEFT OUTER JOIN` 關鍵字的對等查詢。  
  
```  
-- This query uses an old-style outer join operator.  
USE pubs  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee, jobs   
WHERE employee.job_id *= jobs.job_id  
ORDER BY employee.job_id  
  
-- This query uses the ANSI standard keywords LEFT OUTER JOIN.  
USE pubs;  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
ORDER BY employee.job_id  
```  
  
 如需有關外部聯結的詳細資訊，請參閱《SQL Server 線上叢書》中的＜使用外部聯結＞。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
