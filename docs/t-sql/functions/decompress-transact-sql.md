---
title: DECOMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6d94ffd0182bfad3ed95f52640a2aed01ceeaa54
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68118966"
---
# <a name="decompress-transact-sql"></a>DECOMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

此函式會使用 GZIP 演算法來解壓縮輸入運算式值。 `DECOMPRESS` 會傳回位元組陣列 (VARBINARY(MAX) 類型)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
**varbinary(** _n_ **)** 、**varbinary(max)** 或 **binary(** _n_ **)** 值。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="return-types"></a>傳回型別  
**varbinary(max)** 資料類型的值。 `DECOMPRESS` 會使用 ZIP 演算法來解壓縮輸入引數。 使用者應明確將結果轉換成目標類型 (如有需要)。  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
  
### <a name="a-decompress-data-at-query-time"></a>A. 在查詢期間解壓縮資料  
此範例示範如何傳回壓縮的資料表資料：  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. 使用計算資料行顯示壓縮資料  
此範例示範如何建立資料表，以儲存解壓縮的資料：  
  
```  
CREATE TABLE example_table (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>另請參閱  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
