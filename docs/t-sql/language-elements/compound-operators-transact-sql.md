---
title: 複合運算子 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 37539ab0a1d62d5393bff8df94c56c5cffb9ea8f
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982601"
---
# <a name="compound-operators-transact-sql"></a>複合運算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  複合運算子會執行某項作業，然後將原始值設定為該作業的結果。 例如，如果變數 @x 等於 35，則 @x += 2 會用 @x 的原始值加上 2，然後將 @x 設定為該新值 (37)。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會提供下列的複合運算子：  
  
|運算子|詳細資訊連結|動作|  
|--------------|------------------------------|------------|  
|+=|[+= &#40;加法指派&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|將原始值加上某數，然後將原始值設為該結果。|  
|-=|[-= &#40;減法指派&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)|從原始值減去某數，然後將原始值設為該結果。|  
|*=|[&#42;= &#40;乘法指派&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)|乘以某數，然後將原始值設為該結果。|  
|/=|[&#40;除法指派&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|除以某數，然後將原始值設為該結果。|  
|%=|[模數指派 &#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)|除以某數，然後將原始值設為該模數。|  
|&=|[&= &#40;位元 AND 指派&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|執行位元運算 AND，然後將原始值設為該結果。|  
|^=|[^= &#40;位元排除 OR 指派&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|執行位元排除 OR，然後將原始值設為該結果。|  
|&#124;=|[&#124;= &#40;位元 OR 指派&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)|執行位元運算 OR，然後將原始值設為該結果。|  
  
## <a name="syntax"></a>語法  
  
```  
  
expression operator expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是數值類別目錄中任何一個資料類型的任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="result-types"></a>結果類型  
 傳回優先順序較高之引數的資料類型。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 如需詳細資訊，請參閱與每個運算子相關的主題。  
  
## <a name="examples"></a>範例  
 下列範例將示範複合作業。  
  
```  
DECLARE @x1 int = 27;  
SET @x1 += 2 ;  
SELECT @x1 AS Added_2;  
  
DECLARE @x2 int = 27;  
SET @x2 -= 2 ;  
SELECT @x2 AS Subtracted_2;  
  
DECLARE @x3 int = 27;  
SET @x3 *= 2 ;  
SELECT @x3 AS Multiplied_by_2;  
  
DECLARE @x4 int = 27;  
SET @x4 /= 2 ;  
SELECT @x4 AS Divided_by_2;  
  
DECLARE @x5 int = 27;  
SET @x5 %= 2 ;  
SELECT @x5 AS Modulo_of_27_divided_by_2;  
  
DECLARE @x6 int = 9;  
SET @x6 &= 13 ;  
SELECT @x6 AS Bitwise_AND;  
  
DECLARE @x7 int = 27;  
SET @x7 ^= 2 ;  
SELECT @x7 AS Bitwise_Exclusive_OR;  
  
DECLARE @x8 int = 27;  
SET @x8 |= 2 ;  
SELECT @x8 AS Bitwise_OR;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [位元運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
