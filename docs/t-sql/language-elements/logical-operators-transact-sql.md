---
title: "邏輯運算子 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], logical
- testing truth
- truth testing
- TRUE
- FALSE
- logical operators [SQL Server], Transact-SQL
ms.assetid: edd92f08-76fb-4fd7-a4b6-8520d6a81df1
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa7f707ba758b6811f2fc8425bf4c2da96973e02
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="logical-operators-transact-sql"></a>邏輯運算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  邏輯運算子會測試是否符合某些狀況。 如同比較運算子，邏輯運算子會傳回**布林**資料類型值是 TRUE、 FALSE 或 UNKNOWN。  
  
|運算子|意義|  
|--------------|-------------|  
|[ALL](../../t-sql/language-elements/all-transact-sql.md)|如果一組比較全為 TRUE，便是 TRUE。|  
|[AND](../../t-sql/language-elements/and-transact-sql.md)|如果兩個布林運算式都是 TRUE 時，便是 TRUE。|  
|[任何](../../t-sql/language-elements/any-transact-sql.md)|如果一組比較中的任何一項是 TRUE，便是 TRUE。|  
|[之間](../../t-sql/language-elements/between-transact-sql.md)|如果運算元在範圍內，便是 TRUE。|  
|[存在](../../t-sql/language-elements/exists-transact-sql.md)|如果子查詢包含任何資料列，便是 TRUE。|  
|[在](../../t-sql/language-elements/in-transact-sql.md)|如果運算元等於運算式清單中的某個運算式，便是 TRUE。|  
|[類似](../../t-sql/language-elements/like-transact-sql.md)|如果運算元符合某個模式，便是 TRUE。|  
|[NOT](../../t-sql/language-elements/not-transact-sql.md)|反轉任何其他布林運算子的值。|  
|[或](../../t-sql/language-elements/or-transact-sql.md)|如果任一個布林運算式是 TRUE，便是 TRUE。|  
|[某些](../../t-sql/language-elements/some-any-transact-sql.md)|如果一組比較部分為 TRUE，便是 TRUE。|  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operator-precedence-transact-sql.md)  
  
  
