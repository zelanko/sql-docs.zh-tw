---
description: REPLICATE (Transact-SQL)
title: REPLICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REPLICATE_TSQL
- REPLICATE
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], repeating
- REPLICATE function
- repeating character expressions
ms.assetid: 0cd467fb-3f22-471a-892c-0039d9f7fa1a
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d047aa77ca0587a26225f8c0b180d81a8e48fb2d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462449"
---
# <a name="replicate-transact-sql"></a>REPLICATE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  將字串值重複指定的次數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
REPLICATE ( string_expression , integer_expression )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *string_expression*  
 這是字元字串或二進位資料類型的運算式。  
  
> [!NOTE]  
> 若 *string_expression* 是 **binary** 類型，則 REPLICATE 將會隱含轉換為 **varchar**，且因此不會保留二進位輸入。  

> [!NOTE]  
> 如果 *string_expression* 的類型是 **varchar(max)** 或 **nvarchar(max)** ，則 REPLICATE 會將傳回值截斷為 8,000 位元組。 若要傳回大於 8,000 位元組的值，*string_expression* 必須明確轉換成適當的大數值資料類型。  
  
 *integer_expression*  
 這是任何整數類型的運算式，包括 **bigint**。 如果 *integer_expression* 是負數，則會傳回 Null。  
  
## <a name="return-types"></a>傳回型別  
 傳回與 *string_expression* 相同的類型。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-replicate"></a>A. 使用 REPLICATE  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的產品線代碼前面重複 `0` 字元四次。  
  
```sql
SELECT [Name]  
, REPLICATE('0', 4) + [ProductLine] AS 'Line Code'  
FROM [Production].[Product]  
WHERE [ProductLine] = 'T'  
ORDER BY [Name];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name                                               Line Code  
-------------------------------------------------- ---------  
HL Touring Frame - Blue, 46                        0000T   
HL Touring Frame - Blue, 50                        0000T   
HL Touring Frame - Blue, 54                        0000T   
HL Touring Frame - Blue, 60                        0000T   
HL Touring Frame - Yellow, 46                      0000T   
HL Touring Frame - Yellow, 50                      0000T  
...  
```  
  
### <a name="b-using-replicate-and-datalength"></a>B. 使用 REPLICATE 和 DATALENGTH  
 下列範例會在數值資料類型轉換成字元或 Unicode 時，填補到指定的長度。  
  
```sql
IF EXISTS(SELECT name FROM sys.tables  
      WHERE name = 't1')  
   DROP TABLE t1;  
GO  
CREATE TABLE t1   
(  
 c1 varchar(3),  
 c2 char(3)  
);  
GO  
INSERT INTO t1 VALUES ('2', '2'), ('37', '37'),('597', '597');  
GO  
SELECT REPLICATE('0', 3 - DATALENGTH(c1)) + c1 AS 'Varchar Column',  
       REPLICATE('0', 3 - DATALENGTH(c2)) + c2 AS 'Char Column'  
FROM t1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Varchar Column        Char Column  
--------------------  ------------  
002                   2    
037                   37   
597                   597  
  
(3 row(s) affected)  
  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-replicate"></a>C.使用 REPLICATE  
 下列範例會在 `ItemCode` 值前面重複 `0` 字元四次。  
  
```sql
-- Uses AdventureWorks  
  
SELECT EnglishProductName AS Name,  
   ProductAlternateKey AS ItemCode,  
   REPLICATE('0', 4) + ProductAlternateKey AS FullItemCode  
FROM dbo.DimProduct  
ORDER BY Name;  
```  
  
 以下是結果集中的第一個資料列。  
  
 ```
Name                     ItemCode       FullItemCode
------------------------ -------------- ---------------
Adjustable Race          AR-5381        0000AR-5381
All-Purpose Bike Stand   ST-1401        0000ST-1401
AWC Logo Cap             CA-1098        0000CA-1098
AWC Logo Cap             CA-1098        0000CA-1098
AWC Logo Cap             CA-1098        0000CA-1098
BB Ball Bearing          BE-2349        0000BE-2349
 ```  
  
## <a name="see-also"></a>另請參閱  
 [SPACE &#40;Transact-SQL&#41;](../../t-sql/functions/space-transact-sql.md)  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

