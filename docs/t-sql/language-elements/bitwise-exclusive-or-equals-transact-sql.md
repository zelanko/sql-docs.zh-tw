---
title: "^ = (位元互斥 OR EQUALS) (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/10/2017
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
- ^=
- ^=_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ^= (bitwise exclusive OR equals)
- compound operators, ^=
ms.assetid: ce524b0f-a24d-44e7-bd5b-b6943793cd48
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f7c69571c760fe828a6a731b348a12168b095cb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-exclusive-or-equals-transact-sql"></a>^= (位元互斥 OR EQUALS) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在兩個整數值之間執行位元排除 OR 運算，再將值設定為運算結果。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression ^= expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)之任何其中一個資料類型的數值分類，除非**元**資料型別。  
  
## <a name="result-types"></a>結果類型  
 傳回優先順序較高之引數的資料類型。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 如需詳細資訊，請參閱[^ &#40;位元互斥 OR &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md).  
  
## <a name="see-also"></a>另請參閱  
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [位元運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  

