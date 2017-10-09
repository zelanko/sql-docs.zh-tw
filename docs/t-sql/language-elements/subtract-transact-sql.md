---
title: "- （減）(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- subtract
- '-'
- -_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
- minus operator (-)
- subtracting numbers
ms.assetid: db23145f-f17d-4b90-be09-28a881cacd1a
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6f3013e03ddc1d7481c36be6ed8cce4cf4572c04
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="--subtract-transact-sql"></a>- (減) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  執行兩個數字的減法運算 (算術減法運算子)。 也可以從日期中減去一個數字 (表示天數)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression - expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)任一數字的資料類型的資料類型類別目錄，除了**元**資料型別。 不能與**日期**，**時間**， **datetime2**，或**datetimeoffset**資料型別。  
  
## <a name="result-types"></a>結果類型  
 傳回優先順序較高之引數的資料類型。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-subtraction-in-a-select-statement"></a>A. 在 SELECT 陳述式中使用減法  
 下列範例計算稅率最高的州省與稅率最低的州省之間的稅率差。  
  
 **適用於**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
```  
-- Uses AdventureWorks  
  
SELECT MAX(TaxRate) - MIN(TaxRate) AS 'Tax Rate Difference'  
FROM Sales.SalesTaxRate  
WHERE StateProvinceID IS NOT NULL;  
GO  
```  
  
 您可以使用括號來變更執行的順序。 首先會驗算括號內的計算。 如果是巢狀括號，最深的巢狀計算優先。  
  
### <a name="b-using-date-subtraction"></a>B. 使用日期減法  
 下列範例會從 `datetime` 日期中減去天數。  
  
 適用於：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @altstartdate datetime;  
SET @altstartdate = CONVERT(DATETIME, ''January 10, 1900 3:00 AM', 101);  
SELECT @altstartdate - 1.5 AS 'Subtract Date';  
```  
  
 以下為結果集：  
  
 ```
 Subtract Date  
 -----------------------  
 1900-01-08 15:00:00.000  

 (1 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-subtraction-in-a-select-statement"></a>C： 在 SELECT 陳述式中使用減法  
 下列範例會計算最高的基底費率的員工和與最低的稅率，員工的差異基底費率中從`dimEmployee`資料表。  
  
```  
-- Uses AdventureWorks  
  
SELECT MAX(BaseRate) - MIN(BaseRate) AS BaseRateDifference  
FROM DimEmployee;  
```  
  
## <a name="see-also"></a>另請參閱  
 [算術運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)   
 [-&#40;負數 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/unary-operators-negative.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [-= &#40;減 EQUALS &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)   
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



