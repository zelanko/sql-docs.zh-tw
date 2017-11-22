---
title: "百分比字元 （萬用字元-相符的字元） (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Data Warehouse
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs: TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c75d2707cb09a85de67c0b7f9b5d337e6468b4d3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>百分比字元 (萬用字元 - 相符的字元) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  符合任何包含零或多個字元的字串。 這個萬用字元可做為前置詞或後置詞使用。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `Person` 的 `AdventureWorks2012` 資料表中，所有以 `Dan` 開頭的人員名字。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91;&#93;（萬用字元-相符的字元）](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91; ^ &#93;（萬用字元-不相符的字元）](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (萬用字元 - 符合一個字元)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
