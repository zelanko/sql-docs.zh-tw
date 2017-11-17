---
title: "中斷 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BREAK
- BREAK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- exiting innermost loop [SQL Server]
- END keyword
- ignored statements
- BREAK keyword
ms.assetid: 67c30b8d-3f15-41ad-b9a9-a4ced3b2af9f
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ac7f12956aa0f8e2919aa33cf3d3cd8df140b96
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="break-transact-sql"></a>BREAK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  結束 WHILE 陳述式或 WHILE 迴圈內部 IF ELSE 陳述式中最內層的迴圈。 在 END 關鍵字後面出現的任何陳述式 (表示迴圈結束) 都會執行。 BREAK 經常是由 IF 測試來啟動，但並非一律如此。  
  
## <a name="examples"></a>範例  
  
```  
-- Uses AdventureWorks  
  
WHILE ((SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300)  
BEGIN  
    UPDATE DimProduct  
        SET ListPrice = ListPrice * 2;  
     IF ((SELECT MAX(ListPrice) FROM dbo.DimProduct) > $500)  
         BREAK;  
END  
```  
  
## <a name="see-also"></a>另請參閱  
 [流程控制語言 &#40;TRANSACT-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [雖然 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  



