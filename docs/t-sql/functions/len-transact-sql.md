---
title: LEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c505d2a72e9ccd0432f685307e97b16e625e859b
ms.sourcegitcommit: e6c260a139326f5a400a57ece812d39ef8b820bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86032456"
---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

傳回指定字串運算式的字元數，但尾端空格不算。  
  
> [!NOTE]  
> 若要傳回用來表示運算式的位元組數目，請使用 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 函數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>引數  
 *string_expression*  
 這是要評估的字串[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 *string_expression* 可以是字元或二進位資料的常數、變數或資料行。  
  
## <a name="return-types"></a>傳回型別  
 若 **expression** 的資料類型為 *varchar(max)* 、**nvarchar(max)** 或 **varbinary(max)** ，則為 **bigint**，否則為 **int**。  
  
 如果您使用 SC 定序，傳回的整數值也將 UTF-16 Surrogate 字組視為單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="remarks"></a>備註  
LEN 會排除尾端空格。 如果這是個問題，請考慮使用不修剪字串的 [DATALENGTH &#40;Transact-SQL&#41; ](../../t-sql/functions/datalength-transact-sql.md) 函數。 如果處理的是 Unicode 字串，DATALENGTH 會傳回可能不等於字元數目的數字。 下列範例會示範有尾端空白的 LEN 和 DATALENGTH。  
  
```sql  
  DECLARE @v1 VARCHAR(40),  
    @v2 NVARCHAR(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [VARCHAR LEN] , DATALENGTH(@v1) AS [VARCHAR DATALENGTH];  
SELECT LEN(@v2) AS [NVARCHAR LEN], DATALENGTH(@v2) AS [NVARCHAR DATALENGTH];  
```  

> [!NOTE]
> 使用 [LEN](../../t-sql/functions/len-transact-sql.md) 傳回編碼成所給定字串運算式的字元數目，使用 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 則傳回所給定字串運算式的大小 (以位元組為單位)。 取決於資料行中所使用的資料類型和編碼類型而，這些輸出可能會有所不同。 如需不同編碼類型之間儲存體差異的詳細資訊，請參閱[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)。

## <a name="examples"></a>範例  
 下列範例會選取 `FirstName` 居民的 `Australia` 字元數和資料。 這個範例會使用 AdventureWorks 資料庫。  
  
```sql  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回 `FirstName` 資料行中的字元數和 `Australia` 中之員工的名字和姓氏。  
  
```sql  
USE AdventureWorks2016  
GO  
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
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)   
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
