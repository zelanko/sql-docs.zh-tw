---
title: "_ （萬用字元-符合一個字元） (TRANSACT-SQL) |Microsoft 文件"
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
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e47fdb9e12a632323971558d2e894fb7b181498e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (萬用字元 - 符合單一字元) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用底線字元`_`要比對任何單一字元，例如包含模式比對的字串比較作業中`LIKE`和`PATINDEX`。  
  
## <a name="examples"></a>範例  

## <a name="a-simple-example"></a>答： 簡單的範例   

下列範例會傳回所有資料庫名稱以字母為開頭的`m`，而且有字母`d`為第三個字母。 底線字元指定名稱的第二個字元可以是任何字母。 `model`和`msdb`資料庫符合此準則。 `master`資料庫並不會。

```tsql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
您可能必須符合此條件的其他資料庫。

您可以使用多個底線來表示多個字元。 變更`LIKE`準則，以包含兩個底線`'m__%`在結果中包含 master 資料庫。

### <a name="b-more-complex-example"></a>B： 更複雜的範例
 下列範例會利用 `_` 運算子來尋找在 `Person` 資料表中，所有名字都是三個字母且結尾是 `an` 的人員。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C： 逸出底線字元   
下列範例會傳回類似的固定的資料庫角色的名稱`db_owner`和`db_ddladmin`，但它也會傳回`dbo`使用者。 

```tsql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

中的第三個的字元位置底線會被視為萬用字元，加上字母為開頭的主體不會篩選`db_`。 要逸出底線將它括在方括號`[_]`。 

```tsql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
現在`dbo`排除使用者。   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>另請參閱  
 [像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%（萬用字元-相符的字元）](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91;&#93;（萬用字元-相符的字元）](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93;（萬用字元-不相符的字元）](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
  

