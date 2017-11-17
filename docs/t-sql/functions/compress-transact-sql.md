---
title: "壓縮 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c30cb5f351d9a84beec608483380edb94b8c7844
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="compress-transact-sql"></a>壓縮 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

壓縮使用 GZIP 演算法的輸入的運算式。 壓縮的結果是位元組陣列的型別**varbinary （max)**。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>引數  
*expression*  
是**nvarchar (***n***)**， **nvarchar （max)**， **varchar (** *n*  **)**， **varchar （max)**， **varbinary (**  *n*  **)**， **varbinary （max)**， **char (***n***)**， **nchar (**  *n*  **)**，或**二進位 (***n***)**運算式。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。
  
## <a name="return-types"></a>傳回型別
傳回的資料型別**varbinary （max)**表示輸入的壓縮的內容。
  
## <a name="remarks"></a>備註  
壓縮的資料無法編製索引。
  
COMPRESS 函數壓縮提供為輸入運算式的資料，與必須叫用每個區段之壓縮的資料。 在儲存期間資料列或頁面層級自動壓縮，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。
  
## <a name="examples"></a>範例  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. 資料表插入期間壓縮資料  
下列範例顯示如何壓縮資料插入至資料表：
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. 封存壓縮的版的已刪除的資料列  
下列陳述式會刪除舊的播放程式記錄，從`player`資料表，並儲存在記錄`inactivePlayer`壓縮格式，以節省空間的資料表。
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>另請參閱
[字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[解壓縮 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  

