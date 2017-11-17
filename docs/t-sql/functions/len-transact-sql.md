---
title: "LEN (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/03/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LEN
- LEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 532b996c23a8f9746a52434d78783da2a24d1add
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定字串運算式的字元數，但尾端空白不算。  
  
> [!NOTE]  
>  若要傳回用來表示運算式的位元組數目，請使用[DATALENGTH](../../t-sql/functions/datalength-transact-sql.md)函式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>引數  
 *string_expression*  
 是字串[運算式](../../t-sql/language-elements/expressions-transact-sql.md)進行評估。 *string_expression*可以是常數、 變數或資料行的字元或二進位資料。  
  
## <a name="return-types"></a>傳回類型  
 **bigint**如果*運算式*屬於**varchar （max)**， **nvarchar （max)**或**varbinary （max)**資料型別。否則， **int**。  
  
 如果您使用 SC 定序，傳回的整數值也將 UTF-16 Surrogate 字組視為單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="remarks"></a>備註  
 LEN 不包括尾端空白。 如果是問題，請考慮使用[DATALENGTH &#40;TRANSACT-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)函式不會修剪的字串。 如果在處理 unicode 字串，DATALENGTH 會傳回兩次的字元數。 下列範例會示範 LEN 和 DATALENGTH 尾端的空格。  
  
```  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
  
```  
  
## <a name="examples"></a>範例  
 下列範例會選取 `FirstName` 居民的 `Australia` 字元數和資料。 這個範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回資料行中的字元數`FirstName`和員工的名字和姓氏名稱位於`Australia`。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [DATALENGTH &#40;TRANSACT-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [左 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/left-transact-sql.md)   
 [權限 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/right-transact-sql.md)  
  
  



