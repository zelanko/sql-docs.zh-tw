---
title: 百分比字元 (萬用字元 - 相符的字元) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 64eb6442b20d6e8aa15619ae572bb406acde6768
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65980448"
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
  
## <a name="see-also"></a>另請參閱  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91; &#93; (萬用字元 - 要比對的字元)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91;^&#93; (萬用字元 - 不相符的字元)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (萬用字元 - 符合一個字元)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
