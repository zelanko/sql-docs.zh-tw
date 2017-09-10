---
title: "選取@local_variable(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: 1c136514f12749e9eac28bf4b4512acf3e8aaee1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="select-localvariable-transact-sql"></a>選取@local_variable(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將本機變數設定為運算式的值。  
  
 對於指派變數，我們建議您改用[設定@local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)來取代 SELECT @*local_variable*。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>引數  
@*local_variable*  
 這是將指派值的宣告變數。  
  
{= | += | -= | \*= | /= | %= | &= | ^= | |= }   
將右邊的值指派給左邊的變數。  
  
複合指派運算子：  
  |! 運算子之後 |action |   
  |-----|-----|  
  | = | 指派給變數的運算式，如下所示。 |  
  | += | 新增並指派 |   
  | -= | 減去並指派 |  
  | \*= | 乘號和指派 |  
  | /= | 除以並指派 |  
  | %= | 模數指派 |  
  | &= | 位元 AND 並指派 |  
  | ^= | 位元 XOR 並指派 |  
  | \|= | 位元 OR 並指派 |  
  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 其中包括純量子查詢。  
  
## <a name="remarks"></a>備註  
 SELECT @*local_variable*通常用來傳回單一值到變數。 不過，當*運算式*名稱資料行，它可以傳回多個值。 如果 SELECT 陳述式傳回多個值，就會將最後傳回的值指派給變數。  
  
 如果 SELECT 陳述式未傳回任何資料列，變數會保留它目前的值。 如果*運算式*是純量子查詢的傳回任何值，將變數設為 NULL。  
  
 一個 SELECT 陳述式可以初始化多個本機變數。  
  
> [!NOTE]  
>  您不能也利用包含變數指派的 SELECT 陳述式來執行一般結果集擷取作業。  
  
## <a name="examples"></a>範例  
  
### <a name="a-use-select-localvariable-to-return-a-single-value"></a>A. 使用 SELECT@local_variable傳回單一值  
 在下列範例中，`@var1` 變數指派了 `Generic Name` 來作為值。 針對 `Store` 資料表的查詢不會傳回任何資料列，因為資料表中並沒有指定給 `CustomerID` 的值。 變數會保留 `Generic Name` 值。  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-localvariable-to-return-null"></a>B. 使用 SELECT@local_variable以傳回 null  
 在下列範例中，利用子查詢來將值指派給 `@var1`。 由於針對 `CustomerID` 所要求的值並不存在，因此，子查詢不會傳回任何值，變數會設為 `NULL`。  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>另請參閱  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

