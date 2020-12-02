---
description: TRY_CAST (Transact-SQL)
title: TRY_CAST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current||>= sql-server-2016 ||>= sql-server-linux-2017||= sqlallproducts-allversions||>= aps-pdw-2016||= azure-sqldw-latest
ms.openlocfilehash: 02ec3dd7e7047411901dcaad4b76056781a9384c
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91379513"
---
# <a name="try_cast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  如果轉換成功，則會傳回轉換為指定之資料類型的值，否則會傳回 Null。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *expression*  
 要進行轉換的值。 任何有效的運算式。  
  
 *data_type*  
 *運算式* 轉換成的資料類型。  
  
 *length*  
 指定目標資料類型之長度的選擇性整數。  
  
 可接受值的範圍由 *data_type* 值決定。  
  
## <a name="return-types"></a>傳回型別  
 如果轉換成功，則會傳回轉換為指定之資料類型的值，否則會傳回 Null。  
  
## <a name="remarks"></a>備註  
 **TRY_CAST** 會採用傳遞給它的值，然後會嘗試將該值轉換為指定的 *data_type*。 如果轉換成功，**TRY_CAST** 會傳回當做指定之 *data_type* 的值；如果發生錯誤則會傳回 Null。 但是，若您要求明確不允許的轉換，則 **TRY_CAST** 會失敗並出現錯誤。  
  
 **TRY_CAST** 不是新的保留關鍵字，而且可在所有相容性層級使用。 當連接到遠端伺服器時，**TRY_CAST** 的語意與 **TRY_CONVERT** 相同。  
  
## <a name="examples"></a>範例  
  
### <a name="a-try_cast-returns-null"></a>A. TRY_CAST 傳回 null  
 以下的範例示範當轉換失敗時，TRY_CAST 會傳回 null。  
  
```sql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 下列範例示範運算式必須採用所需的格式。  
  
```sql  
SET DATEFORMAT dmy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-try_cast-fails-with-an-error"></a>B. TRY_CAST 失敗並出現錯誤  
 以下的範例示範當明確不允許轉換時，TRY_CAST 會傳回錯誤。  
  
```sql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 此陳述式的結果為錯誤，因為整數無法轉換為 xml 資料類型。  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-try_cast-succeeds"></a>C. TRY_CAST 成功  
 這個範例示範運算式必須採用所需的格式。  
  
```sql
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [TRY_CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
