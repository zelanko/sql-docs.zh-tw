---
title: "（萬用字元-相符的字元）(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/06/2016
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
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18688c96cd0369905844d79a1a109f4e5032bce3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="wildcard---characters-to-match-transact-sql"></a>（萬用字元-相符的字元）(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  符合指定的範圍或指定括號之間集內的任何單一字元`[ ]`。 這些萬用字元可用於模式比對，例如牽涉到的字串比較`LIKE`和`PATINDEX`。  
  
## <a name="examples"></a>範例  
### <a name="a-simple-example"></a>答： 簡單的範例   
下列範例會傳回名稱開頭為字母`m`。 `[n-z]`指定第二個字母必須是某處，範圍從`n`至`z`。 百分比萬用字元`%`允許開頭為 3 個字元的任何或任何字元。 `model`和`msdb`資料庫符合此準則。 `master`資料庫並不會與結果集。
 
```tsql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 您可能需要安裝其他符合資格的資料庫。


### <a name="b-more-complex-example"></a>B： 更複雜的範例   
 下列範例會利用 [] 運算子，來尋找地址有四位數郵遞區號之所有 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 員工的識別碼和名稱。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
 以下為結果集：  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  



  
## <a name="see-also"></a>另請參閱  
 [像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%（萬用字元-相符的字元）](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93;（萬用字元-不相符的字元）](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ （萬用字元-符合一個字元）](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  

