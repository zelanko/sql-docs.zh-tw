---
title: ORDER BY 子句中的資料行別名前置詞不可以是資料表別名 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], columns
ms.assetid: fee7328f-6e8d-4005-930b-56fb6f17e0b2
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb0c12c4112383599b3f6ec67c7a097563a5944c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210708"
---
# <a name="column-aliases-in-order-by-clause-cannot-be-prefixed-by-table-alias"></a>ORDER BY 子句中資料行別名的前置詞不可以是資料表別名
  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本中，ORDER BY 子句中資料行別名的前置詞不可以是資料表別名。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 例如，下列查詢可在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中執行，但在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中則會傳回錯誤：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.l  
```  
  
 [!INCLUDE[ssDEversion10](../../includes/ssdeversion10-md.md)] 不會將 `p.l` 子句中的 `ORDER BY` 比對成資料表中的有效資料行。  
  
### <a name="exception"></a>例外狀況  
 如果在 ORDER BY 子句中指定的前置資料行別名是指定資料表中的有效資料行名稱，則查詢會在無錯誤的情況下執行。但是，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，陳述式的語意可能不同。 例如，在下列陳述式中指定的資料行別名 (`id`) 是 `sysobjects` 資料表中的有效資料行名稱。 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，當該陳述式執行時，`CAST` 作業會在排序結果集之後執行。 這表示 `name` 資料行會用於排序作業中。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，`CAST` 作業會在排序作業之前進行。 這表示 `id` 資料行會用於排序作業中，並以非預期的順序傳回結果集。  
  
```  
SELECT CAST (o.name AS char(128)) AS id  
FROM sysobjects AS o  
ORDER BY o.id;  
```  
  
## <a name="corrective-action"></a>更正動作  
 請使用下列其中一種方式，修改在 ORDER BY 子句中使用以資料表別名當做前置詞之資料行別名的查詢：  
  
-   請盡量不要為 ORDER BY 子句中的資料行別名加上前置詞。  
  
-   使用資料行名稱物來取代資料行別名。  
  
 例如，在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，下列兩個查詢會在無錯誤的情況下執行：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY l  
  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.LastName  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
