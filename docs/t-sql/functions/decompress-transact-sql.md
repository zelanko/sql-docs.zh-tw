---
title: "解壓縮 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/30/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords: DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2988959b7ec3f9eccad74b752e7643f1e6675590
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="decompress-transact-sql"></a>解壓縮 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  解壓縮使用 GZIP 演算法的輸入的運算式。 壓縮的結果是位元組陣列 （varbinary （max） 類型）。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是**varbinary (***n***)**， **varbinary （max)**，或**二進位 (** *n***)**. 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="return-types"></a>傳回類型  
 傳回的資料型別**varbinary （max)**型別。 輸入引數被解壓縮 ZIP 演算法。 如有需要使用者應該明確轉換成目標類型的結果。  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
  
### <a name="a-decompress-data-at-query-time"></a>A. 在查詢階段解壓縮資料  
 下列範例會示範如何顯示資料表的壓縮資料：  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. 顯示使用計算資料行的壓縮的資料  
 下列範例會示範如何建立可儲存解壓縮的資料的資料表：  
  
```  
CREATE TABLE (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>請參閱＜  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;TRANSACT-SQL &#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
