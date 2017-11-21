---
title: "Microsoft SQL 資料庫函式有哪些？ | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- built-in functions [SQL Server]
- function [SQL Server] See functions [SQL Server]
- functions [Transact-SQL]
- functions [SQL Server], about functions
- scalar functions
- functions [SQL Server]
ms.assetid: 17186213-5ab5-40b0-b470-b660af1ec44c
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53a2a1be1099b2224b14f8c8d856b7ae07d42ac6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="what-are-the-sql-database-functions"></a>SQL 資料庫函式有哪些？
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

深入了解您可以使用 SQL 資料庫的內建函式類別。 您可以使用內建函數，或建立您自己的使用者定義函數。
  
## <a name="aggregate-functions"></a>彙總函式

彙總函式會根據一組值來執行計算，再傳回單一值。 允許在 select 清單或 HAVING 子句的 SELECT 陳述式。 您可以使用與 GROUP BY 子句一起使用的彙總來計算的資料列的類別上的彙總。 您可以使用 OVER 子句來計算特定範圍的值上的彙總。 OVER 子句不能跟在 GROUPING 或 GROUPING_ID 彙總。

所有彙總函式不具決定性，這表示它們一律傳回相同的值，當它們在相同的輸入值上執行。 如需詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。 |

## <a name="analytic-functions"></a>分析函數
分析函數會根據資料列群組計算出彙總值。 不過，與不同的彙總函式，是分析函數可以傳回每個群組的多個資料列。 您可以使用分析函數來計算移動平均，累計總數、 百分比或前 N 結果群組內。

## <a name="ranking-functions"></a>排名函數
排名函數會傳回資料分割中每個資料列的次序值。 根據所用的函數而定，有些資料列可能會收到與其他資料列相同的值。 排名函數不具決定性。

## <a name="rowset-functions"></a>資料列集函數
資料列集函數會傳回可以用做為 SQL 陳述式中的資料表參考的物件。

## <a name="scalar-functions"></a>純量函數
處理單一值，再傳回單一值。 凡是運算式有效之處，都能夠使用純量函數。

### <a name="categories-of-scalar-functions"></a>純量函式類別
  
|函數類別目錄|Description|  
|-----------------------|-----------------|  
|[組態函數](configuration-functions-transact-sql.md)|傳回目前組態的詳細資訊。|  
|[轉換函式](conversion-functions-transact-sql.md)|支援資料類型轉型及轉換。|  
|[資料指標函數](cursor-functions-transact-sql.md)|傳回資料指標的詳細資訊。|  
|[日期和時間資料型別和函式](date-and-time-data-types-and-functions-transact-sql.md)|執行作業來處理日期和時間輸入值，以及傳回字串、數值，或日期和時間值。|  
|[JSON 函式](json-functions-transact-sql.md)|驗證、 查詢或變更 JSON 資料。|  
|[邏輯函數](http://msdn.microsoft.com/library/5b2b4546-951b-462d-91d5-e41fc5acd6f9)|執行邏輯運算。|  
|[數學函式](mathematical-functions-transact-sql.md)|根據函數參數所提供的輸入值來執行計算，以及傳回數值。|  
|[中繼資料函數](metadata-functions-transact-sql.md)|傳回資料庫和資料庫物件的相關資訊。|  
|[安全性函數](security-functions-transact-sql.md)|傳回使用者和角色的相關資訊。|  
|[字串函式](string-functions-transact-sql.md)|在字串上執行作業 (**char**或**varchar**) 輸入值，並傳回字串或數值的值。|  
|[系統函式](../../relational-databases/system-functions/system-functions-for-transact-sql.md)|執行作業和傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的值、物件和設定的相關資訊。|  
|[系統統計函數](system-statistical-functions-transact-sql.md)|傳回系統的統計資訊。|  
|[文字和影像函數](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|執行作業來處理文字或影像輸入值或資料行，以及傳回值的相關資訊。|  
  
## <a name="function-determinism"></a>函數決定性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內建函數可能具決定性或不具決定性。 如果每當利用一組特定輸入值來呼叫函數時，函數都會傳回相同的值，這些函數便是具決定性。 如果每次呼叫時都可能傳回不同結果，即便使用同一組特定的輸入值也是如此，這些函數便是不具決定性。 如需詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)  
  
## <a name="function-collation"></a>函數定序  
 採取字元字串輸入、傳回字元字串輸出的函數，輸出會使用輸入字串的定序。  
  
 使用非字元輸入並傳回字元字串的函數，輸出會使用目前資料庫的預設定序。  
  
 採取多重字元字串輸入、傳回單一字元字串的函數，會利用定序優先順序的規則來設定輸出字串的定序。 如需詳細資訊，請參閱[定序優先順序 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
## <a name="see-also"></a>另請參閱  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [決定性與非決定性的函式](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)   
 [使用預存程序 &#40;MDX &#41;](../../mdx/using-stored-procedures-mdx.md)  
  
  

