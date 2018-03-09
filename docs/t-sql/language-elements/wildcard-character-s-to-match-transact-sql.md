---
title: "[] （萬用字元-相符的字元） (TRANSACT-SQL) |Microsoft 文件"
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 04fcf0d9e76db380430bfbf4c4ed6e5fadf14afb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[\] （萬用字元-相符的個字元） (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  符合指定的範圍或指定括號之間集內的任何單一字元`[ ]`。 這些萬用字元可用於模式比對，例如牽涉到的字串比較`LIKE`和`PATINDEX`。  
  
## <a name="examples"></a>範例  
### <a name="a-simple-example"></a>答： 簡單的範例   
下列範例會傳回名稱開頭為字母`m`。 `[n-z]`指定第二個字母必須是某處，範圍從`n`至`z`。 百分比萬用字元`%`允許開頭為 3 個字元的任何或任何字元。 `model`和`msdb`資料庫符合此準則。 `master`資料庫並不會與結果集。
 
```sql
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
  
```sql  
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
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%&#40;萬用字元-字元 &#40; s &#41;若要比對 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93;&#40;萬用字元-字元 &#40; s &#41;不到相符項目 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_&#40;萬用字元-符合一個字元 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
