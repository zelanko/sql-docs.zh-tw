---
title: "（萬用字元-不相符的字元）(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- wildcard
- '[^]_TSQL'
- '[^]'
- Not Match
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[^] (wildcard - character(s) not to match)'
ms.assetid: b970038f-f4e7-4a5d-96f6-51e3248c6aef
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96749cb88e4d98b112de2ce1eb9bff4c7e156e42
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="wildcard---characters-not-to-match-transact-sql"></a>（萬用字元-不相符的字元）(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  比對不在方括號指定範圍或集合內的任何單一字元。  
  
## <a name="examples"></a>範例  
 下列範例會利用 [^] 運算子來尋找 `Contact` 資料表中，所有名字的開頭都是 `Al`，而且名字第三個字母不是 `a` 的人。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%'  
ORDER BY FirstName;  
```  
  
## <a name="see-also"></a>另請參閱  
 [像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [%&#40;萬用字元-字元 &#40; s &#41;若要比對 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91;&#93;（萬用字元-相符的字元）](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [_ （萬用字元-符合一個字元）](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  

