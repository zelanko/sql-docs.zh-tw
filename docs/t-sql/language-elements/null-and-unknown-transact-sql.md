---
title: NULL 和 UNKNOWN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, pdw, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ff35786ca071881f25922ed955301fc8e38af2bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="null-and-unknown-transact-sql"></a>NULL 和 UNKNOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL 表示值是未知的。 NULL 值與空的值或零值不同。 兩個 Null 值永遠不會相等。 因為每個 NULL 的值都是未知的，兩個 Null 值之間、或是一個 NULL 與其他任何值之間的比較都會傳回未知的。  
  
 Null 值通常會指出未知的資料、不適用的資料或之後將要加入的資料。 例如，客戶的稱謂在下訂單時可能是未知的。  
  
 請注意下列有關 Null 值的事項：  
  
-   若要在查詢中測試 Null 值，請在 WHERE 子句中使用 IS NULL 或 IS NOT NULL。  
  
-   可以藉由在 INSERT 或 UPDATE 陳述式中明確地宣告 NULL 或將資料行保留在 INSERT 陳述式外，以將 Null 值插入資料行。  
  
-   Null 值不能當作區別資料表中的一個資料行與另一個資料行所需的資訊，例如主索引鍵或是用來散發資料行的資訊 (例如散發索引鍵)。  
  
 當資料中包含 Null 值時，邏輯與比較運算子可能會傳回第三種結果 UNKNOWN，而非只有 TRUE 或 FALSE。 這種三重數值邏輯的需要是造成應用程式錯誤的來源。 在包含 UNKNOWN 的布林運算式中的邏輯運算子會傳回 UNKNOWN，除非運算子的結果是以 UNKNOWN 運算式為根據。 這些表格提供此行為的範例。  
  
 下列表格顯示將 AND 運算子套用到兩個布林運算式的結果，其中一個運算式傳回 UNKNOWN。  
  
|運算式 1|運算式 2|結果|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|UNKNOWN|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|FALSE|  
  
 下列表格顯示將 OR 運算子套用到兩個布林運算式的結果，其中一個運算式傳回 UNKNOWN。  
  
|運算式 1|運算式 2|結果|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|TRUE|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|UNKNOWN|  
  
## <a name="see-also"></a>另請參閱  
 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
