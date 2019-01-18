---
title: 運算子優先順序 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 933212da81784d7d186fc6ef7c0cdfaa4edab24b
ms.sourcegitcommit: 7ead3a042d369315fc83a9ccc3d74f62e7b05bc0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2019
ms.locfileid: "54012314"
---
# <a name="operator-precedence-transact-sql"></a>運算子優先順序 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  當複雜運算式有多個運算子時，運算子優先順序會決定作業的執行順序。 執行的順序對結果值會有很大的影響。  
  
 下表顯示運算子的優先順序層級。 在較低層級的運算子之前，會評估較高層級的運算子 (在下列資料表中，1 是最高層級，8 是最低的層級)。
  
|層級|操作員|  
|-----------|---------------|  
|1|~ (位元 NOT)|  
|2|* (乘)、/ (除)、% (模數)|  
|3|+ (正)、- (負)、+ (加)、(+ 串連)、- (減)、& (位元 AND)、^ (位元互斥 OR)、&#124; (位元 OR)|  
|4|=、>、\<、>=、<=、<>、!=、!>、!< (比較運算子)|  
|5|NOT|  
|6|與|  
|7|ALL、ANY、BETWEEN、IN、LIKE、OR、SOME|  
|8|= (指派)|  
  
 當運算式中的兩個運算子有相同的運算子優先順序層級時，會依據它們在運算式中的位置，由左至右來評估它們。 例如，在下列 `SET` 陳述式所用的運算式中，會先評估減法運算子，再評估加法運算子。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 請利用括號來覆寫運算式中，已定義的運算子優先順序。 括號內的所有東西都會先評估得出單一值，之後，括號外的任何運算子便可以使用這個值。  
  
 例如，在下列 `SET` 陳述式所用的運算式中，乘法運算子的優先順序高於加法運算子。 因此，會先評估它；運算式結果是 `13`。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 在下列 `SET` 陳述式所用的運算式中，括號會使加法優先執行。 運算式結果是 `18`。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 如果運算式有巢狀括號，最內層的巢狀運算式最先評估。 下列範例包含巢狀括號，最內層的一組巢狀括號中的運算式是 `5 - 3`。 這個運算式會產生 `2` 值。 之後，加法運算子 (`+`) 會將這個結果加上 `4`。 這會產生 `6` 值。 最後，`6` 再乘以 `2`，得出運算式結果 `12`。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>另請參閱  
 [邏輯運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
