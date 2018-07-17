---
title: DIFFERENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 692d3124814aaaeb25e7ec5507dc0a4ccf968b34
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781559"
---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函式會傳回整數值，以測量兩個不同字元運算式的 [SOUNDEX()](./soundex-transact-sql.md) 值之間的差異。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>引數  
*character_expression*  
字元資料的英數[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 *character_expression* 可以是常數、變數或資料行。  
  
## <a name="return-types"></a>傳回類型  
**int**  
 
## <a name="remarks"></a>Remarks  
`DIFFERENCE` 會比較兩個不同的 `SOUNDEX` 值，然後傳回整數值。 這個值會測量 `SOUNDEX` 值相符的程度，級別從 0 到 4。 值為 0 表示 SOUNDEX 值之間相似性弱或完全不相似；4 表示 SOUNDEX 值高度相似，或甚至完全相符。  
  
`DIFFERENCE` 和 `SOUNDEX` 會區分定序。  
  
## <a name="examples"></a>範例  
此範例的第一部分會比較兩個非常相似之字串的 `SOUNDEX` 值。 針對 Latin1_General 定序，`DIFFERENCE` 會傳回 `4` 的值。 範例的第二部分會比較兩個非常不同的字串之 `SOUNDEX` 值，而且針對 Latin1_General 定序，`DIFFERENCE` 會傳回 `0` 的值。  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [SOUNDEX &#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [字串函式 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

