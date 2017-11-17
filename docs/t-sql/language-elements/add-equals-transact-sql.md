---
title: "+ = （加 EQUALS） (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- +=
- +=_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- += (add equals)
- compound operators, +=
ms.assetid: 9ea52519-80d1-473f-b988-0572f0e2c92f
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0d07ab123822db8f381af6fcc4f1707529bed359
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="-add-equals-transact-sql"></a>+= (加 EQUALS) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  兩數相加，再將值設定為運算結果。 例如，如果變數@x等於 35，然後@x+ = 2 會的原始值@x，新增 2 和集合@x為該新值 (37)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression += expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)除了數字的類別目錄中任何資料型別的**元**資料型別。  
  
## <a name="result-types"></a>結果類型  
 傳回優先順序較高之引數的資料類型。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 如需詳細資訊，請參閱[+ &#40;新增 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/add-transact-sql.md).  
  
## <a name="see-also"></a>另請參閱  
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+ = &#40;字串串連 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)  
  
  

