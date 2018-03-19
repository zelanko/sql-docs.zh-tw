---
title: DECOMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/30/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2988959b7ec3f9eccad74b752e7643f1e6675590
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="decompress-transact-sql"></a>DECOMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用 GZIP 演算法解壓縮輸入運算式。 壓縮的結果為位元組陣列 (VARBINARY(MAX) 類型)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 為 **varbinary(***n***)**、**varbinary(max)**，或 **binary(***n***)**。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="return-types"></a>傳回類型  
 傳回 **varbinary(max)** 類型的資料類型。 輸入引數會使用 ZIP 演算法進行解壓縮。 使用者應明確將結果轉換成目標類型 (若需要的話)。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>範例  
  
### <a name="a-decompress-data-at-query-time"></a>A. 在查詢期間解壓縮資料  
 下列範例示範如何顯示來自資料表的壓縮資料：  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. 使用計算資料行顯示壓縮資料  
 下列範例示範如何建立資料表，以儲存解壓縮資料：  
  
```  
CREATE TABLE (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>另請參閱  
 [字串函式 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
