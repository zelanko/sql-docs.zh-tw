---
title: 函式 (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 72f03d8d53e9d85b9b274ad1ac821fdfc79a6f24
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917007"
---
# <a name="functions-ssis-expression"></a>函數 (SSIS 運算式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  運算式語言包含一組可在運算式中使用的函數。 運算式可使用單一函數，但通常運算式會結合函數與運算子，並使用多個函數。  
  
 函數可分類成下列各群組：  
  
-   數學函數，執行以做為函數參數的數字輸入值為主的運算並傳回數值。  
  
-   字串函數，執行字串和十六進位輸入值的運算，並傳回字串或數值。  
  
-   日期和時間函數，執行日期和時間值的運算，並傳回字串、數值或日期和時間值。  
  
-   系統函數，會傳回運算式的資訊。  
  
 運算式語言提供下列數學函數。  
  
|函式|描述|  
|--------------|-----------------|  
|[ABS &#40;SSIS 運算式&#41;](../../integration-services/expressions/abs-ssis-expression.md)|傳回數值運算式的絕對正數值。|  
|[EXP &#40;SSIS 運算式&#41;](../../integration-services/expressions/exp-ssis-expression.md)|傳回做為指定運算式中 e 之基底的指數。|  
|[CEILING &#40;SSIS 運算式&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)|傳回大於或等於數值運算式的最小整數。|  
|[FLOOR &#40;SSIS 運算式&#41;](../../integration-services/expressions/floor-ssis-expression.md)|傳回小於或等於數值運算式的最大整數。|  
|[LN &#40;SSIS 運算式&#41;](../../integration-services/expressions/ln-ssis-expression.md)|傳回數值運算式的自然對數。|  
|[LOG &#40;SSIS 運算式&#41;](../../integration-services/expressions/log-ssis-expression.md)|傳回數值運算式以 10 為底的對數。|  
|[POWER &#40;SSIS 運算式&#41;](../../integration-services/expressions/power-ssis-expression.md)|傳回數值運算式的乘冪結果。|  
|[ROUND &#40;SSIS 運算式&#41;](../../integration-services/expressions/round-ssis-expression.md)|傳回已經進位到指定長度或有效位數的數值運算式。 。|  
|[SIGN &#40;SSIS 運算式&#41;](../../integration-services/expressions/sign-ssis-expression.md)|傳回數值運算式的正 (+)、負 (-) 或零 (0) 符號。|  
|[SQUARE &#40;SSIS 運算式&#41;](../../integration-services/expressions/square-ssis-expression.md)|傳回數值運算式的平方。|  
|[SQRT &#40;SSIS 運算式&#41;](../../integration-services/expressions/sqrt-ssis-expression.md)|傳回數值運算式的平方根。|  
  
 運算式評估工具提供下列字串函數。  
  
|函式|描述|  
|--------------|-----------------|  
|[CODEPOINT &#40;SSIS 運算式&#41;](../../integration-services/expressions/codepoint-ssis-expression.md)|傳回字元運算式最左邊字元的 Unicode 字碼值。|  
|[FINDSTRING &#40;SSIS 運算式&#41;](../../integration-services/expressions/findstring-ssis-expression.md)|傳回運算式中，所指定字元字串出現位置的以 1 為基底的索引。|  
|[HEX &#40;SSIS 運算式&#41;](../../integration-services/expressions/hex-ssis-expression.md)|傳回代表整數的十六進位值的字串。|  
|[LEN &#40;SSIS 運算式&#41;](../../integration-services/expressions/len-ssis-expression.md)|傳回字元運算式中的字元數。|  
|[LEFT &#40;SSIS 運算式&#41;](../../integration-services/expressions/left-ssis-expression.md)|傳回來自給定字元運算式最左邊部分的指定字元數。|  
|[LOWER &#40;SSIS 運算式&#41;](../../integration-services/expressions/lower-ssis-expression.md)|傳回將大寫字元轉換為小寫字元之後的字元運算式。|  
|[LTRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)|傳回移除開頭空白之後的字元運算式。|  
|[REPLACE &#40;SSIS 運算式&#41;](../../integration-services/expressions/replace-ssis-expression.md)|以不同的字串或空白字串取代運算式中的字串後，傳回字元運算式。|  
|[REPLICATE &#40;SSIS 運算式&#41;](../../integration-services/expressions/replicate-ssis-expression.md)|傳回重複了指定次數的字元運算式。|  
|[REVERSE &#40;SSIS 運算式&#41;](../../integration-services/expressions/reverse-ssis-expression.md)|傳回反向順序的字元運算式。|  
|[RIGHT &#40;SSIS 運算式&#41;](../../integration-services/expressions/right-ssis-expression.md)|傳回來自給定字元運算式最右邊部分的指定字元數。|  
|[RTRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)|傳回移除尾端空白之後的字元運算式。|  
|[SUBSTRING &#40;SSIS 運算式&#41;](../../integration-services/expressions/substring-ssis-expression.md)|傳回部份字元運算式。|  
|[TRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/trim-ssis-expression.md)|傳回移除開頭和尾端空白之後的字元運算式。|  
|[UPPER &#40;SSIS 運算式&#41;](../../integration-services/expressions/upper-ssis-expression.md)|傳回小寫字元轉換為大寫字元之後的字元運算式。|  
  
 運算式評估工具提供下列日期和時間函數。  
  
|函式|描述|  
|--------------|-----------------|  
|[DATEADD &#40;SSIS 運算式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)|藉由將日期或時間間隔加入至指定的日期，傳回新的 DT_DBTIMESTAMP 值。|  
|[DATEDIFF &#40;SSIS 運算式&#41;](../../integration-services/expressions/datediff-ssis-expression.md)|傳回跨越兩個指定日期的日期和時間界線數目。|  
|[DATEPART &#40;SSIS 運算式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)|傳回代表日期之日期部分的整數。|  
|[DAY &#40;SSIS 運算式&#41;](../../integration-services/expressions/day-ssis-expression.md)|傳回代表指定日期中日部份的整數。|  
|[GETDATE &#40;SSIS 運算式&#41;](../../integration-services/expressions/getdate-ssis-expression.md)|傳回系統目前的日期。|  
|[GETUTCDATE &#40;SSIS 運算式&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)|傳回以 UTC 時間 (Universal Time Coordinate 或 Greenwich Mean Time) 表示的系統目前日期。|  
|[MONTH &#40;SSIS 運算式&#41;](../../integration-services/expressions/month-ssis-expression.md)|傳回代表指定日期中月份的整數。|  
|[YEAR &#40;SSIS 運算式&#41;](../../integration-services/expressions/year-ssis-expression.md)|傳回代表指定日期中年份的整數。|  
  
 運算式評估工具提供下列 Null 函數。  
  
|函式|描述|  
|--------------|-----------------|  
|[ISNULL &#40;SSIS 運算式&#41;](../../integration-services/expressions/isnull-ssis-expression.md)|依據運算式是否為 Null 來傳回布林結果。|  
|[NULL &#40;SSIS 運算式&#41;](../../integration-services/expressions/null-ssis-expression.md)|傳回所要求資料類型的 Null 值。|  
  
 運算式名稱會以大寫字元顯示，但運算式名稱不區分大小寫。 例如，使用「null」與使用「NULL」的功能相同。  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)   
 [進階 Integration Services 運算式範例](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
