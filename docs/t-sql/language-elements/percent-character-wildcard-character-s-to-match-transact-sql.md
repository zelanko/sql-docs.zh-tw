---
description: 百分比字元 (萬用字元 - 相符的字元) (Transact-SQL)
title: 萬用字元搜尋 (%)
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 3b9a47ebd388c5720a8016763d36eac3b913ce14
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92191104"
---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>百分比字元 (萬用字元 - 相符的字元) (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  符合任何包含零或多個字元的字串。 這個萬用字元可做為前置詞或後置詞使用。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `Person` 的 `AdventureWorks2012` 資料表中，所有以 `Dan` 開頭的人員名字。  
  
```syntaxsql  
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
    
  
